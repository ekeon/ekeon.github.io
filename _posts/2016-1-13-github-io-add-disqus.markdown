---
layout: post
title:  "github.io add disqus!"
date:   2016-01-13 5:44
categories: jekyll update
---

<a href="https://disqus.com/">Disqus</a> 들어가서 signup 해준다.
![disqus1](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus1.png)
오른쪽 Add Disqus To Stie Click
![disqus2](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus2.png)
Start Using Engage
![disqus3](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus3.png)
다 적은후 Finish registration.
![disqus4](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus4.png)
Universal Code 클릭
![disqus5](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus5.png)
아래 소스코드 copy
![disqus6](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus6.png)

자신의 includes 폴더안에 comments.html 생성 해주고 아까 copy 한 내용을 복사해준후 post.html 에 추가해준다.
post.html 은 테마나 사람마다 다를수있슴.

    <html lang="en">
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <title>{% if page.title %}{{ page.title }}{% else %}{{ site.name }}{% endif %}</title>
      <link rel="stylesheet" href="//fonts.googleapis.com/css?family=Source+Sans+Pro:300,300i,600">
      <link rel="stylesheet" href="{{ site.baseurl }}/style.css">
      </head>
    <body>
      <div class="container">
            <article class="content">
                {{ content }}
            <section class="comment">
            {% include comments.html %}
            </section>
        </article>
      </div>
    </body>
    </html>
