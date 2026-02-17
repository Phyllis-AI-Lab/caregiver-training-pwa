# 外籍看護培訓助手 PWA
# Caregiver Training Assistant PWA

專為外籍看護設計的多語言培訓與工作管理系統  
Multilingual training and work management system for foreign caregivers

## 功能特色 Features

### ✅ 核心功能
1. **多語言支援 Multilingual Support**
   - 印尼語（Bahasa Indonesia）- 主要
   - 越南語（Tiếng Việt）
   - 泰語（ภาษาไทย）
   - 菲律賓語（Filipino）
   - 繁體中文
   - English

2. **即時翻譯 Real-time Translation**
   - Google Cloud Translation API 整合
   - 語音輸入支援
   - 常用語句快速翻譯
   - 離線常用語句快取

3. **工作排程系統 Work Schedule System**
   - 早中晚時段分類
   - 自訂工作項目
   - 鬧鐘提醒功能
   - 工作完成追蹤

4. **照顧技能培訓 Care Skills Training**
   - 個人衛生照護
   - 飲食照護
   - 活動輔助
   - 生理監測
   - 緊急處理指南

5. **PWA 功能 PWA Features**
   - 離線可用
   - 可安裝到手機
   - 推送通知
   - 背景同步

## 安裝說明 Installation

### 方法 1：本地測試 Local Testing

```bash
# 1. 進入專案目錄
cd caregiver-training-pwa

# 2. 啟動本地伺服器 (選擇一種)

# 使用 Python
python -m http.server 8080

# 或使用 Node.js http-server
npx http-server -p 8080

# 或使用 PHP
php -S localhost:8080

# 3. 開啟瀏覽器
# 訪問 http://localhost:8080
```

### 方法 2：部署到線上 Deploy Online

#### GitHub Pages
```bash
# 1. 上傳到 GitHub repository
git init
git add .
git commit -m "Initial commit"
git remote add origin YOUR_REPO_URL
git push -u origin main

# 2. 在 GitHub repo 設定中啟用 GitHub Pages
# Settings → Pages → Source: main branch
```

#### Vercel
```bash
# 1. 安裝 Vercel CLI
npm i -g vercel

# 2. 部署
vercel --prod
```

#### Firebase Hosting
```bash
# 1. 安裝 Firebase CLI
npm install -g firebase-tools

# 2. 初始化
firebase login
firebase init hosting

# 3. 部署
firebase deploy --only hosting
```

## Google Translation API 設定

**重要：** 此應用使用 Google Cloud Translation API

### 選項 1：使用免費額度（推薦）

1. 前往 [Google Cloud Console](https://console.cloud.google.com)
2. 建立新專案或選擇現有專案
3. 啟用 Cloud Translation API
4. 建立 API 金鑰：
   - APIs & Services → Credentials → Create Credentials → API Key
5. 限制 API 金鑰（安全性）：
   - Application restrictions: HTTP referrers
   - 新增你的網站 URL
   - API restrictions: Cloud Translation API

6. 將 API 金鑰加入 `js/translator.js`:
```javascript
const GOOGLE_TRANSLATE_API_KEY = 'YOUR_API_KEY_HERE';
```

**免費額度：** 每月前 500,000 字元免費

### 選項 2：使用模擬翻譯（測試用）

如果不想設定 API，應用會使用內建的模擬翻譯功能（常用語句）。

## 使用說明 Usage Guide

### 1. 工作排程 Schedule

- 點擊「+ 新增工作」建立新的工作項目
- 設定工作名稱、時間、時段
- 啟用鬧鐘提醒
- 完成工作時勾選核取方塊

### 2. 即時翻譯 Translation

- 選擇來源語言和目標語言
- 輸入文字或使用語音輸入
- 點擊常用語句快速翻譯
- 朗讀翻譯結果
- 複製翻譯文字

### 3. 培訓課程 Training

- 瀏覽不同照顧技能類別
- 學習圖文並茂的教學內容
- 觀看示範影片
- 查看操作步驟

### 4. 緊急處理 Emergency

- 查看各種緊急情況處理指南
- 跌倒、嗆咳、低血糖等
- 步驟化的處理流程
- 緊急聯絡資訊

## 檔案結構 File Structure

```
caregiver-training-pwa/
├── index.html              # 主頁面
├── manifest.json           # PWA 設定
├── sw.js                   # Service Worker
├── offline.html            # 離線頁面
├── README.md               # 本文件
├── css/
│   └── styles.css          # 樣式表
├── js/
│   ├── app.js              # 主應用程式邏輯
│   ├── i18n.js             # 多語言系統
│   ├── db.js               # 本地資料庫 (IndexedDB)
│   ├── translator.js       # 翻譯功能
│   ├── scheduler.js        # 排程與鬧鐘
│   └── training.js         # 培訓內容
├── images/
│   └── icons/              # 應用程式圖示
└── data/
    ├── translations.json   # 翻譯資料
    ├── training.json       # 培訓內容
    └── common-phrases.json # 常用語句
```

## 瀏覽器支援 Browser Support

- ✅ Chrome 80+ (推薦)
- ✅ Safari 14+ (iOS 14.3+)
- ✅ Firefox 78+
- ✅ Edge 80+

## 進階功能 Advanced Features

### 推送通知 Push Notifications

若要啟用推送通知，需設定 Firebase Cloud Messaging:

1. 建立 Firebase 專案
2. 啟用 Cloud Messaging
3. 取得 VAPID 金鑰
4. 更新 `sw.js` 和相關設定

詳見 [Firebase 設定指南](https://firebase.google.com/docs/cloud-messaging/js/client)

### 資料備份 Data Backup

所有資料儲存在瀏覽器的 IndexedDB：
- 工作排程
- 翻譯歷史
- 學習進度

建議定期匯出資料備份。

## 故障排除 Troubleshooting

### Q: PWA 無法安裝？
A: 確認：
- 使用 HTTPS（或 localhost）
- 有效的 manifest.json
- Service Worker 已註冊
- 圖示檔案存在

### Q: 翻譯功能不work？
A: 檢查：
- API 金鑰是否正確
- 網路連線
- API 配額是否用完
- 瀏覽器 Console 的錯誤訊息

### Q: 鬧鐘不響？
A: 確認：
- 已授予通知權限
- 瀏覽器未關閉
- 系統勿擾模式未開啟

### Q: 離線功能無效？
A: 檢查：
- Service Worker 是否成功註冊
- 快取是否建立
- Chrome DevTools → Application → Service Workers

## 開發指南 Development Guide

### 新增語言

1. 編輯 `js/i18n.js`
2. 新增語言翻譯
3. 更新語言選擇器

### 新增培訓內容

1. 編輯 `data/training.json`
2. 新增類別和課程
3. 準備圖片和影片素材

### 自訂工作模板

1. 編輯 `data/task-templates.json`
2. 定義預設工作項目
3. 設定建議時間

## 授權 License

MIT License

## 貢獻 Contributing

歡迎提交 Issue 和 Pull Request！

## 聯絡 Contact

如有問題或建議，請開 Issue 討論。

---

**版本 Version:** 1.0.0  
**最後更新 Last Updated:** 2026-02-17  
**作者 Author:** Built with Claude (Anthropic)
