---
title: 活动案例
date: 2022-01-06 21:52:55
---

 <iframe  
 id="lists" 
 width=100%
 src="lists.html"  
 frameborder=0  
 >
 </iframe>

<script>
    var ifr = document.querySelector('iframe');
    ifr.onload = function () {
      fixIframeHeight()
    }
    function fixIframeHeight(){
      var oHeight = Math.max(ifr.contentWindow.document.documentElement.offsetHeight, ifr.contentWindow.document.body.offsetHeight);
      var cHeight = Math.max(ifr.contentWindow.document.documentElement.clientHeight, ifr.contentWindow.document.body.clientHeight);
      var height = Math.max(oHeight, cHeight);
      ifr.style.height = height + 'px'
    }
    window.onresize = fixIframeHeight
</script>