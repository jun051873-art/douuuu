<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>現在在幹嘛</title>
    <style>
        body { font-family: sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; background: #f0f2f5; }
        .card { background: white; padding: 20px; border-radius: 15px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); width: 90%; max-width: 400px; text-align: center; }
        h2 { color: #333; }
        .tags { display: flex; flex-wrap: wrap; gap: 10px; justify-content: center; margin-top: 20px; }
        button { padding: 10px 20px; border: none; border-radius: 8px; cursor: pointer; background: #007bff; color: white; font-size: 16px; }
        button.manual { background: #6c757d; }
        input[type="text"] { width: 80%; padding: 10px; margin-top: 15px; border: 1px solid #ccc; border-radius: 8px; }
    </style>
</head>
<body>

<div class="card" id="main-card">
    <h2 id="question">現在在幹嘛？</h2>
    <div class="tags">
        <button onclick="saveActivity('開發程式')">👨‍💻 開發程式</button>
        <button onclick="saveActivity('沙龍工作')">💇‍♂️ 沙龍工作</button>
        <button onclick="saveActivity('休息/吃飯')">🍱 休息/吃飯</button>
        <button onclick="saveActivity('滑手機')">📱 滑手機</button>
    </div>
    <input type="text" id="customInput" placeholder="或是手動輸入...">
    <br><br>
    <button class="manual" onclick="saveActivity(document.getElementById('customInput').value)">確定紀錄</button>
</div>

<script>
    // 這裡設定自動提醒的邏輯 (例如每 30 分鐘)
    // 為了測試，我們先設定 1 分鐘後提醒
    let checkInterval = 60 * 1000; 

    function triggerCheck() {
        alert("叮咚！現在在幹嘛？請記得紀錄一下喔！");
        // 這裡可以播放聲音或震動
    }

    // 儲存紀錄的函式
    function saveActivity(activity) {
        if(!activity) return alert("請輸入內容");
        
        const record = {
            time: new Date().toLocaleString(),
            action: activity
        };

        console.log("已紀錄:", record);
        // 稍後我們會在這裡串接 Firebase
        alert("紀錄成功：" + activity);
        
        // 清空輸入框
        document.getElementById('customInput').value = "";
    }

    // 啟動定時器
    setInterval(triggerCheck, checkInterval);
</script>

</body>
</html>
