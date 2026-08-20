<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VPN Checker</title>

    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: white;
            color: #111;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .container {
            width: 90%;
            max-width: 500px;
            text-align: center;
            padding: 35px 25px;
            border-radius: 20px;
            box-shadow: 0 8px 30px rgba(0,0,0,0.12);
        }

        h1 {
            color: #16a34a;
            font-size: 40px;
            margin-bottom: 10px;
        }

        p {
            color: #555;
            line-height: 1.5;
        }

        .ip-box {
            margin: 25px 0;
            padding: 20px;
            border-radius: 15px;
            background: #f0fdf4;
            border: 2px solid #22c55e;
        }

        #ip {
            font-size: 25px;
            font-weight: bold;
            color: #15803d;
            word-break: break-all;
        }

        button {
            background: #16a34a;
            color: white;
            border: none;
            padding: 15px 25px;
            border-radius: 12px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
        }

        button:hover {
            background: #15803d;
        }

        .info {
            margin-top: 25px;
            font-size: 14px;
            color: #777;
        }
    </style>
</head>

<body>

    <div class="container">

        <h1>VPN Checker</h1>

        <p>
            Prüfe deine öffentliche IP-Adresse.
            Schalte deinen VPN ein und prüfe danach erneut.
        </p>

        <div class="ip-box">
            <p>Deine aktuelle IP-Adresse:</p>
            <div id="ip">Wird geladen...</div>
        </div>

        <button onclick="checkIP()">IP prüfen</button>

        <p class="info">
            Wenn sich deine IP-Adresse nach dem Einschalten
            des VPNs verändert, wird dein Internetverkehr
            wahrscheinlich über den VPN geleitet.
        </p>

    </div>

    <script>
        async function checkIP() {
            const ipElement = document.getElementById("ip");

            ipElement.textContent = "Wird geprüft...";

            try {
                const response = await fetch("https://api.ipify.org?format=json");
                const data = await response.json();

                ipElement.textContent = data.ip;
            } catch (error) {
                ipElement.textContent = "IP konnte nicht ermittelt werden.";
            }
        }

        checkIP();
    </script>

</body>
</html>
