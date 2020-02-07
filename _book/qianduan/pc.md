#一、目前存在的问题及处理（author:徐彦广）：
###1、flex布局兼容问题
```
display: -webkit-box; /* Chrome 4+, Safari 3.1, iOS Safari 3.2+ */  
display: -moz-box; /* Firefox 17- */  
display: -webkit-flex; /* Chrome 21+, Safari 6.1+, iOS Safari 7+, Opera 15/16 */  
display: -moz-flex; /* Firefox 18+ */  
display: -ms-flexbox; /* IE 10 */  
display: flex; /* Chrome 29+, Firefox 22+, IE 11+, Opera 12.1/17/18, Android 4.4+ */
```
    但是这样也只能兼容到ie10，想要兼容ie9还要自己写适合自己网站polyillcss，这样的兼容缺点会导致用于调试更改的过程增加，可以考虑在下个网站PC端重做时使用兼容性更好的浮动布局。
###2、横向滚动问题
    屏幕适配时注意要对绝对定位的元素进行响应式处理，避免发生出现横向滚动条的问题。
###3、头部导航问题
    header导航栏部分为了节约元素数量，把一级导航和其对应的
    二级导航放在了一起，需要注意是用每个一级导航的位置和其二级
    导航的位置把两者关联起来的，动画收缩的背景是写在包含导航盒
    子的外面的。
###4、首屏图片懒加载问题
     注意首屏显示的图片是不需要懒加载的
     导航上图片，banner的首个图片，产品第一个主图...
###5、ajax动态加载js书写注意问题
        1)	ajax.动态添加的产品列表 需要重新启动懒加载。
        2)	动态添加会导致绑定事件失效，需把把事件委托给document或者body或者未被动态刷新的父元素
        3)	动态添加的表单需要重启动校验
###6、swiper 使用问题
    每个轮播都需要new不同的swiper对象进行配置和区分。
###7、cookie作用域问题
    在js命名cookie的时候要指定作用域
###8、产品详情页主图滚动问题
    左侧产品图片详情随进度条滑动效果，使用的是display：fixed，
    这样更加流畅，需要注意的是需要判断头部是否有advert推广，
    调整在不同的高度触发
###9、评论上传图片大小限制问题
     上传评论图片功能 限制图片大小的时候，需要注意ie和
     firebox的在查看文件大小时有区别.
```
//获取文件大小
if (Sys.firefox) {
    filesize = input.files[0].size;
} else if (Sys.ie) {
    var fileobject = new ActiveXObject("Scripting.FileSystemObject"); //获取上传文件的对象
    var file = fileobject.GetFile(input.value); //获取上传的文件
  filesize = file.Size; //文件大小
}
```
###10、产品价格前端计算逻辑
    计算产品价格，利用calPrice函数计算选中选项的价格，
    用updatePrice函数分别计算旧价格与新价格以及折扣掉的价格，
    用roundTwo函数保留两位小数，并输出到对应的盒子中。
#二、通用弹框方法
```
1、openLoading();   加载框
2、closePopup('loading'); 关闭
3、openMessage (msgObject, oneBtn, callBack); 确认框 
    /**
    1.msgObject可以为字符串，也可以写成{
            string:'',//段落
            title:'',//标题
            }
    2.oneBtn为'yes',只添加yes按钮 为'no'只添加no按钮,为window.将为yes按钮添加回调函数
    3.callBack 只有在当在oneBtn 为function是 回味 no按钮 添加回调函数，其他都为yes添加回调函数
    */
4、openTips (string, isFail, delay);
    /**
    1.string，提示框内容
    2.是否为报错内容
    3．停留时间默认为3000ms
    **/
5、openPopup (ElementID) ; //ElementID为需要打开或者关闭的弹窗的id
6、closePopup (ElementID)
```
#三、具体js,css引入的位置及说明会在webpack.config.js 进行
#四、第三方库说明
    Jquery：用于方便实现复杂的js功能
    elevatezoom （jquery）：用于实现详情页产品图片细节预览效果，
    form-validator （jquery）：基于jquery的校验插件，需要手动更改部分代码以达到阻止sumit自动提交用ajax传递表单的功能。
    velocity （jquery）： 用于链式有顺序的执行animate动画，方便写出复杂的动画效果 ，主要用于slaylooks的动画效果。
    baguetteBox：原生js灯箱插件，兼容性良好体积小，主要用于详情页预览评论图片
    idangerous.swiper：2.7.6 版本的swiper，可兼容到ie9，用于网站整个轮播功能，缺点是配置过程较与高版本的swipe更繁琐。
    lozad：依赖于原生js中intersection-observer功能的懒加载插件。性能高，体积小
    intersection-observer：用于lozad兼容ie9的polyfill。
#五、第三方工具的引入：
        1、refersion 联盟
        2、bizrate 第三方评论
        3、结构化数据
        4、bing
        5、facebook
        6、google评论
        7、onesignal
        8、salesiq