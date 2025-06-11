<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI-Powered BMI Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .container {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .input-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input, select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            margin-bottom: 10px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .result {
            margin-top: 20px;
            padding: 15px;
            border-radius: 4px;
            display: none;
        }
        .ai-insights {
            margin-top: 20px;
            padding: 15px;
            background-color: #e8f5e9;
            border-radius: 4px;
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>AI-Powered BMI Calculator</h1>
        
        <div class="input-group">
            <label for="gender">Gender:</label>
            <select id="gender">
                <option value="male">Male</option>
                <option value="female">Female</option>
                <option value="other">Other</option>
            </select>
        </div>

        <div class="input-group">
            <label for="age">Age:</label>
            <input type="number" id="age" min="0" max="120" required>
        </div>

        <div class="input-group">
            <label for="height">Height (cm):</label>
            <input type="number" id="height" min="0" step="0.1" required>
        </div>

        <div class="input-group">
            <label for="weight">Weight (kg):</label>
            <input type="number" id="weight" min="0" step="0.1" required>
        </div>

        <div class="input-group">
            <label for="activity">Activity Level:</label>
            <select id="activity">
                <option value="sedentary">Sedentary</option>
                <option value="light">Lightly Active</option>
                <option value="moderate">Moderately Active</option>
                <option value="very">Very Active</option>
                <option value="extra">Extra Active</option>
            </select>
        </div>

        <button onclick="calculateBMI()">Calculate BMI</button>

        <div id="result" class="result">
            <h2>Your BMI Results</h2>
            <p id="bmi-value"></p>
            <p id="bmi-category"></p>
        </div>

        <div id="ai-insights" class="ai-insights">
            <h2>AI Health Insights</h2>
            <div id="health-recommendations"></div>
            <div id="personalized-tips"></div>
        </div>
    </div>

    <script>
        function calculateBMI() {
            const height = parseFloat(document.getElementById('height').value);
            const weight = parseFloat(document.getElementById('weight').value);
            const age = parseInt(document.getElementById('age').value);
            const gender = document.getElementById('gender').value;
            const activity = document.getElementById('activity').value;

            if (!height || !weight || !age) {
                alert('Please enter all values.');
                return;
            }

            // BMI calculation
            const bmi = weight / Math.pow(height / 100, 2);

            let category = '';
            if (bmi < 18.5) {
                category = 'Underweight';
            } else if (bmi < 24.9) {
                category = 'Normal weight';
            } else if (bmi < 29.9) {
                category = 'Overweight';
            } else {
                category = 'Obese';
            }

            document.getElementById('result').style.display = 'block';
            document.getElementById('bmi-value').textContent = `Your BMI is ${bmi.toFixed(2)}`;
            document.getElementById('bmi-category').textContent = `Category: ${category}`;

            // Simulated AI Insights (replace with real API for actual AI)
            let aiText = '';
            let tips = '';

            if (category === 'Underweight') {
                aiText = "You are below the normal BMI range. Consider a balanced diet with healthy calorie surplus.";
                tips = "Consult a healthcare provider for personalized advice. Regular strength training can help gain healthy weight.";
            } else if (category === 'Normal weight') {
                aiText = "Your BMI is in the normal range. Maintain your healthy habits!";
                tips = "Continue regular physical activity and a balanced diet.";
            } else if (category === 'Overweight') {
                aiText = "You are above the normal BMI range. Consider monitoring your diet and increasing physical activity.";
                tips = "Aim for 30 minutes of moderate exercise most days. Reduce sugary and fatty foods.";
            } else {
                aiText = "You are in the obese BMI range. Health risks are elevated. Please consider professional guidance.";
                tips = "Consult a healthcare provider. Focus on gradual, sustainable changes to your eating and activity patterns.";
            }

            // Activity-based recommendation
            if (activity === 'sedentary') {
                tips += " Try to increase your daily activity, even short walks can help.";
            } else if (activity === 'extra') {
                tips += " Great job staying active! Remember to allow time for recovery.";
            }

            document.getElementById('ai-insights').style.display = 'block';
            document.getElementById('health-recommendations').textContent = aiText;
            document.getElementById('personalized-tips').textContent = tips;
        }
    </script>
</body>
</html>
