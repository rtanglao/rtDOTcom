---

layout: post
title: "Gene Kim: Love Letter To Clojure (Part 1) & Ruby's chevron operator, '<<' mutates"
---

# Pontifications

* Blown out of the water by Gene Kim: [Love Letter To Clojure (Part 1)](https://itrevolution.com/love-letter-to-clojure-part-1/) <-- READ THE WHOLE THING!
* I too didn't realize that the "chevron" operator, `<<` mutates the string!

```ruby
>> s = "hello" 
=> "hello" 
>> s << "*" 
=> "hello*" 	# s value was mutated!!!!
>> s == "hello" 
=> false
```