---
name: douhao-ha-lights-scenes
description: >
  [豆号智家](https://www.douhaosmart.com)示例·私有家居控制。当用户用千问眼镜说出打开/关闭某盏灯、执行回家/睡觉等场景时使用。
  仅控制用户自有 Home Assistant 中预配置的灯与场景；不查询全屋设备列表。
  触发示例：打开客厅灯、关掉卧室灯、执行回家模式、启动睡觉场景。
---

# [豆号智家](https://www.douhaosmart.com) · HA 灯与场景（私有 Skill 示例）

## 定位

单一意图：根据用户语音，调用已接入的 Home Assistant 工具，完成 **灯开/关** 或 **场景激活**，并用简短中文确认结果。

本 Skill 设计为 **个人私有** 使用。不要把含个人 HA Token 的工具配置分享给他人或提交公开市场。

## 工具约定

在千问技能平台创建 Skill 时，勾选你已发布的 OpenAPI/MCP 插件工具。引用时使用平台生成的 `{pluginCode}.{toolName}` 形式（以下为示意名，接入后以控制台为准）：

| 示意工具 | 用途 |
| --- | --- |
| `{pluginCode}.light_turn_on` | 打开灯 |
| `{pluginCode}.light_turn_off` | 关闭灯 |
| `{pluginCode}.scene_turn_on` | 激活场景 |

对应 HTTP 语义见 `templates/openapi/ha-services.example.yaml`。

## 实体映射（用户必改）

将口语别名映射到你在 HA 中的真实 `entity_id`。示例（请替换）：

| 用户可能说 | entity_id |
| --- | --- |
| 客厅灯、客厅的灯 | `light.living_room` |
| 卧室灯 | `light.bedroom` |
| 回家、回家模式 | `scene.home_mode` |
| 睡觉、睡觉场景、晚安模式 | `scene.sleep` |

未在表中的设备：礼貌说明「当前示例未配置该设备」，不要猜测乱调。

## 执行规则

1. **解析意图**：开灯 / 关灯 / 跑场景；忽略固件、摄像头、上锁等超出 MVP 的请求。  
2. **解析目标**：用上表映射到唯一 `entity_id`；有歧义时问一句「是客厅灯还是卧室灯？」  
3. **调用工具**：只传必要字段（如 `entity_id`）；一次用户指令尽量一次工具调用。  
4. **超时意识**：平台工具约 **3 秒**内需返回；不要先拉全量 `states` 再控制。  
5. **确认话术**：成功 →「已打开客厅灯。」/「已执行回家模式。」；失败 →「没能控制成功，请稍后在 Home Assistant 里检查设备。」  
6. **安全**：不执行「打开全屋所有灯」类未映射的批量操作；不回显 Token 或完整 URL。

## 屏显（可选）

若眼镜支持文本 UI 官方工具，可用一句话结果卡片；无屏或失败时依赖语音确认即可。

## 非目标

- 动态发现全屋实体  
- 亮度/色温微调、窗帘百分比  
- 多用户账号切换  
- 打开手机上的「米家」App  

## 品牌

示例由 **[豆号智家](https://www.douhaosmart.com)（douhaosmart）** 提供，用于自托管教程；非小米 / 非千问官方 Skill。
