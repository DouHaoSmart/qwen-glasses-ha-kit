# 千问 AI 眼镜 × Home Assistant 控制套件

**由 [豆号智家](https://www.douhaosmart.com)（DouHaoSmart） / Donnie Ming 维护的免费开源教程与配置模板。**

用自己的 **Home Assistant** + 小米官方集成 [`ha_xiaomi_home`](https://github.com/XiaoMi/ha_xiaomi_home)，通过千问技能平台的 **私有 Skill**，在千问 AI 眼镜上语音开关灯、执行场景。

> **没有托管桥接服务。** 指令只在「千问云 → 你暴露的 HTTPS → 你家的 HA」之间传递；我们不代持你的小米账号，也不运营多租户后端。

仓库：[`DouHaoSmart/qwen-glasses-ha-kit`](https://github.com/DouHaoSmart/qwen-glasses-ha-kit)

---

## 这是什么 / 不是什么

| 是 | 不是 |
| --- | --- |
| 教程 + `SKILL.md` / OpenAPI 示例 / 检查清单 | 云端「一键米家」SaaS |
| 帮你对接**自己的** HA | 重新打包或再授权小米集成源码 |
| 推荐 **个人私有 Skill** | 开箱即用的公开市场多用户 Skill |
| 品牌展示与社区友好文档 | 小米或千问官方产品 |

许可证说明见 [`NOTICE.md`](./NOTICE.md)。本仓原创模板与文档采用 **Apache-2.0**（见 [`LICENSE`](./LICENSE)）。**本文不构成法律意见。**

---

## 架构（简图）

```text
千问 AI 眼镜语音
  → 私有 Skill（本仓 templates/skill）
    → OpenAPI / MCP 插件（Bearer = 你的 HA Long-Lived Token）
      → 你的 HTTPS 隧道
        → Home Assistant /api/services/...
          → ha_xiaomi_home（你自行从上游安装）
            → 米家灯 / 场景
```

这是常见的「眼镜 / 语音助手 → 私有 Skill → 自托管 HA → 设备集成」链路。本仓面向 **千问** 技能平台与 **米家（经 ha_xiaomi_home）**，受众是私有 Skill 开发者。

**原则**

- 本开源项目 = 文档 + 模板，**运行时全部在用户侧**。
- 千问云只调用用户暴露的 HTTPS；[豆号智家](https://www.douhaosmart.com) **不中转设备指令**。
- **不要**把 `XiaoMi/ha_xiaomi_home` 源码拷进本仓再分发——请按上游文档自行安装。

---

## 你需要自备

1. **千问 AI 眼镜**（如 S1）+「千问 AI 穿戴」App + [device.qianwen.com](https://device.qianwen.com) 开发者账号  
2. **常驻 Home Assistant**（建议 Core ≥ 2024.4.4，以 `ha_xiaomi_home` 文档为准）  
3. 按上游说明安装并完成 **小米账号 OAuth** 的 [`XiaoMi/ha_xiaomi_home`](https://github.com/XiaoMi/ha_xiaomi_home)  
4. 让千问云能访问到 HA 的 **HTTPS 入口**（Nabu Casa / Cloudflare Tunnel / 自建反代等）  
5. 一枚 HA **Long-Lived Access Token**（仅用于你的私有插件；勿写入可分享的 Skill）

---

## 安装步骤（高层）

> 逐步勾选版见 [`templates/docs/setup-checklist.md`](./templates/docs/setup-checklist.md)。

1. **HA**：确认灯、场景实体已出现且可在 HA 里手动控制。  
2. **公网 HTTPS**：隧道就绪；用 `curl` 测 `POST /api/services/light/turn_on`（建议 < 3s，对齐千问工具超时）。  
3. **千问工具**：在技能平台创建 **OpenAPI 或 MCP** 插件，指向你的 HA（或对照 [`templates/openapi/ha-services.example.yaml`](./templates/openapi/ha-services.example.yaml) 裁剪）；认证选 Bearer，填入 LLAT。  
4. **Skill**：复制 [`templates/skill/SKILL.md`](./templates/skill/SKILL.md)，改成你的 `entity_id` 与工具引用名；**发布渠道选个人私有**（推荐）。  
5. **真机**：设备管理绑定眼镜 → Skill 真机调试 → 说「打开客厅灯」等召回语。  
6. **收尾**：撤销测试用 token 的权限或轮换；不要把密钥提交进 Git。

---

## 仓库内容

```text
LICENSE                          # Apache-2.0（仅本仓原创模板与文档）
NOTICE.md                        # 上游归属与许可提示
CONTRIBUTING.md
README.md
templates/
  skill/SKILL.md                 # 示例私有 Skill
  openapi/ha-services.example.yaml
  docs/setup-checklist.md
```

本仓**不包含** `ha_xiaomi_home` 源码。请从 [XiaoMi/ha_xiaomi_home](https://github.com/XiaoMi/ha_xiaomi_home) 安装。

---

## 免责声明

- 控制智能家居设备有安全与隐私风险；请限制公网暴露面，并仅为自己的账号与设备使用。  
- `ha_xiaomi_home` 等上游项目有**各自的非商业等许可条款**；请阅读原文。将其用于 APP、Web 服务或商业场景前，请自行评估合规，必要时咨询专业人士。  
- 千问开放平台有工具超时、审核与开发者协议约束；以官方文档为准。  
- [豆号智家](https://www.douhaosmart.com) 提供模板「按原样（AS IS）」，不保证适用于某一特定设备型号或地区。

---

## 品牌与链接

| 项 | 链接 |
| --- | --- |
| 本仓库 | https://github.com/DouHaoSmart/qwen-glasses-ha-kit |
| Issues | https://github.com/DouHaoSmart/qwen-glasses-ha-kit/issues |
| [豆号智家](https://www.douhaosmart.com)官网 | https://www.douhaosmart.com |
| 千问硬件开放平台 | https://device.qianwen.com |
| ha_xiaomi_home | https://github.com/XiaoMi/ha_xiaomi_home |

---

## 推荐用法（务必阅读）

- **只建私有 Skill**，服务你自己的眼镜与 HA。  
- **不要**把同一枚 HA Token 做成给陌生人用的公开 Skill。  
- **不要**指望本教程变成多租户托管；那不是本项目目标。  
- 若你需要面向大量终端用户的正式米家云控产品，请自行调研小米 IoT「控制应用」等官方路径——那是另一条产品线，不在本仓范围。

---

维护：Donnie Ming · [豆号智家](https://www.douhaosmart.com)（DouHaoSmart）
