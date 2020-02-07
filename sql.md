#数据库调整
```
1、移除评论插件相关字段
delete from eav_attribute where backend_model='detailedreview/category_attribute_backend_fields';
2、配合移除俄语站点
DELETE FROM `core_store` WHERE `core_store`.`store_id` = 5;
DELETE FROM `core_store_group` WHERE `core_store_group`.`group_id` = 2;  #重建索引
DELETE from cms_page_store where store_id=5;

3、后端栏目报错：
DELETE from eav_attribute where attribute_code = "bs_menuadvanced";
DELETE from eav_attribute where attribute_code = "cb_category_type";
4、后端报错（系统升级导致）
alter table sales_bestsellers_aggregated_yearly add COLUMN product_type_id varchar(255) default 'simple';
alter table sales_bestsellers_aggregated_monthly add COLUMN product_type_id varchar(255) default 'simple';
alter table sales_bestsellers_aggregated_daily add COLUMN product_type_id varchar(255) default 'simple';
5、移除无用表
DROP TABLE `permission_variable`;   #不一定执行
DROP TABLE `permission_block`;		#不一定执行
drop table `customer_flowpassword`;
drop table `ordersyncquerunner_que`;
drop table  `vstudio_venu_menuitem`;
drop table  `vstudio_venu_menu`;
7、评论相关
DROP TABLE `review_author_ips`;
DROP TABLE `review_helpful`;
DROP TABLE `review_proscons`;
DROP TABLE `review_proscons_store`;
ALTER TABLE `review_detail` DROP `cons`;
ALTER TABLE `review_detail` DROP `pros`;
ALTER TABLE `review_detail` DROP `body_type`;
ALTER TABLE `review_detail` DROP `sizing`;
ALTER TABLE `review_detail` DROP `location`;
ALTER TABLE `review_detail` DROP `age`;
ALTER TABLE `review_detail` DROP `height`;

8、订单表操作
alter table sales_flat_order drop column tm_field1,drop column tm_field2, drop column tm_field3, drop column tm_field4,drop column tm_field5,drop column fake_id;
drop table tm_orderattachment;

10、flat 表移除重新生成
drop table `catalog_category_flat_store_1`;
drop table `catalog_category_flat_store_2`;
drop table `catalog_category_flat_store_3`;
drop table `catalog_category_flat_store_4`;
drop table `catalog_category_flat_store_5`;
drop table `catalog_category_flat_store_6`;
drop table `catalog_product_flat_1`;
drop table `catalog_product_flat_2`;
drop table `catalog_product_flat_3`;
drop table `catalog_product_flat_4`;
drop table `catalog_product_flat_5`;
drop table `catalog_product_flat_6`;

11、关闭rss
UPDATE `core_config_data` SET `value` = '0' WHERE `core_config_data`.`path` = 'rss/catalog/category';
UPDATE `core_config_data` SET `value` = '0' WHERE `core_config_data`.`path` = 'rss/config/active';
UPDATE `core_config_data` SET `value` = '0' WHERE `core_config_data`.`path` = 'rss/wishlist/active';
UPDATE `core_config_data` SET `value` = '0' WHERE `core_config_data`.`path` = 'rss/catalog/special';
UPDATE `core_config_data` SET `value` = '0' WHERE `core_config_data`.`path` = 'rss/catalog/salesrule';
UPDATE `core_config_data` SET `value` = '0' WHERE `core_config_data`.`path` = 'rss/catalog/tag';
UPDATE `core_config_data` SET `value` = '0' WHERE `core_config_data`.`path` = 'clnews/rss/enable';
UPDATE `core_config_data` SET `value` = '0' WHERE `core_config_data`.`path` = 'rss/catalog/new';
```