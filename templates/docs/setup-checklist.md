# 部署检查清单（用户自托管）

按顺序勾选。目标：千问 AI 眼镜私有 Skill → 你家 HA → 米家灯/场景。  
**无托管桥；推荐仅私有 Skill。** 许可提示见仓库根目录 `NOTICE.md`（非法律意见）。

---

## A. Home Assistant

- [ ] 已有常驻 HA 实例（建议 Core 版本满足 `ha_xiaomi_home` 文档要求，常见 ≥ 2024.4.4）
- [ ] 能用浏览器登录 HA，UI 正常
- [ ] 已记录将用于演示的灯 / 场景的 **entity_id**（例如 `light.living_room`、`scene.sleep`）

---

## B. ha_xiaomi_home（米家）

- [ ] 已从上游安装 [XiaoMi/ha_xiaomi_home](https://github.com/XiaoMi/ha_xiaomi_home)（HACS 或手动），**不是**从本教程仓拷贝源码再分发
- [ ] 已按官方集成配置流完成 **小米账号 OAuth**
- [ ] 目标灯、场景已出现在 HA，且在 HA 内手动开关/激活成功
- [ ] 已阅读上游 `LICENSE.md`：理解非商业等约束；本教程场景为个人自托管私有使用

---

## C. HTTPS 隧道（千问云必须打到你家）

- [ ] 已选择入口：Nabu Casa / Cloudflare Tunnel / 其他反代（任选其一）
- [ ] 公网 URL 为 **HTTPS**（勿对公网裸奔 HTTP / 裸 8123）
- [ ] 已签发 HA **Long-Lived Access Token**，仅保存在密码管理器 / 私有插件配置
- [ ] 本机验证（将 `HOST`、`TOKEN`、`ENTITY` 换成你的值）：

```bash
curl -sS -o /dev/null -w "%{http_code} time=%{time_total}\n" \
  -X POST "https://HOST/api/services/light/turn_on" \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"entity_id":"ENTITY"}'
```

- [ ] HTTP 状态可接受（通常 200），且总耗时尽量 **&lt; 3s**（对齐千问工具超时）
- [ ] 同样验证 `light/turn_off` 与 `scene/turn_on`

---

## D. 千问 MCP / OpenAPI 插件

- [ ] 登录 [device.qianwen.com](https://device.qianwen.com)（硬件技能平台，不是 `open.qianwen.com` 替代品）
- [ ] 新建 **OpenAPI** 或 **MCP** 工具插件，Base URL = 你的 HTTPS HA
- [ ] 认证选 **Bearer Token**（或文档允许的等价 Header），填入 LLAT——**不要**选「无认证」
- [ ] 导入或手写路径：对照 `templates/openapi/ha-services.example.yaml`（`light_turn_on` / `light_turn_off` / `scene_turn_on`）
- [ ] 在插件页刷新/探测工具列表，确认工具可见
- [ ] 沙箱或试调用成功；确认失败时不会把 Token 打进日志外传

---

## E. 私有 Skill

- [ ] 复制 `templates/skill/SKILL.md`，修改 `name` / `description` 与实体映射表
- [ ] 创建 Skill 时勾选上一步的工具；引用名改为控制台实际 `{pluginCode}.{toolName}`
- [ ] **发布渠道选个人私有**（推荐）；勿把个人 Token 工具配进可共享包
- [ ] 沙箱调试：文本模拟「打开客厅灯」能调到正确工具与 entity

---

## F. S1 / 真机测试

- [ ] 「千问 AI 穿戴」App 已登录与开发者同一主体账号
- [ ] 开放平台 **设备管理** 已绑定眼镜（一键或扫码）
- [ ] Skill 页开启 **真机测试** / 开发者模式（以控制台文案为准）
- [ ] 对眼镜说出召回语，灯或场景有实物反馈 + 语音确认
- [ ] 测试结束后按需关闭开发者模式；长期不用可解除设备绑定
- [ ] 演示录像/截图（可选）时打码域名与 Token

---

## G. 收尾与安全

- [ ] Token 未写入 Git；`.env` / 本地笔记不进公开仓
- [ ] 已知如何在 HA 配置文件中 **撤销/轮换** LLAT
- [ ] 已读仓库 `NOTICE.md` 与 `README` 免责声明
- [ ] 若有商业/多用户计划：停止套用本清单，改评估小米 IoT 控制应用等正式路径（超出本教程）

---

完成标志：眼镜一句话能稳定开关**至少一盏灯**并执行**至少一个场景**，且全程仅使用你自己的 HA 与私有 Skill。
