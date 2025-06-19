# 📖 Compeq Git Server 使用說明

## 🚀 快速開始

歡迎使用華通電腦Z部門的 Git 程式碼倉庫管理系統！本指南將幫助您快速上手。

## 🔐 登入系統

### 首次登入
1. 訪問 [http://10.1.230.110:3000](http://10.1.230.110:3000)
2. 點擊右上角 **「登入」** 按鈕
3. 使用您的帳號密碼登入
4. 如需註冊新帳號，請聯絡系統管理員

### 忘記密碼
如果忘記密碼，請聯絡系統管理員重置：
- 📧 Email: shawnliu@compeq.com.tw

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
- ✅ 使用小寫英文字母
- ✅ 使用連字符 `-` 分隔單詞
- ✅ 避免使用特殊字符
- 📝 範例：`project-name`、`web-frontend`、`api-server`

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

# 5. 在網頁上建立 Pull Request
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
1. **Fork 或建立分支**
   ```bash
   git checkout -b feature/your-feature
   ```

2. **開發並提交**
   ```bash
   git add .
   git commit -m "feat: 描述你的修改"
   git push origin feature/your-feature
   ```

3. **建立 Pull Request**
   - 在 Gitea 網頁上點擊 **「New Pull Request」**
   - 填寫 PR 標題和描述
   - 指定審查者
   - 提交 PR

4. **代碼審查**
   - 審查者會檢查代碼
   - 根據回饋進行修改
   - 通過審查後合併

### 提交訊息規範
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

## 🏢 組織管理

### 建立組織
1. 點擊右上角 **「+」** 按鈕
2. 選擇 **「新建組織」**
3. 填寫組織資訊
4. 設定組織可見性

### 組織權限
- **Owner**：完全控制權限
- **Admin**：管理權限，不能刪除組織
- **Write**：讀寫權限
- **Read**：只讀權限

## 🔧 專案管理

### Issue 管理
1. **建立 Issue**
   - 點擊 **「Issues」** 頁籤
   - 點擊 **「New Issue」**
   - 填寫標題和描述
   - 指定標籤和負責人

2. **Issue 狀態**
   - **Open**：待處理
   - **Closed**：已完成或已取消

### 里程碑管理
1. 在倉庫中點擊 **「Issues」**
2. 點擊 **「Milestones」**
3. 建立新里程碑並設定截止日期
4. 將 Issues 分配到對應里程碑

## 📊 CI/CD 整合

本系統整合了 Drone CI，支援自動化構建和部署。

### 配置 CI/CD
1. 在倉庫根目錄建立 `.drone.yml` 文件
2. 配置構建步驟：
   ```yaml
   kind: pipeline
   type: docker
   name: default
   
   steps:
   - name: test
     image: node:16
     commands:
     - npm install
     - npm test
   
   - name: build
     image: node:16
     commands:
     - npm run build
   ```

3. 推送代碼後自動觸發 CI/CD

### 查看構建狀態
- 在倉庫頁面查看構建徽章
- 點擊徽章查看詳細構建日誌
- Drone CI 控制台：[http://10.1.230.110:8080](http://10.1.230.110:8080)

## 🛡️ 安全最佳實踐

### 密碼安全
- ✅ 使用強密碼（至少 8 位，包含大小寫字母、數字、特殊字符）
- ✅ 定期更改密碼
- ✅ 不要在代碼中硬編碼密碼
- ✅ 使用環境變數存儲敏感資訊

### 存取控制
- ✅ 遵循最小權限原則
- ✅ 定期檢查倉庫權限
- ✅ 及時移除離職人員的存取權限
- ✅ 使用組織管理大型團隊

### 代碼安全
- ✅ 不要提交敏感資訊（密碼、API 金鑰等）
- ✅ 使用 `.gitignore` 忽略敏感文件
- ✅ 定期更新依賴套件
- ✅ 啟用分支保護規則

## 📚 進階功能

### Webhook
1. 進入倉庫設定
2. 選擇 **「Webhooks」**
3. 添加 Webhook URL
4. 配置觸發事件

### API 使用
Gitea 提供完整的 REST API：
```bash
# 獲取倉庫資訊
curl -H "Authorization: token YOUR_TOKEN" \
     http://10.1.230.110:3000/api/v1/repos/username/repo
```

### 自訂 Git Hooks
可以在倉庫中配置 Git Hooks 來自動化工作流程。

## ❓ 常見問題

### Q: 無法推送代碼？
**A:** 檢查以下項目：
1. 確認有推送權限
2. 檢查分支保護規則
3. 驗證 SSH 金鑰配置
4. 確認沒有大檔案（>100MB）

### Q: 忘記密碼怎麼辦？
**A:** 聯絡系統管理員：shawnliu@compeq.com.tw

### Q: 如何刪除倉庫？
**A:** 
1. 進入倉庫設定
2. 滾動到最下方
3. 點擊 **「刪除此倉庫」**
4. 輸入倉庫名稱確認

### Q: 如何修改提交歷史？
**A:** 
```bash
# 修改最後一次提交
git commit --amend

# 互動式重寫歷史
git rebase -i HEAD~3
```

### Q: 大檔案如何處理？
**A:** 使用 Git LFS：
```bash
# 安裝 Git LFS
git lfs install

# 追蹤大檔案
git lfs track "*.psd"
git add .gitattributes
```

## 🆘 技術支援

### 聯絡資訊
- 📧 **Email**: shawnliu@compeq.com.tw
- 🏢 **部門**: 華通電腦Z部門
- ⏰ **支援時間**: 週一至週五 09:00-18:00

### 常用資源
- 🔗 [Git 官方文檔](https://git-scm.com/docs)
- 🔗 [Gitea 官方文檔](https://docs.gitea.io/)
- 🔗 [Drone CI 文檔](https://docs.drone.io/)
- 🔗 [Markdown 語法](https://www.markdownguide.org/)

### 回報問題
如果遇到技術問題，請提供：
1. 問題描述和重現步驟
2. 錯誤訊息截圖
3. 作業系統和瀏覽器版本
4. Git 客戶端版本

---

**💡 提示：**此文檔會定期更新，請關注最新版本。如有建議或問題，歡迎回饋給系統管理員。 