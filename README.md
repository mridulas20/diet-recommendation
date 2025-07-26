# diet-recommendation
<!DOCTYPE html>
<html>
<head>
  <title>Diet Recommendation System</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #fef6f9;
      color: #333;
      padding: 20px;
      max-width: 500px;
      margin: auto;
    }
    h1 {
      text-align: center;
      color: #d63384;
    }
    label, input, select {
      display: block;
      width: 100%;
      margin-top: 10px;
    }
    button {
      margin-top: 20px;
      padding: 10px;
      width: 100%;
      background: #d63384;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .result {
      margin-top: 20px;
      background: #fff0f6;
      padding: 15px;
      border-radius: 8px;
    }
  </style>
</head>
<body>

  <h1>Diet Recommendation</h1>

  <label>Name:</label>
  <input type="text" id="name" />

  <label>Age:</label>
  <input type="number" id="age" />

  <label>Gender:</label>
  <select id="gender">
    <option value="female">Female</option>
    <option value="male">Male</option>
  </select>

  <label>Goal:</label>
  <select id="goal">
    <option value="lose">Lose Weight</option>
    <option value="gain">Gain Weight</option>
    <option value="maintain">Maintain Weight</option>
  </select>

  <label>Activity Level:</label>
  <select id="activity">
    <option value="low">Low</option>
    <option value="moderate">Moderate</option>
    <option value="high">High</option>
  </select>

  <button onclick="recommendDiet()">Get Recommendation</button>

  <div class="result" id="output"></div>

  <script>
    function recommendDiet() {
      const name = document.getElementById("name").value;
      const age = parseInt(document.getElementById("age").value);
      const gender = document.getElementById("gender").value;
      const goal = document.getElementById("goal").value;
      const activity = document.getElementById("activity").value;

      let baseCalories = (gender === "male") ? 2500 : 2000;

      if (activity === "low") baseCalories -= 300;
      else if (activity === "high") baseCalories += 300;

      let plan = "";

      if (goal === "lose") {
        baseCalories -= 500;
        plan = "High-protein, low-carb meals with more veggies.";
      } else if (goal === "gain") {
        baseCalories += 500;
        plan = "Protein-rich diet with healthy fats and complex carbs.";
      } else {
        plan = "Balanced diet with whole grains, proteins, and veggies.";
      }

      const output = `
        <h3>Hello ${name}!</h3>
        <p>👩‍⚕️ Age: ${age}, Gender: ${gender.charAt(0).toUpperCase() + gender.slice(1)}</p>
        <p>🎯 Your Goal: ${goal.charAt(0).toUpperCase() + goal.slice(1)}</p>
        <p>🔥 Activity Level: ${activity.charAt(0).toUpperCase() + activity.slice(1)}</p>
        <p><strong>🍱 Recommended Daily Calories:</strong> ${baseCalories} kcal</p>
        <p><strong>📝 Diet Plan:</strong> ${plan}</p>
      `;

      document.getElementById("output").innerHTML = output;
    }
  </script>

</body>
</html>
