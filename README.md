# 🐳 Synology NAS Private Auto-Sharing Station 

![Docker Support](https://shields.io)
![Nginx](https://shields.io)
![Language](https://shields.io)
![Encoding](https://shields.io)

這是一個專為 **群暉 Synology NAS** 量身打造的 **極簡、高質感私人雲端檔案全自動分享站**。本項目基於輕量級 Nginx 容器建構，具備全自動感知同步、智慧防亂碼雙編碼解讀核心，並完美兼顧「滑鼠左鍵原地智慧預覽、滑鼠右鍵原生新分頁開啟」的骨灰級操作直覺。

---

## 🌟 項目核心亮點

* 📂 **零代碼，全自動感知上架**：徹底擺脫傳統靜態網頁人工修改網頁手續。只要將檔案丟入 `files` 資料夾，前台網頁重新整理 **一秒鐘全自動即時感知上架**。
* 🔮 **現代化科技感毛玻璃視覺**：採用響應式 UI 設計（隨手機、電視盒自動適應），搭配純 CSS 打造的 **多色發光科技感指示燈號**（圖片亮綠燈、文字亮藍燈、影片亮紫燈）。
* 🔬 **工業級雙編碼防亂碼雷達**：前端大腦內建智慧型 `TextDecoder` 核心，**自動無縫通吃新式 `UTF-8` 與台灣傳統 `Big5` (ANSI) 檔案**，左鍵點擊原地彈出發光閱讀器，徹底消滅黑色菱形亂碼。
* 🖱️ **滑鼠左/右鍵複合操作機制**：
  * **滑鼠左鍵**：多媒體與 PDF 直接線上看；純文字檔案原地跳出黑色半透明毛玻璃閱讀視窗。
  * **滑鼠右鍵**：100% 精準喚醒瀏覽器原生 **「在新分頁中開啟連結」** 系統選單，並首創 URL 路由重定向智慧捕捉技術，讓新分頁也能完美帶著解碼器分身開啟。
* 🚀 **進階後端分流防鎖死**：採用高效非阻塞的 Nginx 雙層 `map` 結構與 `alias` 匹配，點擊「檢視」一律線上預覽，點擊藍色「下載」按鈕則 **100% 全速觸發瀏覽器另存新檔**。

---

## 📂 最終完全體：系統目錄結構矩陣

本項目結構極其純粹、輕量。日後若需搬移、備份系統，僅需將此目錄打包帶走即可：

| 層級與實體路徑 | 檔案 / 資料夾名稱 | 檔案類型 / 權限 | 系統中所扮演的核心職責與機制 |
| :--- | :--- | :--- | :--- |
| 根目錄 `/my-web-server/` | **`docker-compose.yml`** | YAML 設定檔 | **環境守護神**：負責在 Container Manager 中一鍵拉取輕量 Nginx 容器，對照外部 `8081` 連接埠並掛載目錄。 |
| 根目錄 `/my-web-server/` | **`default.conf`** | Nginx 設定檔 | **後端通道指揮官**：掌控底層精確路由。以雙層 `map` 分流下載與檢視，完美防禦 Nginx 經典的路徑疊加與 `if` 鎖死地雷。 |
| 子目錄 `/my-web-server/html/` | **`index.html`** | HTML5 / JS 原始碼 | **前端超級大腦**：採用 **DOM 節點記憶體動態建立法**，免除任何引號字元衝突地雷，掌管智慧解碼與前台視覺。 |
| 子目錄 `/my-web-server/html/` | **`files/`** | 空白資料夾 (可讀寫) | **您的私人小金庫**：專門存放您要分享的所有檔案（支援中文）。新增、刪除檔案免動程式碼，前台自動感應同步。 |

---

## 🛠️ 一鍵快速部署指南

### 1. 建立群暉本地資料夾
打開群暉 **File Station**，在 `docker` 共用資料夾下建立名為 `my-web-server` 的目錄，並依照上方的結構矩陣，在其底下建立 `html` 資料夾與 `html/files` 資料夾。

### 2. 配置後端設定檔 (`default.conf`)
在 `/docker/my-web-server/` 根目錄下建立 `default.conf`，並貼入 Nginx 雙分流規則代碼。

### 3. 配置前端網頁主程式 (`index.html`)
在 `/docker/my-web-server/html/` 目錄下建立 `index.html`，並貼入 DOM 動態節點建立法與智慧雙編碼解碼器代碼。

### 4. 透過群暉 Container Manager 啟動專案
建立 `/docker/my-web-server/docker-compose.yml` 檔案並貼入以下環境配置代碼：

```yaml
version: '3.8'

services:
  web-server:
    image: nginx:alpine
    container_name: lightweight-web-server
    ports:
      - "8081:80"
    volumes:
      - ./html:/usr/share/nginx/html:ro
      - ./default.conf:/etc/nginx/conf.d/default.conf:ro
    restart: always
```

進入群暉 **Container Manager** > **專案 (Project)** > **新增 (Create)**，選取該目錄並載入 `docker-compose.yml`，點擊完成，專案將在 3 秒內全速啟動。

---

## 🏁 終極雙通道操作行為矩陣

| 操作動作 | 檔案類型範例 | 畫面呈現行為 | 後台編碼與分流防禦機制 |
| :--- | :--- | :--- | :--- |
| 🖱️ **滑鼠左鍵點擊** | 純文字檔系列 (`.txt`, `.md`, `.log`) | **原網頁原地彈出**毛玻璃閱讀器 | 前端智慧 JavaScript TextDecoder（自動通吃 UTF-8 / Big5 繁體編碼） |
| 🖱️ **滑鼠左鍵點擊** | 多媒體與文件 (`.png`, `.jpg`, `.pdf`) | 在當前頁面直接線上開啟預覽 | 後端 Nginx Map 路由 `inline` 機制 |
| 🖱️ **滑鼠右鍵點擊** | **所有支援預覽之檔案** | **精準喚醒「在新分頁中開啟連結」**選單 | **全新 URL 路由重定向智慧捕捉技術（新分頁亦能啟動解碼核心）** |
| 🖱️ **不論左或右鍵** | 點擊藍色「下載」按鈕 | 100% 全速觸發瀏覽器另存新檔 | 後端 Nginx Map 路由 `attachment` 強制下載存檔機制 |

---
*Powered by Synology NAS Docker Environment & Nginx High-Performance Server.*
