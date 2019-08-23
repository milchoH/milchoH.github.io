---
layout: post
title: "XXE Basics"
author: milchoH
date: 2019-08-23
image: XXE.png
category: tutorials

---

# What is XXE
An XML External Entity attack is a type of attack against an application that parses XML input. This attack occurs when XML input containing a reference to an external entity is processed by a weakly configured XML parser. This attack may lead to the disclosure of confidential data, denial of service, server side request forgery, port scanning from the perspective of the machine where the parser is located, and other system impacts.[1]

# Types of XXE

There are various types of XXE attacks:

- **Exploiting XXE to retrieve files**, where an external entity is defined containing the contents of a file, and returned in the application's response.
- **Exploiting XXE to perform SSRF attacks**, where an external entity is defined based on a URL to a back-end system.
- **Exploiting blind XXE exfiltrate data out-of-band**, where sensitive data is transmitted from the application server to a system that the attacker controls.
- **Exploiting blind XXE to retrieve data via error messages**, where the attacker can trigger a parsing error message containing sensitive data.[2]

# Example scenarios

For this example I will use Portswigger's labs in order to demonstrate how we can retrieve files using XXE.[3]

An example scenario can be a web application, that checks if items are in stock in certain store. So the application can be sending requests like: 

![Image](/images/InitialRequest.png)

Which result in such responses:

![Image](/images/InitialResponse.png)

In order to try exploiting the XML parser and accessing a the **etc/passwd** file on the target system, we can create a modified request looking like:

![Image](/images/ExploitRequest.png)

And if the application is vulnerable and the attack is successfull, we should receive response looking like:

![Image](/images/ExploitResponse.png)

# References

1. [OWASP XML External Entity (XXE) Processing](https://www.owasp.org/index.php/XML_External_Entity_(XXE)_Processing)
2. [Portswigger XML external entity (XXE) injection](https://portswigger.net/web-security/xxe#exploiting-xxe-to-perform-ssrf-attacks)
3. [Portswigger XXE file retrival lab](https://portswigger.net/web-security/xxe/lab-exploiting-xxe-to-retrieve-files)