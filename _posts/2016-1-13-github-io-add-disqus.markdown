---
layout: post
title:  "github.io add disqus!"
date:   2016-01-13 5:44
categories: jekyll update
---

1.<a href="https://disqus.com/">Disqus</a> 들어가서 signup 해준다.
![disqus1](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus1.png)
2.오른쪽 Add Disqus To Stie Click
![disqus2](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus2.png)
3.Start Using Engage
![disqus3](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus3.png)
4.다 적은후 Finish registration.
![disqus4](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus4.png)
5.Universal Code 클릭
![disqus5](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus5.png)
6.아래 소스코드 copy
![disqus6](https://raw.githubusercontent.com/ekeon/ekeon.github.io/master/image/disqus6.png)

7.자신의 includes 폴더안에 comments.html 생성 해주고 아까 copy 한 내용을 복사해준다 
  '{% include comments.html %}' 를 post.html 은 사람마다 다를수있으나 보통은 content 아래에 추가해준다.

{% highlight java %}
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
            <!--{{ content }}-->
        <section class="comment">
        <!--{% include comments.html %} 마크다운 형식이라 html 파일을 불러와 주석처리해두었슴.-->
        </section>
    </article>
  </div>
</body>
</html>
{% endhighlight %}