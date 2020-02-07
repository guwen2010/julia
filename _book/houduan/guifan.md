#一、网站整体架构
<img src='../images/jiagou.png'>

     此次依然延续现在的mcbv 架构；对b，v端进行深度的优化调整
     全面移除无用xml，v层全部重构
---
#二、注释规则
###block,controllers,model,helper
     1、新建类必须注释，格式为
     /**
      * @author 作者
      * @date 时间
      * @description 类描述
      */
      
     2、创建的常量必须注释
     
     3、方法必须注释，格式为
     	/**
     	 * @author 作者
     	 * @date 时间
     	 * @description  描述
     	 * @param $cart 变量描述
     	 * @return 返回值类型
     	 */
###xml 
     所有新引入的xml必须注释，格式为
     <!--引入说明-->
###phtml
    在页面添加的block块，引入getChildHtml,调用block里面的方
    法。。均必须写清楚注释，格式为
     <?php
      /**
       * 描述
       */
      ?>
#三、大的功能模块
     功能性开发需必须有文档说明
       1、流程图，
       2、数据字典，
       3、核心代码及说明
#四、缓存标签
         首页---home 
         列表---product_list
         详情---product_view
         购物车--checkout
         支付页面---firecheckout
         用户中心---customer
         其他通用--common
         栏目促销折扣--catalog_promotion
         评论缓存----customerreview  