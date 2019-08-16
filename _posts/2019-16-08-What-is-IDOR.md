---
layout: post
title: "What is IDOR"
author: milchoH
date: 2019-08-16
image: whatIsIDOR.jpg
category: tutorials

---

# Quick word on authorization and authentication
Authenticatin lets the application know who is using the app, while authorization means the level of features you have and the level of actions you can perform. [1]
```
IDOR occurs when an application refers to some other internal objects via different parameters in an insecure manner. - Abartan Dhakal
```

# What is Insecure Direct Object Reference(IDOR)
Insecure Direct Object References occur when an application provides direct access to objects based on user-supplied input. The result is the attacker can bypass authorization and access resources in the system directly by modifying the value of a parameter used to directly point to object.

# How to test
The best way to test for IDOR would be having two or more users with different privileges and access to different objects e.g. common user account, manager account and admin account. Then the tester starts exploring every feature, he has access to, with every account while all requests are being documented by a proxy. After the exploration the requests, done by e.g. the admin account can be run again using the common user account. 

Sample request 

```
http://foo.bar/changepassword?user=someuser
```
In this case, the value of the `user` parameter is used to tell the application for which user it should change the password. In many cases this step will be a part of a wizard, or a multi-step operation. In the first step the application will get a request stating for which user's password is to be changed, and in the next step the user will provide a new password (without asking for the current one).

The `user` parameter is used to directly reference the object of the user for whom the password change operation will be performed. To test for this case the tester should attempt to provide a different test username than the one currently logged in, and check whether it is possible to modify the password of another user. [2]

# Conclusion
This is a highly paid vulnerability affecting authorization. It is easy to exploit and easy to detect. If the business value of the exposed data is high, the impact severity can vary from MODERATE to CRICICAL.

# References

1. [Secjuice on IDOR](https://www.secjuice.com/idor-insecure-direct-object-reference-definition/)
2. [OWASP testing for Insecure Direct Object References](https://www.owasp.org/index.php/Testing_for_Insecure_Direct_Object_References_(OTG-AUTHZ-004))