# Terraria Seed Combination Generator

一个用于随机组合《泰拉瑞亚》特殊世界种子的网页工具。纯前端实现，无需后端，可直接托管在 GitHub Pages 上。

## 功能特点

- **随机组合**：按 A / B / C 三类地形变化 + 玩法影响 + 仅外观，随机抽取一组种子组合
- **冲突拦截**：内置硬冲突（无法共存）与软冲突（可能冗余/覆盖）检测，生成时自动规避硬冲突，并对软冲突给出提示
- **排除过滤**：可勾选不想玩到的地形种子或玩法种子，生成时自动排除
- **规则可调**：抽取数量规则集中在脚本顶部 `ROLL_RULES` 中，方便自行修改
- **响应式布局**：适配桌面与移动端，结果卡片每行最多 3 个并排显示

## 使用方法

1. 下载或克隆本仓库
2. 直接用浏览器打开 `roll.html` 即可使用
3. 点击「重新生成一组」随机抽取，点击「清空勾选」重置排除项
4. 展开「不想玩到的地形种子 / 玩法种子」可勾选排除特定种子

## 部署到 GitHub Pages（免费）

1. 新建一个公开仓库（Public）
2. 将 `roll.html` 重命名为 `index.html` 后上传到仓库根目录
3. 进入仓库 **Settings → Pages**
4. **Source** 选择 `Deploy from a branch`，**Branch** 选 `main`，文件夹选 `/ (root)`，点击 **Save**
5. 等待 1~2 分钟，访问 `https://你的用户名.github.io/仓库名/`

> 公开仓库使用 GitHub Pages 完全免费；私有仓库托管需要付费账户。

## 抽取规则配置

脚本顶部的 `ROLL_RULES` 可自定义各类种子的抽取数量：

```js
const ROLL_RULES = {
  A: { min: 0, max: 2, allowZero: true },        // 整体结构剧变
  B: { min: 0, max: 2, allowZero: true },        // 大片地形替换
  C: { min: 0, max: 1, allowZero: true },        // 局部结构增减
  GAMEPLAY: { min: 1, max: 2, allowZero: false },// 玩法影响
  VISUAL: { min: 0, max: 0, allowZero: true },   // 仅外观
  GLOBAL: {
    maxTotalTerrain: 4,   // A+B+C 总数上限
    minTotalTerrain: 1,   // A+B+C 总数下限
  },
};
```

## 冲突机制说明

- **硬冲突（CONFLICTS）**：逻辑互斥、无法同时生效的组合，抽取时自动避免
- **软冲突（SOFT_CONFLICTS）**：可能互相覆盖或冗余的组合，允许出现但会高亮提示
- **固定排除（EXCLUDED_TEXTS）**：默认不参与抽取的种子（如 `I am error`、`how did I get here` 等）
- **用户排除**：通过页面勾选动态排除，若排除过多导致某类无可选种子，会自动忽略部分排除并提示

## 数据来源

- [terraria.wiki.gg - 特殊世界种子](https://terraria.wiki.gg/zh/wiki/特殊世界种子)
- [terraria.wiki.gg - 秘密世界种子](https://terraria.wiki.gg/zh/wiki/秘密世界种子)

> 数据仅用于随机组合参考，具体效果以游戏内为准。

## 许可

可自由使用、修改与分发。
