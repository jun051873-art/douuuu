<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>現在在幹嘛</title>
    <style>
        /* 賈伯斯式簡約美學 CSS */
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; background: #f5f5f7; }
        .card { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); padding: 40px 30px; border-radius: 30px; box-shadow: 0 10px 40px rgba(0,0,0,0.06); width: 90%; max-width: 380px; text-align: center; border: 1px solid rgba(255,255,255,0.4); }
        h2 { color: #1d1d1f; font-weight: 600; margin-bottom: 30px; letter-spacing: -0.5px; }
        .tags { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        button { padding: 15px; border: none; border-radius: 16px; cursor: pointer; background: #fff; color: #1d1d1f; font-size: 15px; font-weight: 500; box-shadow: 0 4px 10px rgba(0,0,0,0.03); transition: all 0.2s; border: 1px solid #e5e5e7; }
        button:active { transform: scale(0.95); background: #f2f2f7; }
        .btn-blue { background: #0071e3; color: white; border: none; grid-column: span 2; margin-top: 10px; }
        input[type="text"] { width: 100%; padding: 15px; margin-top: 25px; border: 1px solid #d2d2d7; border-radius: 14px; font-size: 16px; background: rgba(255,255,255,0.5); box-sizing: border-box; outline: none; transition: border 0.3s; }
        input[type="text"]:focus { border-color: #0071e3; }
    </style>
</head>
<body>

<div class="card">
    <h2>現在在幹嘛？</h2>
    <div class="tags">
        <button onclick="saveActivity('👨‍💻 開發程式')">開發程式</button>
        <button onclick="saveActivity('💇‍♂️ 沙龍工作')">沙龍工作</button>
        <button onclick="saveActivity('🍱 休息吃飯')">休息吃飯</button>
        <button onclick="saveActivity('📱 耍廢滑機')">耍廢滑機</button>
        
        <input type="text" id="customInput" placeholder="或是手動輸入目前在做什麼...">
        <button class="btn-blue" onclick="saveActivity(document.getElementById('customInput').value)">確定紀錄</button>
    </div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
  import { getFirestore, collection, addDoc, serverTimestamp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

  // 根據你的截圖自動填入配置
  const firebaseConfig = {
    apiKey: "AIzaSyAt3NMGtToRrMbau8kIYyOybgIv",
    authDomain: "now-doing.firebaseapp.com",
    projectId: "now-doing",
    storageBucket: "now-doing.firebasestorage.app",
    messagingSenderId: "234295652644",
    appId: "1:234295652644:web:c9b3c37de32d94"
  };

  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);

  window.saveActivity = async function(activity) {
    if(!activity) return;
    
    try {
      // 資料會存入名為 daily_logs 的集合
      await addDoc(collection(db, "daily_logs"), {
        action: activity,
        timestamp: serverTimestamp(),
        device: "iPhone"
      });
      alert("✅ 已記錄：" + activity);
      document.getElementById('customInput').value = "";
    } catch (e) {
      alert("儲存失敗！請確認 Firestore 規則是否為測試模式");
      console.error(e);
    }
  }

  // 設定提醒：每 20 分鐘跳出一次瀏覽器通知
  setInterval(() => {
    alert("叮咚！現在在幹嘛？");
  }, 20 * 60 * 1000);
</script>

</body>
</html>
