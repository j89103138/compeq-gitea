# Gitea 首頁自定義指南

## 快速開始

1. **啟動容器**：雙擊 `start-gitea.bat`
2. **停止容器**：雙擊 `stop-gitea.bat`
3. **添加 LOGO**：將公司 LOGO 放到 `custom/public/assets/img/company-logo.png`
4. **重啟服務**：執行 `docker compose restart server`

## 文件結構（新的 Volume 掛載方式）

```
gitea-docker-new/
├── start-gitea.bat              # 啟動腳本
├── stop-gitea.bat               # 停止腳本
├── docker-compose.yml           # Docker 配置（已更新 volume 掛載）
├── gitea/                       # Gitea 資料目錄
└── custom/                      # 自定義文件目錄（容器外部）
    ├── templates/               # 模板文件 (掛載到 /data/gitea/templates)
    │   ├── home.tmpl           # 自定義首頁模板
    │   └── custom/
    │       └── header.tmpl     # 自定義頁頭
    └── public/                 # 靜態文件 (掛載到 /data/gitea/public)
        └── assets/
            ├── css/
            │   └── custom.css  # 自定義樣式
            └── img/
                ├── company-logo.png    # 公司 LOGO（需要你添加）
                └── README.md           # LOGO 使用說明
```

## 自定義內容

### 1. 修改公司資訊

編輯 `custom/templates/home.tmpl` 文件：

```html
<!-- 修改公司名稱 -->
<h1 class="ui header">歡迎來到【你的公司名稱】代碼管理平台</h1>

<!-- 修改公司簡介 -->
<div class="ui large text">
    <p>這裡是【你的公司名稱】的內部 Git 代碼倉庫管理系統</p>
    <p>【你的公司標語或描述】</p>
</div>

<!-- 修改聯絡資訊 -->
<p>
    📧 Email: <a href="mailto:你的郵箱">你的郵箱</a>
    <br>
    📞 內線: 你的電話
</p>
```

### 2. 添加公司 LOGO

1. 準備你的公司 LOGO 文件（建議 PNG 格式，透明背景）
2. 重命名為 `company-logo.png`
3. 放到 `custom/public/assets/img/` 目錄下
4. 重啟容器：`docker compose restart server`

### 3. 自定義樣式

編輯 `custom/public/assets/css/custom.css` 來修改：

- 顏色主題
- 字體大小
- 背景圖案
- 動畫效果

### 4. 修改功能介紹

在 `home.tmpl` 中找到功能介紹區域，可以修改：

- 功能圖標（使用 Semantic UI 圖標）
- 功能標題
- 功能描述

## 常見問題

### Q: 修改後看不到變化？
A: 確保已重啟 Gitea 容器：`docker compose restart server`

### Q: LOGO 不顯示？
A: 檢查文件名是否為 `company-logo.png`，路徑是否正確

### Q: 想恢復原始首頁？
A: 刪除或重命名 `custom/templates/home.tmpl` 文件

### Q: 如何修改其他頁面？
A: 參考官方文檔的模板覆蓋說明，將對應模板放到 `custom/templates/` 目錄

## 技術支援

如需進一步自定義，可以：

1. 查閱 [Gitea 官方文檔](https://docs.gitea.io/en-us/customizing-gitea/)
2. 參考 `customization.md` 文件
3. 聯絡技術團隊

## 備份建議

定期備份 `custom/` 目錄，以防意外丟失自定義設置。

## Volume 掛載的優勢

使用新的 volume 掛載方式有以下優勢：

✅ **持久化修改**：自定義文件放在容器外部，容器重建不會丟失
✅ **版本升級安全**：更新 Gitea 映像檔不會影響自定義內容  
✅ **管理便利**：直接在宿主機上編輯文件，立即生效
✅ **備份簡單**：只需備份 `custom/` 目錄即可
✅ **開發友好**：可以使用版本控制管理自定義文件 