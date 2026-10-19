<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ski's Result</title>

<style>
    body {
        font-family: Arial, sans-serif;
        background: linear-gradient(135deg, #ede9fe, #fce7f3);
        min-height: 100vh;
        margin: 0;
        padding: 30px 15px;
        box-sizing: border-box;
        text-align: center;
    }

    .card {
        background: white;
        max-width: 380px;
        margin: 25px auto;
        padding: 25px 20px;
        border-radius: 24px;
        box-shadow: 0 8px 25px #00000015;
        box-sizing: border-box;
    }

    h1 {
        color: #7c3aed;
        font-size: 28px;
    }

    .subtitle {
        color: #777;
        margin-bottom: 25px;
    }

    input {
        display: block;
        width: 100%;
        padding: 14px;
        margin: 12px 0;
        border: 2px solid #e5e7eb;
        border-radius: 12px;
        box-sizing: border-box;
        font-size: 16px;
    }

    input:focus {
        outline: none;
        border-color: #8b5cf6;
    }

    button {
        width: 100%;
        padding: 14px;
        margin-top: 10px;
        background: #8b5cf6;
        color: white;
        border: none;
        border-radius: 12px;
        font-size: 17px;
        font-weight: bold;
        cursor: pointer;
    }

    button:active {
        opacity: 0.8;
    }

    #result {
        display: none;
        margin-top: 25px;
        padding: 18px;
        background: #f5f3ff;
        border-radius: 16px;
        overflow-wrap: anywhere;
    }

    .pass {
        color: #16a34a;
    }

    .fail {
        color: #dc2626;
    }

    .message {
        color: #7c3aed;
        font-weight: bold;
        line-height: 1.5;
    }

    .small {
        color: #888;
        font-size: 13px;
        margin-top: 20px;
    }
</style>
</head>

<body>

<div class="card">
    <h1>Result</h1>
    <p class="subtitle">Let's see how you did!</p>

    <input
        id="name"
        type="text"
        placeholder="Enter your name"
        maxlength="40"
    >

    <input
        id="correct"
        type="number"
        placeholder="Correct answers (0–40)"
        min="0"
        max="40"
        step="1"
    >

    <button onclick="calculate()">Check Result </button>

    <div id="result" aria-live="polite"></div>

    <p class="small">Total questions: 40 · Passing mark: 50%</p>
</div>

<script>
function calculate() {
    const name = document.getElementById("name").value.trim();
    const scoreInput = document.getElementById("correct");
    const scoreText = scoreInput.value;
    const score = Number(scoreText);
    const result = document.getElementById("result");

    result.style.display = "block";
    result.replaceChildren();

    if (
        name === "" ||
        scoreText === "" ||
        !Number.isInteger(score) ||
        score < 0 ||
        score > 40
    ) {
        result.textContent =
            "Please enter your name and a whole number from 0 to 40!";
        return;
    }

    const percent = score / 40 * 100;
    const passed = percent >= 50;

    const status = document.createElement("h2");
    status.className = passed ? "pass" : "fail";
    status.textContent = passed ? "PASS " : "FAIL";

    const scoreLine = document.createElement("p");
    scoreLine.textContent = "Correct answers: " + score + " / 40";

    const percentLine = document.createElement("p");
    percentLine.textContent = "Your score: " + percent + "%";

    let messages;

    if (passed) {
        messages = [
            "You did it bro! Bravo",
            "Slayy",
            "You're so smart, Diva!",
            "Keep shining, queen!"
        ];
    } else {
        messages = [
            "Try again,and keep saying 67, buddy",
            "Go clean the toilet, my friend",
            "Study harder next time, Don’t play mobile legend all the time ",
            "Don't give up, study next time instead of texting with your gf/bf!"
        ];
    }

    const message =
        messages[Math.floor(Math.random() * messages.length)];

    const messageLine = document.createElement("p");
    messageLine.className = "message";
    messageLine.textContent = message + ", " + name + "! 😂";

    result.appendChild(status);
    result.appendChild(scoreLine);
    result.appendChild(percentLine);
    result.appendChild(messageLine);
}
</script>

</body>
</html>
