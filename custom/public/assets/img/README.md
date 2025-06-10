# 公司 LOGO 設置說明

## 如何添加公司 LOGO

1. 將你的公司 LOGO 文件重命名為 `company-logo.png`
2. 將文件放在這個目錄下 (`custom/public/assets/img/`)
3. 重啟 Gitea 容器即可看到效果

## LOGO 要求

- 文件格式：PNG、JPG、SVG 都支援
- 建議尺寸：寬度不超過 400px，高度不超過 120px
- 文件大小：建議不超過 1MB
- 背景：建議使用透明背景的 PNG 格式

## 注意事項

- LOGO 文件名必須是 `company-logo.png`
- 如果沒有 LOGO 文件，首頁會自動隱藏 LOGO 區域
- 修改後需要重啟 Gitea 容器才能看到變化

## 重啟容器命令

```bash
docker compose restart server
```

## 新的 Volume 掛載方式

現在使用 Docker Compose 的 volume 掛載，自定義文件放在容器外部：
- 模板文件：`./custom/templates/` 掛載到 `/data/gitea/templates`
- 靜態文件：`./custom/public/` 掛載到 `/data/gitea/public`

這樣的好處：
- ✅ 持久化修改，容器重建不會丟失
- ✅ 更新 Gitea 映像檔不會影響自定義內容
- ✅ 更容易管理和備份自定義文件 