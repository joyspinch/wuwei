# 无为修仙传 · WUWEI

> Godot 版《无为修仙传》的 Zan 原生重制：修行、历练、百艺、万宝、宗门、轮回六大系统。

用 [Zan](https://github.com/joyspinch/zan-lang) 语言写的独立游戏项目（仓库根自带 git 仓库）。完整设计与实现说明见 [`PROJECT.md`](PROJECT.md)。

## 玩法

- **修行**：吐纳/炼气自动运转，灵气、境界（`realms.csv` 10 境）、突破；
- **历练**：29 张地图、69 种敌人，回合制遭遇战，掉落与任务（`quests.csv`）；
- **杂学（百艺）**：108 个配方（钓鱼/采药/炼丹…），按分类筛选、分页制作；
- **万宝**：行囊 236 种物品，装备/使用/售出/分解；坊市（`market.csv`）；
- **宗门**：入门、宗门任务、宝库（`sects.csv` / `sect_tasks.csv` / `sect_vault.csv`）；
- **轮回**：转生继承（因果/世数），天赋（`talents.csv`）与熟练度星级；
- **成就**：33 项成就；设置页音量调节，背景音乐循环播放。

主菜单按原作版式复刻：整幅背景、题字、四个入口，加载资源后进入。
游戏主壳的中部 16 个页面均为 flex 纵列（`zan-flex class="column"`）：
定高行声明尺寸、卡片与行带 `grow` 撑满剩余空间，任何窗口尺寸下页面
正好填满视口——不出现滚动条，也不留页底死空间。

## 构建

需要 [zan-lang](https://github.com/joyspinch/zan-lang) 仓库（`zanc` 编译器、公共包与 stdlib 都在里面）：

```powershell
git clone https://github.com/joyspinch/zan-lang.git
$env:ZAN_HOME = 'D:/path/to/zan-lang'   # 指到刚克隆的 zan-lang 仓库根

pwsh -File client/tools/build.ps1
```

发布版默认走「表格 AES-GCM 加密 + 资源内嵌」，需要 Python 3 与 `cryptography` 包；想改表调试就加 `-Development` 走明文散装。

产物：`build/release/WuweiCultivation.exe`（运行目录要带上它旁边的 `assets/` 与 `skins/`）。

## 运行

```powershell
cd build/release
.\WuweiCultivation.exe
```

## 测试

```powershell
pwsh -File client/tools/test.ps1
```

## 目录结构

```
wuwei/
client/
  src/      # 游戏源码（.zan 源码 + HTML 界面设计稿）
  assets/   # 位图 / 音频素材
  data/     # 数值表与数据文件
  tests/    # 玩法断言用例
  tools/    # 构建与测试脚本
  skins/    # 皮肤包
PROJECT.md
```

## 素材与授权

- 素材清单与授权说明见 [`client/ASSETS.md`](client/ASSETS.md)。

## 许可

本仓库采用 [MIT 许可](LICENSE)。依赖的 zan-lang 仓库采用 ZCSL（Zan Community Source License 1.0）。

## 更多文档

- [`PROJECT.md`](PROJECT.md) —— 完整设计与实现说明
- [`client/README.md`](client/README.md) —— 客户端侧说明
- [`client/ASSETS.md`](client/ASSETS.md) —— 素材清单
