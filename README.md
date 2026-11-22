# 專屬温成龍的幸福集點卡

奶油色系的雙人登入情侶集點網站。

## 功能
- 網站名稱：專屬温成龍的幸福集點卡
- 30 點解鎖「女朋友準備的神秘驚喜」
- 女朋友與温成龍各自使用 Email / Password 登入
- 只有女朋友帳號能加點、扣點、兌換
- 只有這兩個指定 UID 能讀取點數與紀錄
- 集點紀錄即時同步
- 新增 1、2、3 點；扣除 1、2 點；點數限制 0–30

## A. Firebase Authentication 建立兩個帳號
1. Firebase Console -> Authentication -> Sign-in method，啟用 Email/Password。
2. Authentication -> Users -> Add user，建立女朋友自己的 Email / 密碼。
3. 再新增温成龍自己的 Email / 密碼。
4. 在 Users 清單複製兩個帳號各自的 User UID，分別記下 ADMIN_UID（女朋友）和 PARTNER_UID（温成龍）。
5. 不要把密碼寫進網站檔案或分享給任何人。

## B. 設定 firebase-config.js
1. Firebase Console -> Project settings -> General -> Your apps -> SDK setup and configuration -> Config。
2. 將 `firebase-config.js` 裡的六個 YOUR_... 欄位替換成你的 Firebase Web App 設定值。
3. 把 `PASTE_ADMIN_USER_UID` 替換成女朋友的 User UID。
4. 把 `PASTE_PARTNER_USER_UID` 替換成温成龍的 User UID。
5. 儲存檔案。

## C. 設定 Firestore
1. Firebase Console -> Build -> Firestore Database -> Create database。
2. 建立完成後進入 Rules。
3. 將本資料夾 `firestore.rules` 的內容貼上。
4. 把兩處 `PASTE_ADMIN_USER_UID` 換成女朋友的 User UID；把 `PASTE_PARTNER_USER_UID` 換成温成龍的 User UID。
5. 按 Publish。

這份規則會限制只有這兩個 UID 能讀取資料，只有女朋友 UID 能新增或更改點數。請先替換 UID 再發布，否則兩位都無法讀取或操作。

## D. 用 iPhone 上傳到 GitHub
1. 解壓縮 ZIP。
2. 在 GitHub 開啟 `baby-couple-rewards` Repository。
3. 依序進入 Add file -> Upload files。
4. 上傳 `index.html`、`firebase-config.js`、`firestore.rules`、`README.md`。
5. 若同名檔案已存在，GitHub 會要求確認覆蓋；請確認後 Commit changes。

## E. 用 GitHub Pages 發布（不需要電腦）
1. GitHub Repository -> Settings -> Pages。
2. 在 Build and deployment 的 Source 選 `Deploy from a branch`。
3. Branch 選 `main`，資料夾選 `/(root)`，按 Save。
4. 等待部署完成，GitHub Pages 會顯示網站網址，格式通常是 `https://你的GitHub帳號.github.io/baby-couple-rewards/`。
5. 回 Firebase Console -> Authentication -> Settings -> Authorized domains，新增你的 GitHub Pages 網域（例如 `你的GitHub帳號.github.io`）。
6. 用兩位已建立的 Email / 密碼分別登入測試。

## 重要安全說明
- Firebase Web API key 是前端專案識別設定，不是管理者密碼；真正的資料保護依靠 Firebase Authentication 與 Firestore Rules。
- Repository 可設為 Public，因為網頁設定值會被瀏覽器讀取；不要把任何密碼、服務帳戶金鑰或私密金鑰上傳。
- 本網站沒有提供自行註冊功能；請只在 Firebase Authentication 手動建立這兩位使用者。
- 若日後要更換管理者或會員，必須同步更新 `firebase-config.js` 與 Firestore Rules。
