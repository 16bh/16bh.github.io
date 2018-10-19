---
title: hexo支持多说评论
date: 2016-07-05 20:12:33
categories: [Blog]
tags: hexo
---
2018-10-16：多说已经倒闭很多年了

---



只需要三步即可让你的`hexo`主题支持评论

1. 去[多说](http://duoshuo.com)登录，设置`short name`
2. 将上面的`short name `加入配置`themes/landscape/_config.yml`中

``` yml
duoshuo_shortname: 你站点的short_name
```

3. 修改`themes\landscape\layout\_partial\article.ejs`
删除下面的`disqus`评论的代码：

``` js
<% if (!index && post.comments && config.disqus_shortname){ %>
  <section id="comments">
    <div id="disqus_thread">
      <noscript>Please enable JavaScript to view the <a href="//disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
    </div>
  </section>
  <% } %>
```

加入多说评论的代码

``` js
<% if (!index && post.comments && config.duoshuo_shortname){ %>
  <section id="comments">
    <!-- 多说评论框 start -->
    <div class="ds-thread" data-thread-key="<%= post.layout %>-<%= post.slug %>" data-title="<%= post.title %>" data-url="<%= page.permalink %>"></div>
    <!-- 多说评论框 end -->
    <!-- 多说公共JS代码 start (一个网页只需插入一次) -->
    <script type="text/javascript">
    var duoshuoQuery = {short_name:'<%= config.duoshuo_shortname %>'};
      (function() {
        var ds = document.createElement('script');
        ds.type = 'text/javascript';ds.async = true;
        ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
        ds.charset = 'UTF-8';
        (document.getElementsByTagName('head')[0]
         || document.getElementsByTagName('body')[0]).appendChild(ds);
      })();
      </script>
    <!-- 多说公共JS代码 end -->
  </section>
  <% } %>
```
