# BMI-calculator
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Enhanced BMI Calculator</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin: 50px; }
        .container { max-width: 350px; margin: auto; padding: 20px; border: 1px solid #ddd; border-radius: 10px; box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1); }
        input, select { width: 90%; padding: 10px; margin: 10px 0; border: 1px solid #ccc; border-radius: 5px; }
        button { background-color: #28a745; color: white; padding: 10px; border: none; border-radius: 5px; cursor: pointer; }
        button:hover { background-color: #218838; }
        canvas { margin-top: 20px; max-width: 100%; }
    </style>
</head>
<body>
    <div class="container">
        <h2>Enhanced BMI Calculator</h2>
        <label>Weight (kg):</label>
        <input type="number" id="weight" placeholder="Enter weight">
        
        <label>Height (m):</label>
        <input type="number" id="height" placeholder="Enter height">
        
        <label>Age:</label>
        <input type="number" id="age" placeholder="Enter age">
        
        <label>Gender:</label>
        <select id="gender">
            <option value="male">Male</option>
            <option value="female">Female</option>
        </select>
        
        <button onclick="calculateBMI()">Calculate BMI</button>
        
        <h3 id="result"></h3>
        <canvas id="bmiChart"></canvas>
    </div>

    <script>
        function calculateBMI() {
            let weight = document.getElementById("weight").value;
            let height = document.getElementById("height").value;
            let age = document.getElementById("age").value;
            let gender = document.getElementById("gender").value;

            if (!weight || !height || !age) {
                alert("Please fill all fields!");
                return;
            }

            let bmi = weight / (height * height);
            let category = "";
            
            if (bmi < 18.5) category = "Underweight";
            else if (bmi < 24.9) category = "Normal";
            else if (bmi < 29.9) category = "Overweight";
            else category = "Obese";
            
            let advice = "";
            if (gender === "female" && age > 40) advice = "Maintain a balanced diet and regular exercise.";
            else if (gender === "male" && age > 40) advice = "Keep an active lifestyle to avoid health issues.";
            else advice = "Eat healthy and stay active!";

            document.getElementById("result").innerText = `Your BMI: ${bmi.toFixed(2)} (${category}). ${advice}`;
            
            drawChart(bmi);
        }
        
        function drawChart(bmi) {
            let ctx = document.getElementById("bmiChart").getContext("2d");
            if (window.bmiChartInstance) window.bmiChartInstance.destroy();
            
            window.bmiChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ["Underweight", "Normal", "Overweight", "Obese"],
                    datasets: [{
                        label: "BMI Category",
                        data: [18.5, 24.9, 29.9, bmi],
                        backgroundColor: ['blue', 'green', 'orange', 'red']
                    }]
                },
                options: { responsive: true, maintainAspectRatio: false }
            });
        }
    </script>
</body>
</html>
