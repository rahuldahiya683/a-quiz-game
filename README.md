<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Current Affairs Quiz Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f0f8ff;
            color: #333;
            overflow: hidden;
        }
        #question {
            font-size: 24px;
            margin: 20px;
        }
        .options {
            display: block;
            margin: 10px auto;
            padding: 10px;
            font-size: 18px;
            width: 200px;
            cursor: pointer;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
        }
        .options:hover {
            background-color: #45a049;
        }
        #result {
            font-size: 20px;
            margin-top: 20px;
        }
        #balloons-container {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            display: none;
            overflow: hidden;
        }
        .balloon {
            width: 50px;
            height: 70px;
            background-color: red;
            border-radius: 50% 50% 0 0;
            position: absolute;
            cursor: pointer;
            animation: float 6s linear infinite;
        }
        .balloon::before {
            content: '';
            width: 2px;
            height: 10px;
            background-color: black;
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
        }
        @keyframes float {
            0% { transform: translateY(100vh); }
            100% { transform: translateY(-100vh); }
        }
    </style>
</head>
<body>

    <h1>Current Affairs Quiz Game</h1>
    <div id="question"></div>
    <div id="options"></div>
    <div id="result"></div>

    <div id="balloons-container"></div>

    <script>
        const questions = [
            {
                question: "Who is the Prime Minister of India?",
                options: ["Narendra Modi", "Rahul Gandhi", "Amit Shah", "Arvind Kejriwal"],
                answer: "Narendra Modi"
            },
            {
                question: "What is the best time to wake up in the morning?",
                options: ["6 AM", "8 AM", "5 AM", "10 AM"],
                answer: "6 AM"
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;

        function displayQuestion() {
            const currentQuestion = questions[currentQuestionIndex];
            document.getElementById('question').innerText = currentQuestion.question;
            document.getElementById('options').innerHTML = '';

            currentQuestion.options.forEach(option => {
                const button = document.createElement('button');
                button.classList.add('options');
                button.innerText = option;
                button.onclick = () => checkAnswer(option);
                document.getElementById('options').appendChild(button);
            });
        }

        function checkAnswer(selectedOption) {
            const correctAnswer = questions[currentQuestionIndex].answer;
            if (selectedOption === correctAnswer) {
                score++;
            }

            currentQuestionIndex++;
            if (currentQuestionIndex < questions.length) {
                displayQuestion();
            } else {
                endGame();
            }
        }

        function endGame() {
            document.getElementById('question').innerText = "Quiz Completed!";
            document.getElementById('options').style.display = 'none';
            document.getElementById('result').innerText = `Score: ${score}/${questions.length}`;
            
            if (score === questions.length) {
                startBalloons();
            } else {
                document.getElementById('result').innerText += " Try again for all correct answers!";
            }
        }

        function startBalloons() {
            const balloonsContainer = document.getElementById('balloons-container');
            balloonsContainer.style.display = 'block';
            
            for (let i = 0; i < 20; i++) {
                const balloon = document.createElement('div');
                balloon.classList.add('balloon');
                balloon.style.left = Math.random() * 100 + "vw";
                balloon.style.backgroundColor = getRandomColor();
                balloon.onclick = () => balloon.style.display = 'none';
                balloonsContainer.appendChild(balloon);
            }
        }

        function getRandomColor() {
            const colors = ["red", "blue", "green", "yellow", "orange", "purple", "pink"];
            return colors[Math.floor(Math.random() * colors.length)];
        }

        // Start the game by displaying the first question
        displayQuestion();
    </script>
</body>
</html>
