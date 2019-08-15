# Gold-drop-animation
#### 写一个H5签到金币掉落动画



![效果gif](https://upload-images.jianshu.io/upload_images/3888312-c1346bd3942f5963.gif?imageMogr2/auto-orient/strip)



最近项目上写了一个签到页面,其中有一个功能设计的是点击签到，有一个金币坠落的效果，现在总结记录一下：


#### 需求
1. 中间已签到的金色圆球需要倾斜掉落，然轻微反弹后竖直显示。
2. 四周的小金币不能同时掉落在屏幕上，需要有先后次序。
3. 当小金币和金色圆球完全出现在屏幕后需等待500毫秒。
4. 金色圆球逐渐放大并变淡。
5. 小金币此时竖直下落，速度逐渐加快。


#### 实现步骤
如果要实现此效果，至少需要两组动画衔接在一起。
第一组动画是金币掉落，金色圆球倾斜反弹出现在页面上；第二组是金色圆球逐渐放大并变淡金币，金币加速掉落。

#### 具体代码

第1步：HTML布局
```
<div class="signin" id="signin">
	<div class="coin animated ">
		<img id="bg" class="bg animated " src="../../images/v3/coin.png">
		<img class="texts animated " src="../../images/v3/hasdone@2x.png">
	</div>
</div>
```
第2步：CSS布局代码
确定小金币和金色大圆球掉落的最终位置
```
.signin{display:none;position:absolute;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.7);z-index:9999;overflow:hidden}
.coin{width:4.12rem;height:4.12rem;font-size:30px;margin-left:calc((100% - 4.12rem) / 2);margin-top:calc((9.22rem / 2) - 1.5rem);position:relative}
.coin .bg{float:left;width:4.12rem;height:4.12rem}
.coin .texts{position:absolute;top:1.7rem;left:1.11rem;width:1.9rem;height:.72rem}
.coin1{width:.68rem;height:.5rem;position:absolute;top:.3rem;right:0;animation-delay:0.3s}
.coin2{width:.33rem;height:.43rem;position:absolute;top:.5rem;left:3.7rem;animation-delay:0.25s}
.coin3{width:.67rem;height:.8rem;position:absolute;top:3.3rem;left:.9rem;animation-delay:0.2s}
.coin4{width:.75rem;height:.55rem;position:absolute;top:3.7rem;right:1.3rem;animation-delay:0.15s}
.coin5{width:.83rem;height:.59rem;position:absolute;top:6.8rem;right:1.1rem;animation-delay:0.1s}
.coin6{width:.8rem;height:.74rem;position:absolute;top:8rem;right:.3rem;animation-delay:0.05s}
.coin7{width:2.12rem;height:1.9rem;position:absolute;top:8.7rem;left:1.2rem;animation-delay:0.05s}

```
#### 第3步：CSS动画代码
金色大圆球从高处下落
```
.animated {
	-webkit-animation-duration: 1s;
	animation-duration: 1s;
	-webkit-animation-fill-mode: both;
	animation-fill-mode: both;
	-webkit-animation-iteration-count: 1;
	animation-iteration-count: 1;
}

@keyframes bounceInDown {
	from,
	60%,
	75%,
	90%,
	to {
		-webkit-animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
		animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
	}
	0% {
		-webkit-transform: translate3d(0, -3000px, 0);
		transform: translate3d(0, -3000px, 0);
	}
	60% {
		-webkit-transform: translate3d(0, 25px, 0);
		transform: translate3d(0, 25px, 0);
	}
	75% {
		-webkit-transform: translate3d(0, -10px, 0);
		transform: translate3d(0, -10px, 0);
	}
	90% {
		-webkit-transform: translate3d(0, 5px, 0);
		transform: translate3d(0, 5px, 0);
	}
	to {
		-webkit-transform: translate3d(0, 0, 0);
		transform: translate3d(0, 0, 0);
	}
}

.bounceInDown {
	-webkit-animation-name: bounceInDown;
	animation-name: bounceInDown;
	-webkit-animation-duration: 0.8s;
	animation-duration: 0.8s;
}

```
金色大圆球旋转30度
```
@keyframes rotateInDownRight {
	from {
		opacity: 0;
		transform: rotate(60deg);
	}
	60% {
		opacity: 1;
		transform: rotate(60deg);
	}
	to {
		transform: rotate(0);
	}
}

.rotateInDownRight {
	-webkit-animation-name: rotateInDownRight;
	animation-name: rotateInDownRight;
	-webkit-animation-duration: 0.8s;
	animation-duration: 0.8s;
}

```
已签到文本动画
```
@keyframes rotateInDownRighttext {
	from {
		opacity: 0;
		transform: rotate(60deg) scale(1.2);
	}
	75% {
		opacity: 1;
		transform: rotate(60deg) scale(1);
	}
	to {
		transform: rotate(0) scale(1);
	}
}

.rotateInDownRighttext {
	-webkit-animation-name: rotateInDownRighttext;
	animation-name: rotateInDownRighttext;
	-webkit-animation-duration: 0.8s;
	animation-duration: 0.8s;
}

```
放大然后消失
```
@keyframes bigVanish {
	from {
		opacity: 1;
		transform: scale(1);
	}
	to {
		opacity: 0;
		transform: scale(3);
	}
}

.bigVanish {
	-webkit-animation-name: bigVanish;
	animation-name: bigVanish;
	-webkit-animation-duration: 0.4s;
	animation-duration: 0.4s;
	animation-delay: 1s;
}


```
6枚金币掉落
```
@keyframes coinDown {
	from {
		-webkit-transform: translate3d(0, -3000px, 0);
		transform: translate3d(0, -3000px, 0);
	}
	to {
		-webkit-transform: translate3d(0, 0, 0);
		transform: translate3d(0, 0, 0);
	}
}
@keyframes goDown {
	from {
		-webkit-transform: translate3d(0, 0, 0);
		transform: translate3d(0, 0, 0);
	}
	to {
		-webkit-transform: translate3d(0, 1000px, 0);
		transform: translate3d(0, 1000px, 0);
	}
}
.signin>img{
	-webkit-animation-name: coinDown;
	animation-name: coinDown;
	-webkit-animation-duration: 0.8s;
	animation-duration: 0.8s;
	-webkit-animation-timing-function: ease-out;
	animation-timing-function: ease-out;
}
.signin>img.goDown{
	-webkit-animation-name: goDown;
	animation-name: goDown;
	-webkit-animation-duration: 1s;
	animation-duration: 1s;
	animation-delay: 1s;
}

```

#### 第4步：Javascript
增加clss、判断是否拥有claa
```
function hasClass(elem, cls) {
	cls = cls || '';
	if(cls.replace(/\s/g, '').length == 0) return false; //当cls没有参数时，返回false
	return new RegExp(' ' + cls + ' ').test(' ' + elem.className + ' ');
}

function addClass(elem, cls) {
	if(!hasClass(elem, cls)) {
		elem.className = elem.className == '' ? cls : elem.className + ' ' + cls;
	}
}
```
获取基本信息
```
var container = document.getElementById('signin');
var btn = document.getElementById('btn');
var coinBg = document.getElementsByClassName("bg")[0];
var texts = document.getElementsByClassName("texts")[0];
var coinImgs = document.getElementsByClassName("coins");
var coin = document.getElementsByClassName("coin")[0];

/*定义小金币基本信息 */
var coinPosition = [
	[0.3, 0],
	[0.5, 3.5],
	[3.3, 6],
	[3.7, 1.3],
	[6.8, 1.1],
	[8, 0.3],
	[8.7, 4.2]
];
var coinSize = [
	[0.68, 0.5],
	[0.33, 0.43],
	[0.67, 0.8],
	[0.75, 0.55],
	[0.83, 0.59],
	[0.8, 0.74],
	[2.12, 1.9]
];
```
动画事件触发的监听
```
btn.addEventListener('click', function() {
	addClass(coin, "bounceInDown")
	addClass(coinBg, "rotateInDownRight")
	addClass(texts, "rotateInDownRighttext")
	container.style.display="block"
	init()

}, false);
```
开始金币动画掉落
```
function init() {
	try {
		for(var i = 0; i < 7; i++) {
			container.appendChild(createALeaf(i));
		}
		second();
	} catch(e) {
		console.log("error")
	}

}

function createALeaf(i) {
	var image = document.createElement('img');
	image.src = '../../images/v3/coin' + (i + 1) + '.png';
	image.className = 'coins animated';
	image.style.width = coinSize[i][0] + "rem";
	image.style.height = coinSize[i][1] + "rem";
	image.style.top = coinPosition[i][0] + "rem";
	image.style.right = coinPosition[i][1] + "rem";
	image.style.webkitAnimationName = "coinDown";
	image.style.animationName = "coinDown";
	// 随机delay时间
	var leafDelay = 0.05 * (7 - i);
	image.style.webkitAnimationDelay = leafDelay + "s";
	image.style.animationDelay = leafDelay + "s";
	return image;
}
```
设置监听，当第一组动画执行完毕后执行下面的代码
```
//第二部分金币掉落和已签到放大
function second() {
	//最后一枚金币出现在屏幕的动画结束时触发
	coinImgs[0].addEventListener("webkitAnimationEnd", function(e) {
		//console.log("动画执行完毕");
		if(hasClass(coinImgs[0], "goDown")) {
			console.log("下一步");
		}
		addClass(texts, "bigVanish")
		addClass(coinBg, "bigVanish")
		Array.from(coinImgs).forEach((item, index) => {
			coinImgs[index].style.animationName = '';
			coinImgs[index].style.animationDelay = '';
			addClass(coinImgs[index], "goDown")
		});
	}, false);
}
```

