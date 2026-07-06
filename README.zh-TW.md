**[English](README.md) | 繁體中文**

# Sakura Atelier

一個以滾動敘事為主軸的互動單頁網站,主題是一間虛構的水墨與櫻花工作室——結合滾動視差、SVG 筆畫繪製動畫,以及即時 GPU 流體模擬,作為設計示範作品。

**線上展示:** https://fab34.github.io/sakura-atelier/

## 功能特色

- **滾動視差** — 每個區塊有多層背景以不同速度與方向隨滾動位移。
- **滾輪驅動的 SVG 筆畫繪製** — 墨枝、禪圓(ensō)、裝飾花紋、鳥居線稿,會在對應區塊滾入畫面時逐筆「畫」出來(使用 GSAP `ScrollTrigger` 搭配 `stroke-dashoffset` 技巧)。
- **百葉窗遮罩轉場** — 引言區塊會透過多條動畫色塊組成的遮罩「掀開」進入下一個區塊,靈感來自 [tympanus 的 SVG mask 滾動轉場範例](https://tympanus.net/Tutorials/SVGMaskScrollTransition/)。
- **墨流し(Suminagashi)水墨流體背景** — 首頁區塊執行完整的 GPU 流體模擬(velocity/dye 平流、curl 與渦度侷限、散度、jacobi 壓力求解、梯度減除),以 Three.js 渲染。可點擊或拖曳畫面攪動墨色、切換四種傳統墨色、開關自動演出,或將畫布洗滌乾淨。
- 完全響應式版面,並會依 `prefers-reduced-motion` 降低自動演出頻率。

## 技術棧

- 純靜態 HTML/CSS/JS — 無需建置流程、無框架、無後端。
- [GSAP](https://greensock.com/gsap/) + `ScrollTrigger` — 滾動連動動畫與釘選(pin)效果。
- [Three.js r128](https://threejs.org/) — 流體模擬的 WebGL 渲染。
- Google Fonts:Cormorant Garamond、Noto Serif JP、Shippori Mincho。
- [辰宇落雁體 ChenYuluoyan](https://github.com/Chenyu-otf/chenyuluoyan_thin)(OFL-1.1 授權)— 用於結尾引言文字;已裁剪(subset)成只包含實際用到的字,檔案僅約 12KB(`fonts/chenyuluoyan-quote-subset.woff2`)。

## 專案結構

```
.
├── index.html   # 整個網站——標記、樣式、腳本都在單一檔案內
└── README.md
```

## 本機執行

不需要任何建置步驟,用任何靜態檔案伺服器即可,例如:

```bash
python3 -m http.server 8080
# 然後開啟 http://localhost:8080
```

直接用 `file://` 開啟 `index.html`無法正常運作——流體模擬與字型載入需要 HTTP 環境。

## 部署方式

網站透過 **GitHub Pages** 部署,從 `main` 分支根目錄發佈。推送到 `main` 會自動更新線上網站。

## 瀏覽器支援

需要支援 WebGL 的現代瀏覽器。流體模擬會自動偵測可用的最佳材質精度(float → half-float → byte),在較弱的顯示晶片上會優雅降級;當首頁區塊被捲出畫面外或分頁被切換到背景時,會自動暫停運算。

## 授權

未指定授權條款——版權歸作者所有。
