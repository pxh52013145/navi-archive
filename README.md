# Navi Archive — Amazfit 表盘设计资产库

从 Amazfit 表盘（HMDIAL / QZIP · protobuf-varint 格式）逆向提取的 **87 组设计素材**：数字、指针、表盘环、背景、图标、字形等。其中 **78 组为透明底**，可直接用于设计稿与开发。

- **在线画廊**：<https://pxh52013145.github.io/navi-archive/>
- 交互：总线树两级导航（表盘 → 分类）、标签 AND 筛选、搜索、URL 深链（`?d=navi_en&c=digit`）、详情弹层、实时表盘预览
- **拖拽取图**：直接把卡片 / 弹层大图拖到画布（Figma / PS）或桌面，得到最大尺寸 WebP（透明底）；拖到桌面会自动下载为 `素材id-宽x高.webp`

## 直链引用

所有素材都是**相对路径直链**，可外链或整包下载：

```
img/<hash>-<宽>.webp    # 通用（透明底）
img/<hash>-<宽>.avif    # 更小，现代浏览器
```

文件名与尺寸清单见 [`data.json`](data.json)（`assets[].img` 字段）。

### jsDelivr CDN 镜像（全球加速）

```
https://cdn.jsdelivr.net/gh/pxh52013145/navi-archive@main/img/<文件名>
```

## 速度

- AVIF → WebP 两级 `<picture>` 回退 + `srcset` 尺寸自适应，弱网自动降级
- `loading="lazy"` + IntersectionObserver 分批渲染（36/批）
- GitHub Pages 自带 CDN 与 brotli/gzip；全站图片仅 ~800KB

## 更新素材

本地项目（`gallery/`）里执行：

```bash
python build_site.py          # 重建 data.json + img/
cd web && npm run build       # 重建 index.html + assets/
cd ../site
git add -A && git commit -m "rebuild" && git push   # Pages 自动部署
```

## 提取与构建

素材来自表盘文件逆向：切片 → 像素哈希去重（140 切片 → 87 唯一素材，`×N` 标注重复）→ 尺寸规则 + 聚类推断分类 → 像素统计生成标签（色相 / 透明度 / 填充率）。构建器与画廊源码在本地 `gallery/` 项目（Python + React/Vite）。
