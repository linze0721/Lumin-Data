# Lumin-Data

绿梦(时空之声,`com.zhuziplay.lvmengnew.op`)从 FairGuard 资源加密中**离线完整导出**的全部数据。
解密工具(Lumin-Dumper,纯 Zig)可从任意容器密文直接算出密钥流,解密与导出全程无需运行游戏。

## 内容

```
prod/            正式服(build 12451 / client v1.0.5):
  tables/           374 张配置表 .bytes(全 JSON 文本;excel/bin 导出)
  tables_csv/       上表的 CSV 版(UTF-8 BOM,Excel 直接打开)
  localization/     19 张 Unity Localization 文本表(textmap)JSON,带类型树
  localization_csv/ textmap 四语对照 CSV(id,key,zh,en,ja)
  dll/              48 个热更 DLL(全部 MZ 有效)
  story/            完整剧情:每场一个 AVG_<id>.txt + 剧情全量.csv(1243 场 / 13,568 句)

dev_v94/         dev/beta 测试线最新可下载线(build 12787 / cs v94,zip 在
                 https://cdn-rs-lm.zhuziplay.com/full_v1/release/en/a/dev/...):
  tables/           374 张表(比 prod 多更新 20 张剧情/任务/文案;含 prod 已删的 4 张)
  tables_csv/       CSV 版
  localization/     19 张 textmap(shortcommon_zh 31436 条,比 prod 多 14 条)
  localization_csv/ 四语对照
  CHARACTERS.md     角色挖掘结论(可玩 19 人与 prod 一致;dev 包内 6 个未实装
                    模型:Role_07/12/14/15/19/23,undefined 名单中"瑟拉"最接近可玩)
  characters.csv    19 人角色明细(Id/Name/Tags/Config)
  model_names.txt   assets v143 全部 12,344 bundle 的模型相关容器路径(挖掘证据)
  story/            dev 完整剧情(1244 场 / 13,582 句;比 prod 多 1 场新 AVG)

il2cpp/          dump.cs(46.9 MB,IL2CPP 元数据重建;对应 Lumin-Dumper 的逆向用途)
data.unity3d/    APK 内置 data.unity3d 完全解密版(du3d_fixed.bin,UnityPy 14070 对象)
```

## 使用建议

- `tools/`(Zig,见 Lumin-Dumper)可从 `yoo/yoo/<Package>/BundleFiles/<2>/<hash>/__data` 解出任何容器,再取 TextAsset/MonoBehaviour。
- 文本表里几乎所有数字(如 `Name`=24616)都是文本 id,查 `localization_csv/shortcommon.csv` 得原文。
- 热更代码在 dev_v94 线不公开(zip 走 `/full_v1/debug/...` 内网),prod 的 48 个 DLL 是最新可得。

## 验证

- 374 张表分别经密文独立复算和运行时捕获双路径逐字节比对,0 差异。
- `cs_tables_localization/` 中的 textmap 直接来自各容器 MonoBehaviour 的类型树,与字段一一对应。

## 更新方法

1. `POST https://lmapi.zhuziplay.com/remote/config`(请求体含 `app_env`:beta/dev 与 build_id)拿清单。
2. 下载 `normal.full[]` 的 zip(host `https://cdn-rs-lm.zhuziplay.com`,URL 里 `/release/de/a/` → `/release/en/a/`)。
3. 解压(每 zip 为 YooAsset 缓存:`xx/<hash>/__data + __info`),用 Lumin-Dumper 解密,再取 TextAsset / MonoBehaviour。
