# 工程教學入口 · Engineering Academy

純靜態、零相依套件的互動式教學網站,可直接託管。結構是「**入口頁 + 三個子頁**」:

| 檔案 | 內容 |
|---|---|
| `index.html` | 入口頁,三個選項:示波器操作原理 / FLH Interface / NAND Flash 元件養成 |
| `scope.html` | 示波器操作原理(泰克 × Keysight,Flash / SSD 量測導向) |
| `flash_interface.html` | FLH Device Engineering 養成手冊(介面 / 操作面,新人 → Senior) |
| `flash_device.html` | NAND Flash 元件養成手冊(元件物理面,新人 → Senior) |
| `fae.html` | FAE 技能養成清單(Flash/SSD 控制器 FAE 訓練路徑,37 項可勾選追蹤) |

兩個子頁左上 / 導覽列都有「← 回到入口」按鈕。

---

## ⚠️ 先看這個:私有 repo + GitHub Pages 的條件

| 你的方案 | 私有 repo 能不能用 Pages |
|---|---|
| GitHub Free(免費個人帳號) | ❌ 不行,Pages 只支援公開 repo |
| GitHub Pro / Team / Enterprise | ✅ 可以 |

**重點 1**:私有 repo 要發佈成網頁,需要 **Pro / Team / Enterprise** 方案。免費帳號只能用公開 repo 發佈。

**重點 2**:就算 repo 是私有的,**發佈出去的網站本身是公開的**(任何人有網址就能開、也能看 View Source 原始碼)。要做到「需要登入才看得到」的私有網站,需要 GitHub Enterprise Cloud 組織帳號。如果你只是想對外公開但 repo 不外流,Pro 方案就夠。

> 如果你是免費帳號又想用私有 repo,建議改用下面的 **Vercel** 方案(免費、支援私有 repo、還能加密碼保護)。

---

## 方法 A：GitHub Pages —「從分支發佈」(最簡單,推薦)

1. 在 GitHub 建立一個新的 repo(可設為 Private,前提是你是 Pro/Team/Enterprise)。
2. 把這個資料夾的內容推上去:

   ```bash
   git init
   git add .
   git commit -m "示波器教學網頁"
   git branch -M main
   git remote add origin git@github.com:<你的帳號>/<repo名稱>.git
   git push -u origin main
   ```

3. 進 repo 的 **Settings → Pages**:
   - Source 選 **Deploy from a branch**
   - Branch 選 **main**、資料夾選 **/ (root)** → Save
4. 等約 1 分鐘,網址會出現在同一頁:
   `https://<你的帳號>.github.io/<repo名稱>/`

完成。之後每次 `git push`,網站就會自動更新。

---

## 方法 B：GitHub Pages —「用 GitHub Actions」

本資料夾已附 `.github/workflows/deploy.yml`,若你偏好用 Actions 部署:

1. 一樣把內容 push 上 `main`。
2. **Settings → Pages → Source** 選 **GitHub Actions**。
3. 每次 push 到 `main`,Actions 會自動建置並發佈(可在 **Actions** 分頁看進度)。

---

## 方法 C：Vercel(免費帳號也能用私有 repo,推薦給免費 GitHub 用戶)

1. 把這個 repo(可 Private)push 到 GitHub。
2. 到 https://vercel.com → Add New → Project → 匯入這個 GitHub repo。
3. Framework Preset 選 **Other**,其餘留空,直接 Deploy。
4. 幾秒後拿到 `https://<專案名>.vercel.app` 網址。
5. (選用)Vercel 專案 **Settings → Deployment Protection** 可加密碼/登入保護,做到真正的私有網站。

---

## 檔案說明

```
.
├── index.html                      # 教學網頁本體(就是全部)
├── .nojekyll                       # 告訴 Pages 不要跑 Jekyll(純靜態)
├── README.md                       # 本說明
└── .github/workflows/deploy.yml    # (選用)GitHub Actions 自動部署
```

## 更新內容

直接編輯 `index.html` 後 `git push` 即可;Pages / Vercel 會自動重新發佈。
