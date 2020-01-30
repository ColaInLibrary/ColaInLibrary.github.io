---
title: 最热阅读
date: 2019-10-27 22:38:19
comments: false
---

<div id="top"></div>

<script src="//cdn1.lncld.net/static/js/3.0.4/av-min.js"></script>
<script>AV.initialize("owryKYMxVRpqksq7EoJmoJHy-gzGzoHsz", "W7BaIi1FbwpgIDuNXyGAfUsl");</script>
<script type="text/javascript">
    var time=0
    var title=""
    var url=""
    var query = new AV.Query('Counter');
    query.notEqualTo('id',0);
    query.descending('time');
    query.limit(1000);
    query.find().then(function (todo) {
        for (var i=0;i<1000;i++){
            var result=todo[i].attributes;
            time=result.time;
            title=result.title;
            url=result.url;
            var content="<a href='"+"https://colainlibrary.github.io"+url+"'>"+title+"</a>"+"<br />"+"<font color='#555'>"+"热度："+time+"°C"+"</font>"+"<br /><br />";
            document.getElementById("top").innerHTML+=content
        }
    }, function (error) {
        console.log("error");
    });
</script>

<style>.post-description { display: none; }</style>