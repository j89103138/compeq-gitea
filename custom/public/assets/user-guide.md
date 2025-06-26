# 📖 Compeq Git Server 使用說明

---

**🏢 華通電腦 Z部門 Git 程式碼倉庫管理系統**
📧 支援：[shawnliu@compeq.com.tw](mailto:shawnliu@compeq.com.tw)
🌐 系統地址：[http://10.1.230.110:3000](http://10.1.230.110:3000)

---

## 📋 目錄

- [🔐 登入系統](#登入系統)
- [📁 建立倉庫](#建立倉庫)
- [💻 VSCode UI 操作指南](#vscode-ui-操作指南)
- [🌿 Git 基本操作](#git-基本操作)
- [🔑 SSH 金鑰配置](#ssh-金鑰配置)
- [👥 團隊協作](#團隊協作)
- [📊 CI/CD 整合](#cicd-整合)
- [❓ 常見問題](#常見問題)

🔄 此教學文檔會持續更新，有相關問題歡迎指教。

## 🔐 登入系統

### 首次登入

1. 訪問 [http://10.1.230.110:3000](http://10.1.230.110:3000)
2. 點擊右上角 **「登入」** 按鈕
3. 使用您的帳號(不是email) & 密碼登入
4. 尚未註冊帳號的請直接登入AD帳號

## 📁 建立倉庫

### 建立新倉庫

1. 登入後點擊右上角 **「+」** 按鈕
2. 選擇 **「新建倉庫」**
3. 填寫倉庫資訊：
   - **倉庫名稱**：使用小寫英文和連字符
   - **描述**：簡短描述專案用途
   - **可見性**：選擇公開或私有
4. 點擊 **「建立倉庫」**

### 倉庫命名規範

> ✅ **最佳實踐**
> - 使用小寫英文字母
> - 使用連字符 `-` 分隔單詞
> - 避免使用特殊字符
> - 📝 範例：`project-name`、`web-frontend`、`api-server`

## 💻 VSCode UI 操作指南

對於不熟悉命令列操作的使用者，VSCode 提供了直觀的圖形化界面來進行 Git 操作。以下是使用 VSCode UI 進行常見 Git 操作的步驟說明。

### 📝 提交變更 (Add & Commit)

當您修改了檔案後，可以透過 VSCode 的 Source Control 面板輕鬆提交變更：

> 💡 **操作步驟：**
> 1. 點擊左側活動列的 **Source Control** 圖示（或按 `Ctrl+Shift+G`）
> 2. 在 **Changes** 區域中，您會看到所有修改過的檔案
> 3. 點擊檔案旁的 **「+」** 按鈕將檔案加入暫存區（Stage）
> 4. 或點擊 **Changes** 標題旁的 **「+」** 按鈕一次暫存所有變更
> 5. 在上方的訊息框中輸入提交訊息
> 6. 點擊 **「✓ Commit」** 按鈕完成提交

![VSCode Add & Commit 操作示意圖](img/add-commit.png)
*▲ VSCode Source Control 面板中的 Add & Commit 操作*

### 🚀 推送到遠端倉庫 (Push)

提交變更後，需要將本地的提交推送到遠端倉庫：

> 💡 **操作步驟：**
> 1. 完成 Commit 後，您會在 Source Control 面板看到待推送的提交
> 2. 點擊 **「Sync Changes」** 按鈕（雲朵圖示）
> 3. 或點擊 **「Push」** 按鈕（向上箭頭圖示）
> 4. 如果是第一次推送新分支，VSCode 會詢問是否要發布分支到遠端
> 5. 確認後，變更就會推送到 Gitea 伺服器

![VSCode Push 操作示意圖](img/push.png)
*▲ VSCode 中的 Push 操作按鈕位置*

### 🔄 其他常用 UI 操作

> ✅ **實用功能**
> - **檢視變更**：點擊檔案名稱可以查看具體的變更內容
> - **撤銷變更**：點擊檔案旁的 **「↶」** 按鈕可以撤銷未暫存的變更
> - **分支切換**：點擊左下角的分支名稱可以切換或建立新分支
> - **拉取更新**：點擊 **「Pull」** 按鈕（向下箭頭）可以拉取遠端的最新變更
> - **查看歷史**：使用 `Ctrl+Shift+P` 開啟命令面板，搜尋 "Git: View History" 查看提交歷史

> ⚠️ **注意事項：**
> - 首次使用時，VSCode 可能會要求您設定 Git 使用者名稱和電子郵件
> - 如果遇到認證問題，請確認已正確設定 Git 認證或 SSH 金鑰
> - 建議在推送前先拉取最新的遠端變更，避免衝突
> - 對於重要的變更，建議透過 Pull Request 流程進行程式碼審查

## 🌿 Git 基本操作

### 克隆倉庫

```bash
# HTTPS 方式 (推薦)
git clone http://10.1.230.110:3000/username/repo-name.git

# SSH 方式
git clone git@10.1.230.110:2222:username/repo-name.git
```

### 基本工作流程

```bash
# 1. 克隆倉庫
git clone <倉庫地址>
cd <倉庫名稱>

# 2. 建立分支
git checkout -b feature/new-feature

# 3. 修改代碼後提交
git add .
git commit -m "feat: 添加新功能"

# 4. 推送到遠端
git push origin feature/new-feature

# 5. 在網頁上建立 Pull Request (合併請求)
```

## 🔑 SSH 金鑰配置

### 生成 SSH 金鑰
```bash
# 生成新的 SSH 金鑰
ssh-keygen -t ed25519 -C "your.email@compeq.com.tw"

# 查看公鑰內容
cat ~/.ssh/id_ed25519.pub
```

### 添加 SSH 金鑰到 Gitea
1. 登入 Gitea 後點擊右上角頭像
2. 選擇 **「設定」**
3. 左側選單選擇 **「SSH / GPG 金鑰」**
4. 點擊 **「增加金鑰」**
5. 貼上公鑰內容並設定名稱
6. 點擊 **「增加金鑰」**

### 測試 SSH 連線
```bash
# 測試 SSH 連線（注意是 2222 埠）
ssh -T git@10.1.230.110 -p 2222
```

## 👥 團隊協作

### Pull Request 流程

1. **建立分支**
   ```bash
   git checkout -b feature/your-feature
   ```

2. **開發並提交 (不建議 push 到 main 分支)**
   ```bash
   git add .
   git commit -m "描述你的修改"
   git push origin feature/your-feature
   ```

3. **建立 Pull Request (合併請求, 建議使用這個來推上main分支)**
   - 在 Gitea 網頁上點擊 **「New Pull Request」**
   - 填寫 PR 標題和描述
   - 指定審查者
   - 提交 PR
   - *請注意 請先設置倉庫PR的規則rules，例如誰可以核可? 需要幾位人員核可?

### 提交訊息規範 (僅供參考~)

```bash
# 格式：<類型>: <描述>
feat: 添加用戶登入功能
fix: 修復登出時的記憶體洩露
docs: 更新 API 文檔
style: 修正代碼格式
refactor: 重構用戶服務模組
test: 添加單元測試
chore: 更新依賴套件
```

## 📊 CI/CD 整合

本系統CICD流程使用流行的Github Actions 的本地版本，支援自動化 Build 和部署。

### 配置 CI/CD

1. 在倉庫根目錄建立 `.gitea/workflows/name.yaml` 文件
2. 配置構建步驟 (範例)：
   ```yaml
   name: Run CI on test_branch

   on:
     push:
       branches:
         - test_branch

   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - name: Check out code
           uses: actions/checkout@v4

         - name: Run a test script
           run: echo "✅ Running on test_branch!"
   ```
3. 推送代碼(git push or PR merge)後自動觸發 CI/CD

### 查看構建狀態

- 在倉庫頁面點擊上方 Actions 分頁
- 查看詳細 CICD 日誌

## ❓ 常見問題

### Q: 無法推送代碼？ 如遇到 fatal: Authentication failed

> ⚠️ **解決方案：** 檢查以下項目：
> - 很多時候直接push第二次，就可以解決 Auth 問題
> - 確認有推送權限
> - 檢查分支保護規則
> - 驗證 SSH 金鑰配置
> - 確認沒有大檔案（>100MB）

### Q: 忘記密碼怎麼辦？

> 💡 **答案：** 這是AD帳號與AD密碼，請聯絡公司AD密碼重設管理員

### Q: 如何刪除倉庫？

> ⚠️ **操作步驟：**
> 1. 進入倉庫設定
> 2. 滾動到最下方
> 3. 點擊 **「刪除此倉庫」**
> 4. 輸入倉庫名稱確認

### Q: 大檔案如何處理？

> 💡 **使用 Git LFS：**
> ```bash
> # 安裝 Git LFS
> git lfs install
>
> # 追蹤大檔案
> git lfs track "*.psd"
> git add .gitattributes
> ```

## 🆘 技術支援

---

### 聯絡資訊

📧 **Email**: [shawnliu@compeq.com.tw](mailto:shawnliu@compeq.com.tw)

[🌐 返回 Git 系統](http://10.1.230.110:3000)

---

**💡 提示：** 此文檔會定期更新。如有建議或問題，歡迎回饋給管理員。