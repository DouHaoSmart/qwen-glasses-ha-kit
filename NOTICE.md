# NOTICE — 归属、许可与商标提示

> **本文件不是法律意见。** 以下仅为便于用户自行核对的摘要与指针；以各项目官方 LICENSE / 开发者协议原文为准。商业或再分发前请自行合规审查，必要时咨询专业人士。

---

## 1. 本仓库（[豆号智家](https://www.douhaosmart.com)模板）

- 维护品牌：**[豆号智家](https://www.douhaosmart.com)（DouHaoSmart）** / Donnie Ming  
- 仓库：https://github.com/DouHaoSmart/qwen-glasses-ha-kit  
- 对本仓库**原创**的教程、Skill 示例、OpenAPI stub、检查清单等采用 **Apache License 2.0**（见根目录 [`LICENSE`](./LICENSE)）。  
- 上述许可证**仅**覆盖本仓作者创作的内容，**不**改变、不转授任何第三方软件的许可。

---

## 2. XiaoMi / ha_xiaomi_home（Home Assistant 集成）

- 项目：https://github.com/XiaoMi/ha_xiaomi_home  
- 本开源教程**要求用户自行**从上游安装该集成；**本仓不附带、不再分发、不重新许可**其源代码。  
- 据该仓库公开的 `LICENSE.md`（请以当时版本为准），其条款为**非商业**导向的定制许可：通常仅授权为**非商业目的使用 Home Assistant** 而复制、使用、修改、分发；并常见表述为**未授权**将软件用于开发 **APP、Web 服务**等。  
- **因此本项目立场：**  
  - 推荐场景：个人 / 非商业、**自托管** Home Assistant、**私有**千问 Skill。  
  - **不**提供多租户托管桥，也**不**鼓励把该集成包装成面向公众的 Web/云控服务。  
  - 任何超出上游许可的用途，由使用者自行负责取得书面授权或改用其他合规路径（例如小米 IoT 官方「控制应用」等，需另行申请）。

---

## 3. XiaoMi / xiaomi-miloco（非本 MVP 依赖）

- 项目：https://github.com/XiaoMi/xiaomi-miloco  
- 本教程 **MVP 不依赖** Miloco。若你自行安装，请同样阅读其非商业许可及关于 APP / Web 服务的限制表述，勿默认可被公有云 Skill 长期调用。

---

## 4. Home Assistant

- Home Assistant 为核心开源家庭自动化平台，有独立的许可与商标政策。  
- 通过 REST API、Long-Lived Access Token 访问时，请遵守 HA 安全实践：HTTPS、最小暴露、可撤废 token、勿将管理员级凭证写入公开仓库或可共享 Skill。

---

## 5. 千问 / 阿里相关平台

- 硬件与技能：[千问 AI 硬件开放平台](https://device.qianwen.com)（`device.qianwen.com`）  
- 通用智能体平台：`open.qianwen.com`（**不替代**眼镜硬件 Skill / SDK）  
- 使用技能平台、MCP/OpenAPI 插件、真机调试与发布时，须遵守当时有效的**开发者服务协议、隐私政策、使用限制**（含工具超时等）。  
- 本仓模板中的 Skill / OpenAPI 示例仅为结构示意，**不**表示已获平台上架批准，也**不**授予千问侧任何官方标识使用权。

---

## 6. 商标

| 名称 | 说明 |
| --- | --- |
| 米家、小米、Xiaomi 等 | 归小米及相关权利人；本项目非小米官方 |
| 千问、通义等 | 归阿里及相关权利人；本项目非千问官方 |
| Home Assistant | 归其权利人 |
| **[豆号智家](https://www.douhaosmart.com) / DouHaoSmart / douhaosmart** | 本教程维护品牌 |

未经授权，请勿在物料中暗示「官方合作」「官方 Skill」等易混淆表述。

---

## 7. 第三方内容

若文档引用社区帖、截图或外部 API 字段名，版权与准确性以原出处为准；链接可能失效，请以现行官方文档为准。

---

最后更新日期：2026-11-09
