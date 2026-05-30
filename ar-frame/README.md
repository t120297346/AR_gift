# AR Frame Gift

這是一個可部署到 GitHub Pages 的純前端 WebAR 範例，使用 A-Frame 1.5.0 與 MindAR image tracking。

## 檔案結構

```text
ar-frame/
├─ index.html
├─ assets/
│  ├─ end_frame.png
│  └─ dance.webm
├─ targets/
│  └─ frame.mind
└─ README.md
```

## 放入 `frame.mind`

1. 使用 MindAR image target compiler 將你的 target image 編譯成 `.mind` 檔案。
2. 將輸出的檔案命名為 `frame.mind`。
3. 放到這個路徑：

```text
ar-frame/targets/frame.mind
```

`index.html` 已經設定好讀取：

```html
imageTargetSrc: ./targets/frame.mind
```

## 放入 `end_frame.png`

1. 將要顯示在照片上方的圖片命名為 `end_frame.png`。
2. 放到這個路徑：

```text
ar-frame/assets/end_frame.png
```

若要調整圖片大小或位置，請編輯 `index.html` 裡的這段：

```html
<a-image
  src="#endFrame"
  position="0 0.18 0"
  width="1.1"
  height="1.1"
  rotation="0 0 0"></a-image>
```

- `width` / `height`：調整 AR 圖片大小。
- `position="x y z"`：調整 AR 圖片位置；`y` 越大越上方。
- `rotation`：調整旋轉角度。

## 放入透明背景影片 `dance.webm`

影片程式碼已經預留在 `index.html`，目前先註解起來。

1. 將透明背景影片命名為 `dance.webm`。
2. 放到這個路徑：

```text
ar-frame/assets/dance.webm
```

3. 到 `index.html` 取消 `<video id="danceVideo">` 與 `<a-video>` 的註解。
4. 依需求調整 `<a-video>` 的 `width`、`height`、`position`。

手機瀏覽器播放影片通常需要：

```html
muted
loop
playsinline
webkit-playsinline
```

本專案預留的 `<video>` 已包含這些設定。

## 部署到 GitHub Pages

這個專案是 static site，不需要 build step。

### 方法一：部署整個 repository

1. 將 `ar-frame/` commit 並 push 到 GitHub repository。
2. 到 GitHub repository 的 **Settings** → **Pages**。
3. 在 **Build and deployment** 選擇 **Deploy from a branch**。
4. Branch 選擇你的分支，例如 `main`，資料夾可選 `/root`。
5. 部署後網址通常會是：

```text
https://你的帳號.github.io/你的-repo/ar-frame/
```

### 方法二：只部署 `ar-frame` 內容

如果你想讓網址根目錄直接開啟 AR 頁面，可以把 `ar-frame/` 裡面的內容移到 repository 根目錄，再用 GitHub Pages 部署根目錄。

## 手機測試注意事項

- 手機測試需要 HTTPS，GitHub Pages 預設提供 HTTPS。
- iPhone Safari、Android Chrome 都建議直接用 HTTPS 網址測試。
- 如果相機無法開啟，請檢查：
  - 瀏覽器是否允許相機權限。
  - 網站是否使用 HTTPS。
  - `targets/frame.mind` 是否存在且路徑正確。
  - `assets/end_frame.png` 是否存在且路徑正確。

## 本機測試

因為瀏覽器相機權限通常需要 HTTPS，最接近正式環境的測試方式是部署到 GitHub Pages 後用手機開啟。

若只是檢查頁面是否能載入，可以在本機開一個 static server，例如：

```bash
cd ar-frame
python3 -m http.server 8080
```

再用瀏覽器開啟：

```text
http://localhost:8080
```

> 注意：手機從區網 IP 開啟 `http://` 網址時，可能無法取得相機權限；正式測試請使用 HTTPS。
