---
layout: post
title: Scraping a scrolling Ajaxy log page with Python, Beautiful Soup, and Selenium
---

## Pontifications

* See [Managed to extract Hub live log for my usage via python script](https://community.smartthings.com/t/managed-to-extract-hub-live-log-for-my-usage-via-python-script/77837)
* amazing what you can do with scrapers :-) I bet I can reuse this code when scraping instagram, flickr and other places where the API is going to stop functioning.
* I only copy and pasted the code below because I don't trust S*msung to keep the Smart Things website up.

### Code by Philippe_Portes:

```python
import platform
from bs4 import BeautifulSoup
from selenium import webdriver
import datetime
import time
import re
import difflib

login_l = 'yourSTusername'
password_l='yourSTpassword'

#function to extract needed string
def xstr(s):
if (s==None) or len(s)==0:
    return ""
else:  
    return ''.join(s)

# PhantomJS files have different extensions
# under different operating systems
if platform.system() == 'Windows':
PHANTOMJS_PATH = './phantomjs.exe'
else:
PHANTOMJS_PATH = './phantomjs'

# Initialize difflib for later usage
d= difflib.Differ()

# here we'll use pseudo browser PhantomJS,
# but browser can be replaced with browser = webdriver.FireFox(),
# which is good for debugging.
browser = webdriver.PhantomJS(PHANTOMJS_PATH)
browser.get('https://graph-na02-useast1.api.smartthings.com/login/auth')
username = browser.find_element_by_name('j_username')
password = browser.find_element_by_name('j_password')
username.send_keys(login_l)
password.send_keys(password_l)

browser.find_element_by_name('_action_Log in').click();
#time.sleep(10) # to replace by a page.load detection to ensure the login was successfully done.
print "Authenticating :",

while(login_l not in browser.page_source):
print ".",
print ""
print "Authenticated as ", login_l
browser.get('https://graph-na02-useast1.api.smartthings.com/ide/logs')

# variable needed log and page parsing management
first_log_trace=''
log_trace=''
old_page=''

#CSV file name
csv_file_name=''
last_file_name=''

print "Parsing...",

while (True):            
time.sleep(10) # put a sleep to avoid socket get messed-up while in WAIT state

#Check if the page content changed (=new logs)
while browser.page_source==old_page:
    pass
   
# new page content, we'll have to write things in the log file
new_log=1

#Prepare for file name based on the date.
timestr = time.strftime("%Y%m%d")

# first logs in this file might include last minutes of the day before logs
logfile= open(timestr+".csv","a+")

# If new file name, add csv header.
if last_file_name!=timestr+'.csv':
    # write csv header
    logfile.write('"Log_Class";"Device_Name";"Local_Log_Time";"Log_Message"')
    last_file_name=timestr+".csv"
    
# Prepare to parse page
new_page=browser.page_source

soup = BeautifulSoup(new_page, "html.parser")

# keep track of the page content to avoid reloading same page content
old_page=new_page

# We'll put the device names and the corresponding href used by ST logs to put the name in clear in the logs we export
devicename_dic={}
# the devices already traced are added as filters option on the top of the window,
# checking all element of <a class=filter> help to know the correspondance between later href URL and ST device names 
div_tools = soup.findAll('div', {'class':'tools'}) 
# loop in the device names
for child in div_tools:
    device_href_name=child.findAll('li')
    for href in device_href_name:
        device_href=re.search('.*href="(.*)".*', str(href.a))
        device_name=re.search('.*href=.*>(.*)</a>', str(href.a))
        if device_name != None:
            devicename_dic[str(device_href.group(1))]=str(device_name.group(1))
# search for the div sections with style attributes containing the logs
div_class_body = soup.findAll('div', {'style':'display: block;'})

for child in div_class_body:
    log_class=xstr(re.findall('<div class="(.*?)".*', str(child)))
    # extract the url from the console log and match it to the device name we stored.
    device_href=xstr(re.findall('.*href="(.*)".*', str(child)))
    # extract the time. Will be in format (H)H:(M)M:(S)S AM/PM TZ
    log_time=xstr(re.findall('<span class="time">(.*?)</span>', str(child)))
    # extract the log message text.
    log_msg=xstr((re.findall('.*msg">(.*?)</span>', str(child), re.MULTILINE)))
    # build the string. Due to ST displays the newest first, each line will be written in the file in the new->old order for this group
    # example:
    # [c
    #  b
    #  a] ==> first set of logs 
    # [f
    #  e] ==> second set of logs
    # This is not really important as file can be reordered by the program using the csv file. However, smartthings doesn't add the day 
    log_trace = '"'+log_class+ '";'+'"'+ devicename_dic.get(device_href,"")+ '";'+'"'+log_time+'";'+'"'+log_msg+'"\n'
    
    # events being in reverse date order, stop writing to files events already written last time.
    if (log_trace==first_log_trace ):
        new_log=0
    #first time parsing? then write csv header in the file and set variables for next time in order to avoid writing past events
    if first_log_trace=='':
        first_log_trace=log_trace
        new_log=1
    # got new logs? print them in the file
    if new_log==1:
        print log_trace
        logfile.write(log_trace)
   
logfile.close
```

```
Example of logs as csv file I got:
"Log_Class";"Device_Name";"Local_Log_Time";"Log_Message"
"log debug";"Arrival Sensor guest";"3:55:14 PM PST";"Creating battery event for voltage=2.2V: Arrival Sensor guest battery is 70%"
```