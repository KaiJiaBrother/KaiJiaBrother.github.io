---
title: Why my website is not secure?
tags: hexo
categories: hexo
abbrlink: 4d1d841d
date: 2020-04-10 17:13:31
---
{% cq %}After I updated NexT from v7.7.1 to the latest version(v7.8.0), the secure site suffers from the problem of mixed content.{% endcq %}
<!-- more -->

> Using `HTTPS` instead of `HTTP` means that communications between your browser and a website is encrypted via the use of an `SSL (Secure Socket Layer)`. Even if your website doesn’t handle sensitive data, it’s a good idea to make sure your website loads securely over HTTPS. It’s now becoming a requirement for many new browser features as well as potentially having an impact on search engine rankings.

1. When I enable `Enforce HTTPS`, the website is available over HTTPS.

![Enforce HTTPS](/images/why-my-website-is-not-secure/1.png)

2. However, today I found the website became not secure.

![Not fully secure](/images/why-my-website-is-not-secure/2.png)

3. So I checked the certificate to ensure it was still valid.

![The certificate is still within its validity](/images/why-my-website-is-not-secure/3.png)

4. Next, I checked the Console and found the problem.

![It was a problem of Mixed Content!](/images/why-my-website-is-not-secure/4.png)

{% note info %}
Mixed content means the green padlock icon will not be displayed for an `https://` site because, in fact, it’s not truly secure.

Here’s the problem: if an `https://` website includes any content from a site (even its own) served over `http://`, the green padlock can’t be displayed. That’s because resources like images, JavaScript, audio, video etc. included over `http://` open up a security hole into the secure website. A backdoor to trouble.

Today, Google Chrome shows a `circled i` on any `https://` that has insecure content.

To get a green padlock from either of these browsers requires every single subresource (resource loaded by a page) to be served over HTTPS.
{% endnote %}

5. So where is the insecure image `http://www.baidu.com/search/error.html` from?

![I found the link!](/images/why-my-website-is-not-secure/5.png)

6. After that, I went to Resources and found this link. The {% label danger@Status Code %} is `307 Internal Redirect` which means we need to check previous requests!

![Check previous requests from Request initiator chain](/images/why-my-website-is-not-secure/7.png)

7. An exciting finding! The link `https://zz.bdstatic.com/linksubmit/push.js` works but the link `https://sp0.baidu.com/9_Q4simg2RQJ8t7jm9iCKT-xh_/s.gif?l=https://kaijiadage.com/` has a problem, how do they work here?

8. According to [this article](https://ziyuan.baidu.com/college/articleinfo?id=1587) from baidu platform and the results that we can see from `Request initiator chain`. Both two links are used when our blogs are pushed to baidu for SEO.

![The baidu JavaScript for pushing code to baidu](/images/why-my-website-is-not-secure/6.png)

9. As we can see from this picture, we can clearly know where the previous link `.../push.js` comes from.

   And when we open this JavaScript file, we can clearly see where the latter link comes form.

![The latter link](/images/why-my-website-is-not-secure/8.png)

10. when the latter link didn't work, it navigated to the error page. So that was the problem.

![The latter link](/images/why-my-website-is-not-secure/9.png)

11. More importantly, how can we solve this problem?
- Obviously, `baidupush` function is not really necessary, so we can simply turn off it.
- If we still need to use this function, we need to learn more about how this funtion work. So here we go!
- 刚才在第8点里，我们提到了一段JavaScript代码，只要把这段代码放入每个页面中（这个`hexo`已经做了），每当用户访问这些页面时，就会通过这段JavaScript从百度下载一个1x1的`gif`（即出错的链接来源），将window.location.href等信息推送给百度，同时记录页面此时此刻的URL地址（出错链接传参就是页面URL地址）。
- More solutions could be found in [this post](https://blog.cloudflare.com/fixing-the-mixed-content-problem-with-automatic-https-rewrites/)
- 暂时未想到其他方法，先关闭百度推送功能。

Reference:
1. [20i.com](https://www.20i.com/support/ssl-certificates/force-https)
2. [blog.cloudflare.com](https://blog.cloudflare.com/fixing-the-mixed-content-problem-with-automatic-https-rewrites/)
3. [ziyuan.baidu.com](https://ziyuan.baidu.com/college/articleinfo?id=1587)
