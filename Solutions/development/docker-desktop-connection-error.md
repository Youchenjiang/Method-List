# Docker Desktop 連接錯誤解決方案

## 問題描述

在執行 Docker 命令時出現以下錯誤：
![image](https://github.com/user-attachments/assets/de03fed7-681f-422d-89d3-8a22c431a269)
```
docker pull node:18-alpine
error during connect: Post "http://%2F%2F.%2Fpipe%2FdockerDesktopLinuxEngine/v1.50/images/create?fromImage=docker.io%2Flibrary%2Fnode&tag=18-alpine": open //./pipe/dockerDesktopLinuxEngine: The system cannot find the file specified.
```

## 錯誤原因

這個錯誤表示 Docker CLI 無法連接到 Docker Desktop 的後端引擎。常見原因包括：

1. Docker Desktop 未啟動
2. Docker Desktop 服務未正常運行
3. Docker Desktop 需要重新啟動
4. 系統權限問題

## 解決方法

### 方法 1：啟動 Docker Desktop

1. 開啟 Docker Desktop 應用程式
2. 等待 Docker Desktop 完全啟動（系統托盤圖示會顯示綠色）
3. 確認 Docker Desktop 狀態為 "Running"
4. 重新執行 Docker 命令

### 方法 2：重新啟動 Docker Desktop

1. 關閉 Docker Desktop
2. 完全結束所有 Docker 相關程序
3. 以系統管理員身份重新啟動 Docker Desktop
4. 等待服務完全啟動後重試

### 方法 3：重啟 Docker 服務（Windows）

在 PowerShell（以系統管理員身份執行）中執行：

```powershell
# 停止 Docker Desktop Service
Stop-Service -Name com.docker.service -Force

# 啟動 Docker Desktop Service
Start-Service -Name com.docker.service

# 檢查服務狀態
Get-Service -Name com.docker.service
```

### 方法 4：檢查 WSL 2 狀態（如果使用 WSL 2 後端）

```powershell
# 檢查 WSL 狀態
wsl --list --verbose

# 重啟 WSL
wsl --shutdown

# 重新啟動 Docker Desktop
```

### 方法 5：重新安裝 Docker Desktop

如果以上方法都無效：

1. 完全卸載 Docker Desktop
2. 清除 Docker 相關資料夾：
   - `C:\Program Files\Docker`
   - `C:\ProgramData\Docker`
   - `%APPDATA%\Docker`
3. 重新安裝最新版本的 Docker Desktop
4. 重新配置設定

## 驗證解決方案

執行以下命令確認 Docker 正常運行：

```bash
# 檢查 Docker 版本
docker --version

# 檢查 Docker 狀態
docker info

# 測試拉取映像
docker pull hello-world
docker run hello-world
```

## 參考連結

- [Docker Desktop 官方文件](https://docs.docker.com/desktop/)
- [Docker Desktop Windows 疑難排解](https://docs.docker.com/desktop/troubleshoot/overview/)
