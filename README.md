<!DOCTYPE html>
<html lang="he">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>תזונה אישית לספורטאים</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>ברוך הבא לתזונה מותאמת אישית</h1>
        <p>הכנס את הנתונים האישיים שלך כדי לקבל תוכנית תזונה מותאמת לספורטאים.</p>
    </header>
    
    <main>
        <form id="nutritionForm">
            <label for="age">גיל:</label>
            <input type="number" id="age" required><br><br>

            <label for="weight">משקל (ק"ג):</label>
            <input type="number" id="weight" required><br><br>

            <label for="height">גובה (ס"מ):</label>
            <input type="number" id="height" required><br><br>

            <label for="goal">מטרה (הרזיה/ההשמנה):</label>
            <select id="goal">
                <option value="lose">הרזיה</option>
                <option value="gain">ההשמנה</option>
                <option value="maintain">שימור משקל</option>
            </select><br><br>

            <label for="activity">רמת פעילות גופנית:</label>
            <select id="activity">
                <option value="low">נמוכה</option>
                <option value="moderate">בינונית</option>
                <option value="high">גבוהה</option>
            </select><br><br>

            <button type="submit">קבל תוכנית תזונה</button>
        </form>

        <div id="result"></div>
    </main>

    <script src="app.js"></script>
</body>
</html># -
/* styles.css */
body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #f4f4f4;
    padding: 20px;
}

header {
    margin-bottom: 30px;
}

form {
    display: block;
    margin: 0 auto;
    width: 300px;
    background-color: #fff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

label {
    display: block;
    margin-bottom: 5px;
}

input, select {
    width: 100%;
    padding: 10px;
    margin-bottom: 15px;
    border-radius: 5px;
    border: 1px solid #ccc;
}

button {
    padding: 10px 20px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}

#result {
    margin-top: 30px;
}
// app.js
document.getElementById('nutritionForm').addEventListener('submit', function(e) {
    e.preventDefault();
    
    // קבלת נתונים מהטופס
    const age = parseInt(document.getElementById('age').value);
    const weight = parseInt(document.getElementById('weight').value);
    const height = parseInt(document.getElementById('height').value);
    const goal = document.getElementById('goal').value;
    const activity = document.getElementById('activity').value;

    // חישוב קלוריות בסיסיות על פי נתוני הגובה, המשקל, גיל ורמת פעילות
    let bmr = 10 * weight + 6.25 * height - 5 * age + 5; // נוסחת Harris-Benedict
    let calorieMultiplier = 1.2; // למקרה של פעילות גופנית נמוכה (סוגי פעילות אחרים יכולים לשנות את הערך)
    
    if (activity === 'moderate') calorieMultiplier = 1.55;
    if (activity === 'high') calorieMultiplier = 1.9;

    let calories = bmr * calorieMultiplier;

    // התאמה על פי המטרה
    if (goal === 'lose') {
        calories -= 500; // חיסול של 500 קלוריות לירידה במשקל
    } else if (goal === 'gain') {
        calories += 500; // הוספת 500 קלוריות להשמנה
    }

    // הצגת התוצאה למשתמש
    const resultDiv = document.getElementById('result');
    resultDiv.innerHTML = `<h2>תוכנית תזונה מותאמת</h2>
                           <p>הקלוריות היומיות המומלצות עבורך: ${Math.round(calories)} קלוריות.</p>`;
});
