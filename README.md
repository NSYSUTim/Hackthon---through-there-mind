本人(江威廷)負責流程圖中 api (google vertex ai agent)之部分

<img width="460*2" height="378*2" alt="image" src="https://github.com/user-attachments/assets/8d5d9664-3aa4-49fb-bdfd-1f09e5a79c8a" />

---------------------------------------------------------------------------------------------------------------

# Through Their Mind

一個以精神疾病認識與同理為主題的互動式網站，希望讓使用者透過疾病資訊與 AI 互動，更容易了解不同精神疾病相關知識。

## 專案功能

目前 repository 主要包含：

- 精神疾病知識介紹
- AI 互動／文字處理功能
- Firebase Firestore 疾病資料
- Next.js 前端與 API routes

網站以 Next.js 建置，疾病資料由 Firebase 提供，AI 相關功能則另外串接雲端 Agent / API。

## 江威廷負責內容

本人主要負責 **Google Vertex AI Agent 與 Agent 所使用的知識資料**。

Agent 的定位類似網站中的 AI 智能小助手：使用者可以輸入精神疾病相關問題，由 Agent 即時根據提供的資料回答。

實作內容包含：

- 參考 Google Codelab 的 Vertex AI Agent 建置流程：  
  https://codelabs.developers.google.com/devsite/codelabs/building-ai-agents-vertexai?hl=zh-tw#0
- 從 **PubMed** 蒐集精神疾病相關論文資料。
- 將當時取得的資料整理成可供 Agent 使用的靜態知識資料集。不是持續抓取網頁裡的資料，因為疾病這種資訊也不太可能一下變化太多。
- 將整理後的資料一次性提供給 Agent 作為回答依據，而不是持續即時抓取 PubMed 網頁。
- 撰寫指定 prompt，定義 Agent 的任務、回答方向與使用方式。
- 在 Google Vertex AI 上建立並設定 Agent。
- 建立可供網站端呼叫 Agent 的 API / 存取方式，交由負責前端的隊友整合。

因此，我負責的範圍主要是：

```text
PubMed 論文資料
      ↓
資料蒐集與整理
      ↓
Vertex AI Agent 知識資料
      ↓
Prompt / Agent 任務設定
      ↓
建立 Agent API / 呼叫方式
      ↓
交由隊友串接前端
```

Agent 本身的設定、prompt 與知識資料主要存在 Google Cloud / Vertex AI 端，因此不一定能從目前 repository 的程式碼完整看到。

## 網站架構

```text
使用者
  │
  ├─ 疾病知識頁
  │     ↓
  │   Next.js
  │     ↓
  │   Firebase Firestore
  │
  └─ AI 功能
        ↓
      網站前端
        ↓
      AI API / Agent
        ↓
      Google Cloud / Vertex AI
```

## 使用技術

- **Frontend**：Next.js 15、React 19、TypeScript
- **UI**：Tailwind CSS
- **Database**：Firebase Firestore
- **AI Agent**：Google Vertex AI
- **Knowledge Source**：PubMed 論文資料
- **Other AI API routes in repository**：Dialogflow CX / OpenAI

## Repository 結構

```text
src/
├─ app/
│  ├─ page.tsx
│  ├─ knowledge/page.tsx
│  ├─ transform/page.tsx
│  ├─ api/
│  │  ├─ dialogflow-transform/route.ts
│  │  └─ transform/route.ts
│  └─ admin/upload/page.tsx
├─ components/
├─ hooks/
├─ services/
└─ types/
```

## 執行方式

### 1. 安裝套件

```bash
npm install
```

### 2. Firebase 設定

```bash
cp src/lib/firebase.example.ts src/lib/firebase.ts
```

再依自己的 Firebase 專案填入設定，詳細步驟可參考 `FIREBASE_SETUP.md`。

### 3. 啟動網站

```bash
npm run dev
```

開啟：

```text
http://localhost:3000
```

> 本專案為 Hackathon 原型，重點在短時間內完成可操作的產品流程，因此部分雲端 Agent 設定與資料處理流程並未完整保存在 repository 中。
