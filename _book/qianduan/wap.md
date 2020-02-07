#注：这里需要说明的是，第三方代码的引入对手机端的评分还是有一定的影响的，尤其是facebook,salesiq 影响较明显
---
#一、目前存在的问题及处理（author:徐彦广）
###1、由于使用zepto库替换jquery,这里会使用tab 事件替换 click事件
###2、处理有遮罩层下方依然滚动问题
        添加以下两个全局方法
```
var t = 0;
window.unScroll = function() {
        t = $('header').offset().top;
        if ($('#xker')[0]) {
            t = t - $('#xker').height();
            if (t < 0) {
                t = 0
            }
        }
        $(document.body).addClass(function() {
            $(this).css('top', -t + 'px');
            return 'unScroll';
        });
        window.scrollToT = function() {
            $(document.body).removeClass('unScroll').css('top', '');
            window.scrollTo(0, t);
        }
    }
```
###3、header 结构问题
    Header部分需注意四个部分组成，分别是nav 、navbar、navbar左侧滑出后的半透明背景、搜索框.，nav中的五个图标需要注意电话图标的不同屏幕适配问题。Navbar和他的背景需要是兄弟关系这样比较利于用js控制。
###4、回到顶部问题
    因为ios对scroll事件的处理不同于安卓浏览器，这个动画效果需要借助原生js来完成，window.requestAnimationFrame方法和window.cancelAnimationFrame方法。
###5、产品列表js处理
    产品目录页面的产品下拉刷新的工程需要借助原生js中的
    IntersectionObserver 对象来完成。该页面的需要注意动态添加
    的内容较多，绑定时间需要委托给父级元素、document或body
###6、产品详情
    1)产品详情页tab选项卡这一块的滚动动画依旧需要使用回到顶部所用的原生js方法。
    2)产品详情页新增上传图片增加缩略图的功能，需要用到原生js中的FileReader对象
```
function readAndPreview(file) {
            // Make sure `file.name` matches our extensions criteria
            if (/\.(jpe?g|png|gif)$/i.test(file.name)) {
                var reader = new FileReader();
                reader.addEventListener("load", function() {
                    var image = new Image();
                    image.title = file.name;
                    image.src = this.result;
                    preview.appendChild(image);
                }, false);
                reader.readAsDataURL(file);
            }
        }
```
#二、通用弹框
    弹窗部分与PC虽异曲同工但有所出入，样式上弹窗宽度统一为96%，并且优化了视觉效果，ui变化较大。Js上需换掉click事件为tap事件，并且为更适合移动端弹窗做了一些调整和改动
#三、用到的第三方库
         Zepto：用于移动端代替jquery的一款更适合移动端需求的框架，较与jquery性能更佳，体积更小，而且兼容性良好，虽不及jquery面面俱到，但也足以满足移动端开发的需求。
    	validator：轻量级的验证插件，原生js编写，兼容性良好，为满足开发需求更改过此中内容用于阻止表单提交。缺点是，编写验证的过程繁琐，功能不够完善。
    	baguetteBox：与pc一致
    	lozad：与pc一致
    	swiper：与pc一致
#四、第三方代码
    与 pc一致
#五、输入框通用结构说明（author:石爱朵）
###1、输入框通用结构
```
 <div class="form-list">
       <div class="form-list_item form-list_item--all">
           <label class="form-label form-label--validator" for="email">Email Address</label>
           <input class="form-input" type="text" name="email" id="email">
       </div>
  </div>
  <!--
form-label: 表单标题class;
form-label--validator: 必填项特殊标记添加class;
form-list_item--all: input 框宽度为整屏幕时添加class
form-list_item--sub : input 框宽度为屏幕一半的宽度时添加class
    -->
```
###2、输入框右侧有apply 按钮结构的
```
<div class="form-list">
    <div class="form-list_item form-list_item--all position-relative">
        <input class="form-input" type="text" name="reward-points" id="reward-points">
        <button class="button checkout-reward_btn">Apply</button>
</div>
</div>
```
<font color='red'>注释：需要在之前输入框结构的基础上 form-list_item class上增加class: position-relative,并在该标签中添加button;</font>

###3、多选框通用结构

```
<div class="form-control">
  <input class="form-control_input form-control_input--checkout" name="checkout-save" type="checkbox" id="checkout-save-address">
 <label class="form-control_label" for="checkout-save-address">Save in address book</label>  </div>
```

###4、单选框通用结构

```
<div class="form-control">
    <input class="form-control_input form-control_input--radio" name="method" type="radio" id="checkout-mathod1">
<label class="form-control_label" for="checkout-mathod1">FREE SHIPPING <span class="form-control_label_price">$0.00</span>  (3-5 working days) </label>
 </div>
```

<font color='red'>注释：多选框需要在type为checkbox的input标签上添加form-control_input 、form-control_input--checkout两个class 单选框要在type为radio的input标签上添加form-control_input、form-control_input--radio两个class
</font>