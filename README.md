# Aya-poke

HoshinoBot 公主连结「戳一戳集卡」插件。戳一戳机器人，她可能会送你公主连结卡片哦~

原插件为 [GWYOG/GWYOG-Hoshino-plugins](https://github.com/GWYOG/GWYOG-Hoshino-plugins) 的 pokemanpcr（2021 年起停更），本仓库在其最终版本基础上维护，与原版的主要差异有两点：

1. **适配 NapCat 戳一戳 API**：原版回戳使用 go-cqhttp 时代的 `poke` 消息段，而 OneBot 11 标准并无该消息段，在 NapCat 协议端下会被静默丢弃（不报错、不回戳）；现改为调用 NapCat 专用 action `group_poke`。
2. **优化卡片黑名单**：原版按图标文件名手工维护黑名单；现改为角色号段白名单制——官方 1xxx 号段自动收录，主人公、剧情 NPC 额外头像（7 位文件名）等非收集内容自动排除，并防止 7 位文件名被截断解析成假卡；启动预检与「刷新卡片」指令共用同一份卡池逻辑。

## 功能

- 戳一戳机器人：概率掉落卡片（1% 大暴击 10 连），每日掉落次数上限
- 合成/一键合成：献祭卡片获得新卡
- 交换 / 赠送：玩家间卡片流通
- 查看仓库：生成收集进度图与群内排名
- 刷新卡片：新增角色头像后无需重启刷新卡池

## 安装

- 依赖：bot 的 res 资源包（`res/img/priconne/unit` 角色头像）、同 bot 安装 `priconne` 模块（角色花名册）、Pillow。
- 将本仓库整个目录放入 `hoshino/modules/`（目录名任意，如 `pokemanpcr2`），在 `MODULES_ON` 加一行后重启 bot。

## 配置

主文件顶部常量可调：掉落概率、每日上限、稀有度概率、合成概率表、`CARD_EASTER_EGG_IDS`（可选：把自定义角色 chara_id 加进卡池）等。

数据落盘于 `~/.hoshino/poke_man_pcr.db`。

## License

GPL-3.0（沿用原插件许可）
