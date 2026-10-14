# Muse 风 UI 改造说明（v1）

基于 MBox（CNShanJu/MBox，TVBoxOS-Mobile 延续版）改的，改动都在 `:app` 层，没碰模块边界。

## 改了什么

1. **主题** `app/src/main/assets/theme/themes/bright/default.json`
   - 改名「暖纸」，仍为默认主题
   - `bg_body` → `#f5f3ef`（暖纸底）
   - `bg_surface` → `#ffffff`（白卡片）
   - `bg_card_alpha` → 100（卡片不透明）
   - `brand` → `#1c1c1a`（暖墨文字主色）
   - `text_highlight` / `download_active` → `#ec5b36`（暖橙强调色）
   - `btn_confirm_bg` → `#1c1c1a`
   - 构建时 `generateThemeColors` 会自动派生全套颜色，不用手改 colors.xml

2. **卡片比例** `app/.../ui/kit/RatioShadowLayout.java`
   - `RATIO_H_W` 由 `4f/3f`（3:4 竖图）改为 `9f/16f`（16:9 横图）
   - 影响：首页网格、搜索宫格、收藏、下载、搜索海报卡（统一横图）

3. **首页卡片布局** `app/src/main/res/layout/item_grid.xml`
   - 重做为白卡片：16:9 横图在上（上方圆角），标题+副标题在下
   - 保留了 `ivThumb` / `tvName` / `tvNote` / `tvYear` 四个 ID，GridAdapter 不用改
   - 年份徽章改用新建的 `@drawable/bg_badge_year`（半透明黑圆角）

## 在 Android Studio 里构建

1. 用 Android Studio 打开本目录（Gradle 项目）
2. SDK 用你本机的（已删掉 local.properties，AS 会自己配）
3. 直接 Run `app` 即可，`generateThemeColors` 会在 preBuild 自动跑
4. 如需换回竖图卡片：把 `RatioShadowLayout.RATIO_H_W` 改回 `4f/3f`

## 下一步可继续做的
- 首页顶部问候头 + Hero 大卡（需改 HomeFragment/Fragment 结构）
- 详情页抽屉式重做（activity_detail.xml）
- 暗色主题同步暖色系
