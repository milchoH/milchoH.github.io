---
layout: post
title: "What is Cross-Site Scripting"
date: 2019-08-12
image: whatIsXss.jpg
category: tutorials
tags: tutorial xss information

---

# What is XSS
Cross-Site Scripting (XSS) attacks are type of injection, in which malicious scripts are injected into websites. The injected script can access cookies, session tokens or other sensitive information retained by the browser and used with the vulerable site.

# Types of XSS Attacks
XSS attacks can be categorized in three categories - stored, reflected and DOM based

## Stored XSS Attacks
Stored (Persistent or Type-I XSS) attacks are those, where the injected script is stored on the target servers e.g. message in forum, visitor log, comment fields, etc. After the XSS is stored, it is then executed by every visitor, attepting to view the page where it is stored.

## Reflected XSS Attacks
Reflected (Non-Persistent or Type-II XSS) attacks are those, where the injected script is reflected off the web server e.g. ub ab error message, search result or any other response, that includes some or all of the input sent to the server as part of the request. These attacks are delivered to the victims via other routes e.g. phishing - malicious e-mail, links in other websites, IMs, etc. 

## DOM Based XSS
DOM Based XSS(or Type-0) as defined by Amit Klein, who published the first article about this issue[1], DOM Based XSS is a form of XSS where the entire tainted data flow from source to sink takes place in the browser, i.e., the source of the data is in the DOM, the sink is also in the DOM, and the data flow never leaves the browser. For example, the source (where malicious data is read) could be the URL of the page (e.g., document.location.href), or it could be an element of the HTML, and the sink is a sensitive method call that causes the execution of the malicious data (e.g., document.write)."

# Sources

[Cross-Site scripting on OWASP](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS))

[Types of Cross-Site scripting](https://www.owasp.org/index.php/Types_of_Cross-Site_Scripting)

[DOM Based Cross Site Scripting or XSS of the Third Kind (WASC writeup), Amit Klein, July 2005](http://www.webappsec.org/projects/articles/071105.shtml)
