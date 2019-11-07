---
keywords:
  - github
  - interesting
comments: true
title: What is github.com.cnpmjs.org
cover_image: https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/china_github.jpg
---

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/china_github.jpg)

TLDR; this is an proxy for high speed access to github repo in China

My friend was browsing around and stumble upon this github page which looks legit. But, when you look close at the url, the domain belongs to an open source ([https://github.com/cnpm/cnpmjs.org](https://github.com/cnpm/cnpmjs.org)) private npm registry project. 

By doing a quick search on ICANN, it seems like the domain was registered from GoDaddy and belongs to a owner from Zhejiang, China. Tracing the IP address of the domain, it belongs to Alibaba cloud service (Aliyun) in Singapore.

![](https://raw.githubusercontent.com/theblackcat102/theblackcat102.github.io/master/images/github_cnpmjs_nope.png)

For any programmer this should be a huge red flag as a possible phishing site to access your sweet password and username right?

But no sane hacker would also use a legit domain (cnpmjs.org) to host a phishing site as well right?

A quick search on google, github, duckduckgo to find any mentions about this domain, I found a github [issue #4823 from ant-design](https://github.com/ant-design/ant-design-pro/issues/4823) contain details about the origins of github.com.cnpmjs.org.

Aparrently this is suppose to be an proxy for china to clone github projects. From the test mentioned in this issue shows this github clone is roughly 2X faster than github.com in cloning task.

However, the domain do provide a fully clone interface of github and register interface for user to login in/sign up. I tried to sign in ( and sign up) using a burner account, and the website always redirect me to the 404 page. Search function on github.com.cnpmjs.org works but sometimes slows (probably due to the extra routing time).


