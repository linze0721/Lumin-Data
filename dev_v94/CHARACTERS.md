# 角色挖掘结论(beta_v94 = dev 线 build 12787,cs v94 / assets v143)

## 可玩角色(entityCharacterDatas):19 人,与正式服 v6 完全一致
主角(10001)、洛夕、莉塔、摩菲、达里娅、弗莉兹、贝伊、诗凛、潘娜西娅、璃琅、
阿萌、布雷兹、海拉、塔可、赛琳塔、艾提、玛塔、莉特莉丝、何雨莲。
- 标签三系:回声/共振/噪波;Id 编号 10101–12701,缺 10701/11201/11401/11501/11801-12001/12301/12401。
- v94 vs v6:全部字段零变化(v97 分支曾有 11001 PresentId、12601 SpecialEnergy 两处调整)。

## 未实装候补(assets 里有全套模型,表里没有行)
| 编号 | 名字 | 证据 | 判定 |
|---|---|---|---|
| Role_12 | **瑟拉** | dialogueCharacterDatas 11201 + 皮肤 101201/101202(Role_12_02/03,v94 新增第三个);talentNodeLevelDatas、itemWeaponUpgrades 引用 | 最接近可玩 |
| Role_14 | **诺瓦莉** | 对话+28 张表引用;Face/Body/Hair 全套贴图+表情 anim(a/i/u/e/o/微笑/脸红/受伤) | 重剧情 NPC |
| Role_19 | **艾斯塔娜** | 98 条对话、副本 raids、技能详情 4 条 | 重剧情 NPC/头目 |
| Role_23 | **薇诺娜** | 61 条对话、rewards 51、entityCharacterLevelDatas 7 | 重剧情 NPC |
| Role_07 | ? | Gacha Tape prefab 已做好,无名字无对话 | 未知 |
| Role_15 | ? | 仅模型+Skin,无任何引用 | 未知 |

- `Assets/Designer/废弃的男npc/废弃的Role_14_01/` —— Role_14 最初是废弃的男性 NPC 设计,现复用为诺瓦莉。
- CharacterHeadOnCard 头像图仅 15 张(现有卡池角色);6 个候补均无头像/立绘。
- 判定可玩角色的充分条件(四项全占):entityCharacterDatas 行 + skillGroup→skillDetail→talent 链 + CharacterHeadOnCard + Gacha 记录。

## 证据文件
- `beta_v94/model_names.txt`:4 个 assets zip(12,344 bundle)全部容器路径中角色相关条目。
- `beta_v94/role14_bundle_idx.json`:Preload 包内 Role_07/14 路径→bundle 映射。
- `beta_v94/characters.csv`:19 人明细(Id/Name/Tags/Config)。
- 角色相关表逐表对比(v6 vs v94):角色本体 0 差异;周边表 star 152→144、试用 208→90、greets 281→241、texts 88→72、NPC 对话 3448→3162、npcConfigs 930→877。
