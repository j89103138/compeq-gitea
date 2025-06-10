# Gitea + Drone CI 使用指南

## 系統概述

本系統整合了以下兩個主要組件：
- **Gitea**: 輕量級的 Git 服務器，提供代碼託管功能
- **Drone CI**: 持續整合/持續部署 (CI/CD) 平台

## 快速開始

1. 訪問服務：
- Gitea UI: http://localhost:3000
- Drone CI UI: http://localhost:8080

## 使用指南

### 1. Gitea 使用

1. 登入 Gitea
   - 使用您的帳戶登入
   - 如果是首次使用，請聯繫管理員創建帳戶

2. 創建倉庫
   - 點擊右上角 "+" 按鈕
   - 選擇 "New Repository"
   - 填寫倉庫名稱和描述
   - 選擇是否公開
   - 點擊 "Create Repository"

3. 推送代碼

#### 基本 Git 操作流程

1. **clone repo**
```bash
# 從 Gitea 克隆倉庫到本地
git clone http://localhost:3000/your-username/your-repo.git

# 進入專案目錄
cd your-repo
```

2. **創建並切換到新分支**
```bash
# 創建並切換到新分支
git checkout -b feature/new-feature

# 查看當前分支
git branch
```

3. **修改代碼並提交**
```bash
# 查看修改的文件
git status

# 添加修改的文件到暫存區
git add .                    # 添加所有修改
# 或
git add specific-file.txt    # 添加特定文件

# 提交修改
git commit -m "描述你的更改"
```

4. **同步遠程倉庫**
```bash
# 拉取遠程更新
git pull origin main

# 推送到遠程倉庫
git push origin feature/new-feature
```

#### 進階 Git 操作

1. **查看提交歷史**
```bash
# 查看提交歷史
git log

# 查看簡潔的提交歷史
git log --oneline

# 查看特定文件的修改歷史
git log -p filename
```

2. **分支操作**
```bash
# 分支命名規範
# feature/* - 新功能開發分支
# hotfix/* - 緊急修復分支
# bugfix/* - 一般錯誤修復分支
# release/* - 發布分支
# 例如：
#   feature/user-login    - 用戶登入功能
#   hotfix/payment-error  - 支付錯誤修復
#   bugfix/typo-fix      - 文字錯誤修復
#   release/v1.0.0       - 1.0.0 版本發布

# 創建新分支
git branch feature/new-feature    # 創建新分支但不切換
git checkout -b feature/new-feature  # 創建並切換到新分支

# 從特定分支創建新分支
git checkout -b feature/new-feature origin/main  # 從遠程 main 分支創建
git checkout -b hotfix/bug-fix main  # 從本地 main 分支創建

# 列出所有分支
git branch -a

# 切換分支
git checkout main

# 合併分支
git merge feature/new-feature

# 刪除分支
git branch -d feature/new-feature  # 安全刪除（如果分支未合併會提示）
git branch -D feature/new-feature  # 強制刪除
```

3. **暫存和恢復**
```bash
# 暫存當前修改
git stash

# 查看暫存列表
git stash list

# 恢復暫存的修改
git stash pop
```

4. **解決衝突**
```bash
# 當發生衝突時，Git 會在文件中標記衝突
# 手動解決衝突後：
git add .
git commit -m "解決衝突"
```

#### 常用 Git 配置

1. **設置用戶信息**
```bash
# 設置全局用戶名和郵箱
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# 設置當前倉庫的用戶名和郵箱
git config user.name "Your Name"
git config user.email "your.email@example.com"
```

2. **設置默認編輯器**
```bash
# 設置默認編輯器為 VS Code
git config --global core.editor "code --wait"
```

3. **設置默認分支**
```bash
# 設置默認分支為 main
git config --global init.defaultBranch main
```

4. **設置遠程倉庫**
```bash
# 查看當前遠程倉庫
git remote -v

# 添加遠程倉庫
git remote add origin http://localhost:3000/your-username/your-repo.git

# 修改遠程倉庫地址
git remote set-url origin http://localhost:3000/your-username/your-repo.git

# 刪除遠程倉庫
git remote remove origin

# 添加多個遠程倉庫
git remote add upstream http://localhost:3000/upstream/repo.git
git remote add staging http://localhost:3000/staging/repo.git

# 推送到特定遠程倉庫
git push origin main
git push staging develop
1. **提交信息規範**
- 使用清晰的提交信息
- 遵循 Conventional Commits 規範
- 例如：
  - `feat: 添加新功能`
  - `fix: 修復某個問題`
  - `docs: 更新文檔`
  - `style: 代碼格式修改`
  - `refactor: 代碼重構`

2. **分支管理策略**
- `main`: 主分支，保持穩定
- `develop`: 開發分支
- `feature/*`: 功能分支
- `hotfix/*`: 緊急修復分支
- `release/*`: 發布分支

3. **代碼審查流程**
- 創建 Pull Request
- 等待審查者審核
- 根據反饋修改代碼
- 通過審核後合併

4. **定期同步主分支**
```bash
# 切換到主分支
git checkout main

# 拉取最新代碼
git pull origin main

# 切換回功能分支
git checkout feature/new-feature

# 合併主分支的更新
git merge main
```

### 2. Drone CI 使用

1. 登入 Drone
   - 使用 Gitea 帳戶登入
   - 首次登入需要授權 Drone 訪問倉庫

2. 查看構建結果
   - 在 Drone UI 中查看構建狀態
   - 點擊構建查看詳細日誌
   - 查看構建產物

## 故障排除

### 常見問題

1. **無法訪問 Gitea**
   - 確認服務是否正常運行
   - 檢查網絡連接

2. **Drone 構建失敗**
   - 檢查 `.drone.yml` 配置
   - 查看構建日誌
   - 確認環境變數設置

3. **Git 操作問題**
   - 確認認證信息
   - 檢查分支權限
   - 確認倉庫狀態

### 查看日誌

```bash
# 查看 Gitea 日誌
docker compose logs server

# 查看 Drone Server 日誌
docker compose logs drone-server

# 查看 Drone Runner 日誌
docker compose logs drone-runner
```

## 安全建議

1. 使用強密碼
2. 定期更新代碼
3. 不要分享敏感信息
4. 使用 SSH 密鑰認證
5. 定期備份重要數據

## 完整使用流程範例

以下是一個完整的使用流程範例，展示如何從創建倉庫到完成 CI/CD 流程：

### 1. 創建新專案

1. **登入 Gitea 並創建倉庫**
   - 訪問 http://localhost:3000
   - 點擊右上角 "+" 按鈕
   - 創建名為 "my-project" 的新倉庫

2. **初始化本地專案**
```bash
# 克隆倉庫
git clone http://localhost:3000/your-username/my-project.git
cd my-project

# 創建基本專案結構
mkdir src
touch src/main.py
touch README.md
```

3. **添加初始代碼**
```python
# src/main.py
def hello():
    return "Hello, World!"

if __name__ == "__main__":
    print(hello())
```

4. **提交初始代碼**
```bash
git add .
git commit -m "feat: 初始化專案結構"
git push origin main
```

### 2. 設置 CI/CD

1. **創建 `.drone.yml` 文件**
```yaml
kind: pipeline
type: docker
name: default

steps:
- name: test
  image: python:3.9
  commands:
  - pip install pytest
  - pytest tests/

- name: build
  image: python:3.9
  commands:
  - python src/main.py
  when:
    branch: main
```

2. **提交 CI 配置**
```bash
git add .drone.yml
git commit -m "ci: 添加 Drone CI 配置"
git push origin main
```

### 3. 開發新功能

1. **創建功能分支**
```bash
git checkout -b feature/add-tests
```

2. **添加測試文件**
```python
# tests/test_main.py
from src.main import hello

def test_hello():
    assert hello() == "Hello, World!"
```

3. **提交測試代碼**
```bash
git add tests/
git commit -m "test: 添加單元測試"
git push origin feature/add-tests
```

### 4. 代碼審查和合併

1. **創建 Pull Request**
   - 在 Gitea 界面中創建 PR
   - 填寫 PR 描述
   - 等待審查

2. **合併到主分支**
   - 通過審查後合併 PR
   - 刪除功能分支

### 5. 查看 CI 結果

1. **訪問 Drone UI**
   - 打開 http://localhost:8080
   - 查看構建狀態和日誌

2. **確認構建成功**
   - 檢查測試結果
   - 查看構建日誌
   - 確認部署狀態

### 6. 維護和更新

1. **定期同步主分支**
```bash
git checkout main
git pull origin main
```

2. **更新依賴**
```bash
# 更新 requirements.txt
pip freeze > requirements.txt
git add requirements.txt
git commit -m "chore: 更新依賴"
git push origin main
```

這個範例展示了一個完整的開發流程，從專案初始化到 CI/CD 配置，再到功能開發和代碼審查。每個步驟都遵循了最佳實踐，確保代碼質量和團隊協作效率。

## 支援

如有問題，請聯繫系統管理員或提交 Issue。 