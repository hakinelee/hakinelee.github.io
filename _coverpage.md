<!-- ![logo](_media/logo.png) -->

<!-- <h1 style="font-size: 3rem;
    font-weight:bold;
    margin: 0px;
    padding: 0px;">hakine的博客</h1> -->

<!-- <h2 style="font-size: 3rem;">HAKINE'S BLOG</h2> -->
<div id=Title2 style="color: gray; font: bold 50px arial; position: absolute; visibility:hidden; top:200px; left:300px;">
    <p>HAKINE'S BLOG</p>
</div>
<div id=Title1 style="color: white; font: bold 50px arial; position: absolute; visibility:hidden; top:200px; left:300px">
    <p>HAKINE'S BLOG</p>
</div>
<script>
var Tle2="document.all.Title2.style";
var Tle1="document.all.Title1.style";
eval(Tle2).top=eval(Tle1).top=document.body.clientHeight/2 - 20;
eval(Tle2).left=eval(Tle1).left=document.body.clientWidth/2 - 150;
function Fade(){   
	var BackX = Math.random()*10;
	var BackY = Math.random()*5;   
	if(Math.random()<0.5){   
		BackX = -BackX;   
		BackY = -BackY;   
	}   
	eval(Tle1).visibility = eval(Tle2).visibility = "visible";   
	eval(Tle2).left = parseInt(eval(Tle1).left) + BackX;   
	eval(Tle2).top = parseInt(eval(Tle1).top)  + BackY;   
	var FadeID = setTimeout("Fade()",50);   
}
Fade();
</script>

## 记录一些自己的心得与感触

[![stars](https://badgen.net/github/stars/hakinelee/hakinelee.github.io?icon=github&color=4ab8a1)](https://github.com/hakinelee/hakinelee.github.io) [![forks](https://badgen.net/github/forks/hakinelee/hakinelee.github.io?icon=github&color=4ab8a1)](https://github.com/hakinelee/hakinelee.github.io)

<span id="busuanzi_container_site_pv" style='display:none'>
    👀 本站总访问量：<span id="busuanzi_value_site_pv"></span> 次
</span>
<span id="busuanzi_container_site_uv" style='display:none'>
    | 🚴‍♂️ 本站总访客数：<span id="busuanzi_value_site_uv"></span> 人
</span>

[GitHub](<https://github.com/hakinelee/hakinelee.github.io>)
[开始阅读](README.md)
