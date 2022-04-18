---
title: OWASP top10💻
tag: 信息安全
date: 2021/04/08
---
~~可以直接看目录~~
# OWASP top10 
因为网上top10众说纷纭（可能是版本问题），于是我去owasp官网找到了最新的top10，[官网链接](https://owasp.org/www-project-top-ten/)，有任何问题，请参考官网。
## [注入 Injection. ](https://owasp.org/www-project-top-ten/2017/A1_2017-Injection)
Injection flaws, such as SQL, NoSQL, OS, and LDAP injection, occur when untrusted data is sent to an interpreter as part of a command or query. The attacker’s hostile data can trick the interpreter into executing unintended commands or accessing data without proper authorization.
## [失效的身份验证 Broken Authentication. ](https://owasp.org/www-project-top-ten/2017/A2_2017-Broken_Authentication)
Application functions related to authentication and session management are often implemented incorrectly, allowing attackers to compromise passwords, keys, or session tokens, or to exploit other implementation flaws to assume other users’ identities temporarily or permanently.
## [敏感信息泄露 Sensitive Data Exposure. ](https://owasp.org/www-project-top-ten/2017/A3_2017-Sensitive_Data_Exposure)
Many web applications and APIs do not properly protect sensitive data, such as financial, healthcare, and PII. Attackers may steal or modify such weakly protected data to conduct credit card fraud, identity theft, or other crimes. Sensitive data may be compromised without extra protection, such as encryption at rest or in transit, and requires special precautions when exchanged with the browser.
## [XML外部实体漏洞 XML External Entities (XXE). ](https://owasp.org/www-project-top-ten/2017/A4_2017-XML_External_Entities_(XXE))
Many older or poorly configured XML processors evaluate external entity references within XML documents. External entities can be used to disclose internal files using the file URI handler, internal file shares, internal port scanning, remote code execution, and denial of service attacks.
## [失效的访问控制 Broken Access Control. ](https://owasp.org/www-project-top-ten/2017/A5_2017-Broken_Access_Control)
Restrictions on what authenticated users are allowed to do are often not properly enforced. Attackers can exploit these flaws to access unauthorized functionality and/or data, such as access other users’ accounts, view sensitive files, modify other users’ data, change access rights, etc.
## [安全配置错误 Security Misconfiguration. ](https://owasp.org/www-project-top-ten/2017/A6_2017-Security_Misconfiguration)
Security misconfiguration is the most commonly seen issue. This is commonly a result of insecure default configurations, incomplete or ad hoc configurations, open cloud storage, misconfigured HTTP headers, and verbose error messages containing sensitive information. Not only must all operating systems, frameworks, libraries, and applications be securely configured, but they must be patched/upgraded in a timely fashion.
## [跨站脚本攻击 Cross-Site Scripting (XSS). ](https://owasp.org/www-project-top-ten/2017/A7_2017-Cross-Site_Scripting_(XSS))
XSS flaws occur whenever an application includes untrusted data in a new web page without proper validation or escaping, or updates an existing web page with user-supplied data using a browser API that can create HTML or JavaScript. XSS allows attackers to execute scripts in the victim’s browser which can hijack user sessions, deface web sites, or redirect the user to malicious sites.
## [不安全的反序列化 Insecure Deserialization. ](https://owasp.org/www-project-top-ten/2017/A8_2017-Insecure_Deserialization)
Insecure deserialization often leads to remote code execution. Even if deserialization flaws do not result in remote code execution, they can be used to perform attacks, including replay attacks, injection attacks, and privilege escalation attacks.
## [使用含有已知漏洞的组件 Using Components with Known Vulnerabilities. ](https://owasp.org/www-project-top-ten/2017/A9_2017-Using_Components_with_Known_Vulnerabilities)
Components, such as libraries, frameworks, and other software modules, run with the same privileges as the application. If a vulnerable component is exploited, such an attack can facilitate serious data loss or server takeover. Applications and APIs using components with known vulnerabilities may undermine application defenses and enable various attacks and impacts.
## [不足的日志记录和监控 Insufficient Logging & Monitoring. ](https://owasp.org/www-project-top-ten/2017/A10_2017-Insufficient_Logging%2526Monitoring)
Insufficient logging and monitoring, coupled with missing or ineffective integration with incident response, allows attackers to further attack systems, maintain persistence, pivot to more systems, and tamper, extract, or destroy data. Most breach studies show time to detect a breach is over 200 days, typically detected by external parties rather than internal processes or monitoring.