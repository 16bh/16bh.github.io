---
title: hexo的landscape-plus主题安装不蒜子访问量统计插件
date: 2016-07-06 12:04:15
category:
tags: website
---

修改`themes/landscape-plus/layout/_partial/footer.ejs`如下：


``` js
<footer id="footer">
  <% if (theme.sidebar === 'bottom'){ %>
    <%- partial('_partial/sidebar') %>
  <% } %>
  <div class="outer">
    <div id="footer-info" class="inner">
      &copy; <%= date(new Date(), 'YYYY') %> <%= config.author || config.title %><br>
      Powered by <a href="http://hexo.io/" target="_blank">Hexo</a>
      .
      Theme by <a href="https://github.com/xiangming/landscape-plus" target="_blank">Landscape-plus</a>
      <!-- 不蒜统计 -->
      <br>
      <span style="display: inline;" id="busuanzi_container_site_uv">本站总访客数 <span id="busuanzi_value_site_uv" font="微软雅黑" style="color:white"></span> 次</span>
      <span style="display: inline;" id="busuanzi_container_site_pv">本站总访问量 <span id="busuanzi_value_site_pv" font="微软雅黑" style="color:white"></span> 次</span>
    </div>
  </div>
</footer>
<script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```
