---
layout: post
title:  "github.io add disqus!"
date:   2016-01-13 5:44
categories: jekyll update
---

<h2>1.</h2> <h3><a href="https://disqus.com/">Disqus</a> 들어가서 signup 해준다.</h3>
![disqus1](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus1.png)
<h2>2.</h2> <h3>오른쪽 Add Disqus To Stie Click</h3>
![disqus2](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus2.png)
<h2>3.</h2> <h3>Start Using Engage</h3>
![disqus3](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus3.png)
<h2>4.</h2> <h3>다 적은후 Finish registration.</h3>
![disqus4](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus4.png)
<h2>5.</h2> <h3>Universal Code 클릭</h3>
![disqus5](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus5.png)
<h2>6.</h2> <h3>아래 소스코드 copy</h3>
![disqus6](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus6.png)

<h2>7.</h2> <h3>자신의 includes 폴더안에 comments.html 생성 해주고 아까 copy 한 내용을 복사해준다.</h3>

<h2>8.</h2> <h3>comments.html 을 post.html 안에 추가해준다.</h3>

```
<!--<html lang="en">
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
</html>-->
```