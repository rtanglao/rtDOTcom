---
layout: post
title: "(All) DNS Resource Records <-- doesn't have ALIAS records?!? <-- Alias records are a non standard way to alias apex domains"
---
*  [(All) DNS Resource Records](https://www.netmeister.org/blog/dns-rrs.html) <-- doesn't have ALIAS records?!? 
* Apparently, ALIAS records are a non standard way to alias apex domains.
  * CloudFlare calls this `CNAME flattening`. See 2014 blog post: [Introducing CNAME Flattening: RFC-Compliant CNAMEs at a Domain's Root](https://blog.cloudflare.com/introducing-cname-flattening-rfc-compliant-cnames-at-a-domains-root/): `Traditionally, the root record of a domain needed to point to an IP  address (known as an A -- for "address" -- Record). While it may not  seem like a big deal, tying a service to an IP address can be extremely  limiting.`
  * [Azure DNS alias records overvie](https://docs.microsoft.com/en-us/azure/dns/dns-alias)w: `As described previously, CNAME records aren't supported at the zone  apex. You can’t use a CNAME record to point contoso.com to your CDN  endpoint. Instead, you can use an alias record to point the zone apex to a CDN endpoint directly.`
  * [AWS Route 53 Choosing between alias and non-alias records](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-choosing-alias-non-alias.html): `You can't create a CNAME record that has the same name as the hosted  zone (the zone                              apex). This is  true both for hosted zones for domain names (example.com) and for hosted zones for  subdomains (zenith.example.com).`                                                   `
  * Namecheap: [How to create an ALIAS record](https://www.namecheap.com/support/knowledgebase/article.aspx/10128/2237/how-to-create-an-alias-record/)

