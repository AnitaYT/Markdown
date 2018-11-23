### 1.移动端字体适配/使用rem/手机端动态设置font-size
```
$(function (){
    // 字体比例 屏幕宽度 根字体大小
    var fontRatio = 18.75, windowWidth, rootFontSize;
    function modifyRootFontSize()
    {
        windowWidth = document.documentElement.clientWidth;
        rootFontSize = windowWidth / 18.75;
        document.getElementsByTagName('html')[0].style.cssText = 'font-size:' + rootFontSize + 'px';
    }
    modifyRootFontSize();
    // 当窗口大小发生改变时
    window.onresize = function () {
        modifyRootFontSize();
    }
})();
```
### 2.获取地址栏参数
```
window.location.search:?wd=移动端%20rem适配&rsv_spt=1&rsv_iqid=0xb5e021da0000b83f&issp=1&f=8&rsv_bp=0&rsv_idx=2&ie=utf-8&tn=baiduhome_pg
// 1 getRequest().name
function getRequest() {
    var url = window.location.search;   //获取url中"?"符后的字串
    var theRequest = new Object();
    if (url.indexOf("?") != -1) {  // 判断地址栏是否有传递参数
        var str = url.substr(1);  // 截取？号后的字符串
        strs = str.split("&");   // &号切割后的数组类似为['name=ann','age=18','gender=girl']
        for (var i = 0; i < strs.length; i++) {   //地址栏参数有时候会进行加密，decodeURI解密
            theRequest[strs[i].split("=")[0]] = decodeURI(strs[i].split("=")[1]);
        }
    }
    return theRequest;
}
// 2 getUrlParam('name')
function getUrlParam (name) { // 获取地址参数
    var url = window.location.search;
    var reg = new RegExp("(^|&)"+ name +"=([^&]*)(&|$)");  // 匹配的表达式为：/(^|&)参数=([^&]*)(&|$)/ 例如：/(^|&)name=([^&]*)(&|$)/
    var result = url.substr(1).match(reg); // 匹配?号后的字符串
    console.log(result)
    return result ? decodeURIComponent(result[2]) : null;
}

```
### 3.前端加密、解密
```
加密：window.btoa(xxx);
解密：window.atob(xxx);
//加密
function utoa(str) {
    return window.btoa(unescape(encodeURIComponent(str)));
}
// 解密
function atou(str) {
    return decodeURIComponent(escape(window.atob(str)));
}

var a = utoa('谢玉婷');
var b = atou(a);
console.log(a,b)

```
### 4.js计算精度问题
```
function add(a, b) {
    var c, d, e;
    try {
        c = a.toString().split(".")[1].length;
    } catch (f) {
        c = 0;
    }
    try {
        d = b.toString().split(".")[1].length;
    } catch (f) {
        d = 0;
    }
    return e = Math.pow(10, Math.max(c, d)), (mul(a, e) + mul(b, e)) / e;
}
function sub(a, b) {
    var c, d, e;
    try {
        c = a.toString().split(".")[1].length;
    } catch (f) {
        c = 0;
    }
    try {
        d = b.toString().split(".")[1].length;
    } catch (f) {
        d = 0;
    }
    return e = Math.pow(10, Math.max(c, d)), (mul(a, e) - mul(b, e)) / e;
}
function mul(a, b) {
    var c = 0,
        d = a.toString(),
        e = b.toString();
    try {
        c += d.split(".")[1].length;
    } catch (f) { }
    try {
        c += e.split(".")[1].length;
    } catch (f) { }
    return Number(d.replace(".", "")) * Number(e.replace(".", "")) / Math.pow(10, c);
}
function div(a, b) {
    var c, d, e = 0,
        f = 0;
    try {
        e = a.toString().split(".")[1].length;
    } catch (g) { }
    try {
        f = b.toString().split(".")[1].length;
    } catch (g) { }
    return c = Number(a.toString().replace(".", "")), d = Number(b.toString().replace(".", "")), mul(c / d, Math.pow(10, f - e));
}
        
console.log('正常计算:','10000 * 0.0006 = ',10000*0.0006,'出现精度问题')
mul(10000,0.0006);
console.log('使用mul方法解决bug:',mul(10000,0.0006))
```
### 5.localStore本地存储
```
let data = {
  code: 0,
  data: [1, 3, 5]
}
localStorage.setItem('datas', JSON.stringify(data))
console.log(JSON.stringify(data))

let data = localStorage.getItem('datas')
console.log(JSON.parse(data))

```
### 6.判断时间是否在时间段内
```
     var time_range = function (beginTime, endTime, nowTime) {
     var strb = beginTime.split (":");
     if (strb.length != 2) {
         return false;
     }
 
     var stre = endTime.split (":");
     if (stre.length != 2) {
         return false;
     }
 
     var strn = nowTime.split (":");
     if (stre.length != 2) {
         return false;
     }
     var b = new Date ();
     var e = new Date ();
     var n = new Date ();
 
     b.setHours (strb[0]);
     b.setMinutes (strb[1]);
     e.setHours (stre[0]);
     e.setMinutes (stre[1]);
     n.setHours (strn[0]);
     n.setMinutes (strn[1]);
 
     if (n.getTime () - b.getTime () > 0 && n.getTime () - e.getTime () < 0) {
         return true;
     } else {
         alert ("当前时间是：" + n.getHours () + ":" + n.getMinutes () + "，不在该时间范围内！");
         return false;
     }
 }
 time_range ("21:30", "23:30", "22:22");
```

### 7.