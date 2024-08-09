# KevyPredictor
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KevyPredictor</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(to bottom, #FF69B4, #FFB6C1);
            color: white;
            text-align: center;
            margin: 0;
            padding: 0;
        }
        header {
            padding: 20px;
            background-color: #0047AB;
            color: white;
            font-size: 1.5em;
            text-shadow: 2px 2px #000000;
            animation: fadeIn 2s ease-in-out;
        }
        #description {
            margin-top: 10px;
            font-size: 1em;
            color: #C0C0C0;
            animation: slideIn 2s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        @keyframes slideIn {
            from { transform: translateY(-20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        .container {
            margin-top: 50px;
            text-align: center;
        }
        input[type="text"] {
            padding: 10px;
            width: 80%;
            max-width: 400px;
            font-size: 1em;
            border: 2px solid #0047AB;
            border-radius: 5px;
            margin-bottom: 10px;
        }
        button {
            padding: 10px 20px;
            background-color: #0047AB;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #00308F;
        }
        #error-message, #loading, #result {
            margin-top: 20px;
            font-size: 1.2em;
            animation: fadeIn 0.5s ease-in-out;
        }
        #error-message {
            color: red;
            animation: shake 0.5s;
        }
        @keyframes shake {
            0% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            50% { transform: translateX(5px); }
            75% { transform: translateX(-5px); }
            100% { transform: translateX(0); }
        }
        #loading {
            display: none;
        }
        #result {
            color: #00FF00;
            display: none;
            animation: resultAppear 1s ease-in-out;
        }
        @keyframes resultAppear {
            from { opacity: 0; transform: scale(0.5); }
            to { opacity: 1; transform: scale(1); }
        }
        #warning {
            margin-top: 20px;
            font-size: 0.9em;
            color: white;
            animation: fadeIn 1s ease-in-out;
        }
        #contact-button {
            position: absolute;
            top: 10px;
            left: 10px;
            background-color: black;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }
        #contact-button:hover {
            background-color: #333333;
        }
        footer {
            margin-top: 50px;
            padding: 10px;
            background-color: #0047AB;
            color: white;
            font-size: 0.8em;
            animation: fadeIn 1.5s ease-in-out;
        }
    </style>
</head>
<body>

    <header>
        Bienvenue sur KevyPredictor💻
        <div id="description">KevyPredictor est votre outil de prédiction basé sur des scores précédents.</div>
    </header>

    <button id="contact-button" onclick="contactMe()">Me Contacter</button>

    <div class="container">
        <input type="text" id="scores" placeholder="Entrez les scores précédents, séparés par des virgules (ex: 1.2, 2.3, 3.4)" />
        <br>
        <button onclick="predict()">PREDICTION</button>

        <div id="error-message"></div>
        <div id="loading">Calcul en cours...</div>
        <div id="result"></div>
        <div id="warning">
            Les prédictions ne sont pas sûres à 100%, pariez avec précaution.<br>
            By_Kevy WHATSAPP : +2250768388770
        </div>
    </div>

    <footer>@2024 créé par Kevin_Amon Tout droit réservé.</footer>

    <script>
        function contactMe() {
            window.location.href = "https://wa.me/qr/DLQCUHPIVBYLE1";
        }

        function predict() {
            const scoresInput = document.getElementById('scores').value;
            const scores = scoresInput.split(',').map(Number);
            const errorMessage = document.getElementById('error-message');
            const loading = document.getElementById('loading');
            const result = document.getElementById('result');

            errorMessage.textContent = '';
            result.style.display = 'none';

            if (scores.length < 5 || scores.some(isNaN)) {
                errorMessage.textContent = '🚫ENTREZ MINIMUM 5 SCORES🚫';
                return;
            }

            loading.style.display = 'block';

            setTimeout(() => {
                const prediction = calculatePrediction(scores);
                loading.style.display = 'none';
                result.textContent = `Prochaine côte probable : ${prediction.toFixed(2)}`;
                result.style.display = 'block';
            }, 2000); 
        }

        function calculatePrediction(scores) {
            const sum = scores.reduce((a, b) => a + b, 0);
            const average = sum / scores.length;
            const squaredDiffs = scores.map(score => Math.pow(score - average, 2));
            const stdDev = Math.sqrt(squaredDiffs.reduce((a, b) => a + b, 0) / scores.length);
            return average + stdDev;
        }
    </script>

</body>
</html>
