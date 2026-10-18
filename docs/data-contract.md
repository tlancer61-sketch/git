# 数据约定 v0.1

## 主键与粒度

JSON 使用 UTF-8；schema_version 当前为 "0.1"。一条 vehicle 记录对应“中国市场 + 品牌 + 车系 + 年款 + 能源 + 具体配置”。文件名与 vehicle_id 一致，使用小写英文数字和连字符，ID 发布后不改。换年款或配置新增记录；更正同版本用 Git 保留历史。

## 车型字段

- is_example：虚构示例必须 true；真实记录 false。
- market、brand、series、model_year、powertrain、trim：身份字段，不明确填 null，禁止猜测。
- lifecycle：unknown / announced / on_sale / delivering / discontinued。
- facts：以稳定 fact_id 列表保存每项价格、配置或实测结果。
- 每项 fact：kind（public_fact / manufacturer_promise / media_test / owner_account / field_account / inference）、value、unit、conditions、source_ids、official_confirmation、verification、checked_at、valid_until。
- value=null 表示未知，不能用 0 或空字符串代替未知；不适用时 value=null 并在 conditions.reason 解释。
- conditions 按事实需要填 city、price_type（guide / quote / transaction / on_road）、payment、subsidy、software_version、test_method 等；金额统一人民币元，续航须记录 CLTC/WLTC/实测与条件。
- checked_at 使用含时区 ISO 8601；valid_until 未知为 null，不代表永久有效。
- 实际报告引用 vehicle_id、fact_id、source_id 及数据 commit SHA。事实变更时报告不会自动重算，发布前必须复核。

## 来源表

registry.json 的 sources 数组每项含 source_id、publisher、author、title、url、published_at、accessed_at、origin_group、locator、rights。source_id 唯一，事实引用须存在；URL 指向原始页面，locator 记录页码/段落/视频时间点。

## v0.1 检查方式

当前为人工字段规范，不附自动 schema 校验器。录入时检查 JSON 可解析、ID 唯一、引用存在、示例与真实记录隔离、三源独立性及有效期；不能因为语法正确就认定事实真实。

后续字段兼容增加可升级次版本；删除或改变含义须升级主版本并提供迁移说明。迁移前保留原数据提交。
