<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Couveuse Automatique</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 500px;
            margin: auto;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
            display: flex;
            justify-content: space-around;
            align-items: center;
        }
        .section {
            width: 45%;
        }
        .separator {
            width: 2px;
            height: 100px;
            background-color: black;
        }
        .btn {
            margin: 5px;
            padding: 10px;
            font-size: 16px;
            cursor: pointer;
            border: none;
            background-color: #007bff;
            color: white;
            border-radius: 5px;
        }
        .btn:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <h1>Couveuse Automatique</h1>
    <div class="container">
        <div class="section">
            <h2>Température</h2>
            <p><span id="temperature">--</span>°C</p>
            <button class="btn" onclick="changerValeur('temperature', 1)">+1°C</button>
            <button class="btn" onclick="changerValeur('temperature', -1)">-1°C</button>
        </div>
        <div class="separator"></div>
        <div class="section">
            <h2>Humidité</h2>
            <p><span id="humidite">--</span>%</p>
            <button class="btn" onclick="changerValeur('humidite', 5)">+5%</button>
            <button class="btn" onclick="changerValeur('humidite', -5)">-5%</button>
        </div>
    </div>
    <script>
        function changerValeur(elementId, increment) {
            let span = document.getElementById(elementId);
            let valeur = parseInt(span.innerText);
            valeur = isNaN(valeur) ? 0 : valeur + increment;
            span.innerText = valeur;
        }

        function getDHT11Data() {
            fetch('/dht11')
                .then(response => response.json())
                .then(data => {
                    document.getElementById('temperature').innerText = data.temperature;
                    document.getElementById('humidite').innerText = data.humidite;
                })
                .catch(error => console.error('Erreur lors de la récupération des données:', error));
        }
        
        setInterval(getDHT11Data, 5000);
    </script>
</body>
</html>
