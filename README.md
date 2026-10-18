# 汽车买车研究与内容工作台

第一版 v0.1：把消费者需求 → 车型证据 → 购车建议 → 自媒体内容串成可追溯流程。采用 Markdown + JSON，无数据库服务或付费依赖；当前只有虚构示例，没有已核实车型数据。

## 目录

- `skills/car-buying-analysis/`：购车研究 Skill 与随包参考规范。
- `data/vehicles/`：按中国市场、车系、年款、具体配置记录车型。
- `data/sources/`：来源登记表；车型里的每条事实引用 source_id。
- `intake/`：用户需求采集模板与匿名示例。
- `content/templates/`：购车报告、新车上市、短视频模板。
- `content/projects/`：选题到发布的项目清单。
- `docs/`：证据、字段、协作和扩展约定。

## 从第一次使用开始

1. 复制 [需求模板](intake/brief-template.md) 到本地 `private/intake/`，填已知条件；未知项保留未知。
2. 以 [车型示例](data/vehicles/example-2026-base.json) 为结构，新建真实车型文件并设置 `is_example=false`；按 [字段约定](docs/data-contract.md) 填写。
3. 在 [来源表](data/sources/registry.json) 登记原始链接、日期、机构、独立来源组；真实来源不得使用示例 URL。
4. 按 [证据规范](docs/sources.md) 逐项核实。关键结论至少三条独立信息源，未满足就保留待核实，不补造证据。
5. 使用 [研究 Skill](skills/car-buying-analysis/SKILL.md) 和 [购车报告模板](content/templates/buying-report.md)，形成条件式建议。
6. 复制 [内容项目清单](content/projects/project-template.md)，选择上市图文或短视频模板；人工复核后再发布，记录链接与反馈。

## 使用 Skill

支持仓库读取的助手可直接读取 `skills/car-buying-analysis/SKILL.md`。安装到支持本地 Skill 的客户端时，复制整个 `skills/car-buying-analysis/` 文件夹到该客户端的技能目录；随包 references 必须保留。安装不会自动同步本仓库的数据；调用时同时提供仓库路径及目标车型文件。

## 维护约定

- 本仓库维护可复用规则、公开证据和匿名内容；真实客户需求、合同、联系方式放 `private/`，不提交。仓库当前公开，忽略规则不能撤回已经提交的秘密。
- 真实车型数据由本仓库维护；Obsidian 可以链接或导出阅读副本，避免两边同时修改。v0.1 未配置自动同步。
- 价格区分指导价、报价、核实成交价和落地价，逐条记录地区、支付条件与有效期；发布前重新确认。
- 历史研究和文章引用明确 commit SHA；保留历史，不把过期结论当作当前事实。
- [协作与扩展约定](docs/contributing.md) 规定 ID、版本迁移、审核和后续路线。
- 本版不包含自动抓取、自动发布、客户管理系统或车型推荐算法；按实际使用需求逐步增加。
