<!DOCTYPE html>
<html lang="en">
<head>
  <!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-QDD42BLBF5"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-QDD42BLBF5');
</script>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Startup Idea Assessment</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            text-align: center;
            background: url('https://wallpaperaccess.com/full/17520.jpg') no-repeat center center fixed; 
            background-size: cover; 
            color: white;
        }
        .container {
            max-width: 600px;
            margin: 50px auto;
            background: rgba(0, 0, 0, 0.7);
            padding: 20px;
            border-radius: 10px;
        }
        .question { display: none; }
        .active { display: block; }
        label {
            display: flex;
            align-items: center;
            gap: 10px;
            margin: 10px 0;
            font-size: 18px;
        }
        input[type=radio], input[type=checkbox] {
            transform: scale(1.5);
        }
        button { 
            padding: 12px 20px; 
            font-size: 16px; 
            cursor: pointer; 
            background: #6200ea; 
            color: white; 
            border: none; 
            border-radius: 5px;
            margin-top: 20px;
            transition: 0.3s;
        }
        button:hover {
            background: #3700b3;
        }
        #restart {
            display: none;
            background: #ff5722;
        }
        #restart:hover {
            background: #d84315;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>👁️ WorthWiz 👁️</h2>
        <form id="quizForm">
            <div class="question active">
                <p>1. How Unique is your idea?🦄</p>
                <label><input type="radio" name="q1" value="2" onclick="enableNext()"> Copied from TikTok</label>
                <label><input type="radio" name="q1" value="5" onclick="enableNext()"> Reimagined a popular concept</label>
                <label><input type="radio" name="q1" value="10" onclick="enableNext()"> Unexplored territory</label>
            </div>
            
            <div class="question">
                <p>2. How Desperate is the World for This?😩</p>
                <label><input type="radio" name="q2" value="10" onclick="enableNext()"> People are crying for this</label>
                <label><input type="radio" name="q2" value="5" onclick="enableNext()"> Nice-to-have</label>
                <label><input type="radio" name="q2" value="2" onclick="enableNext()"> No one cares (yet)</label>
            </div>
            
            <div class="question">
                <p>3. Who's your competition?</p>
                <label><input type="radio" name="q3" value="10" onclick="enableNext()"> No competitors</label>
                <label><input type="radio" name="q3" value="5" onclick="enableNext()"> Competitors exist, but I'm better</label>
                <label><input type="radio" name="q3" value="2" onclick="enableNext()"> Overcrowded AF</label>
            </div>
            
            <div class="question">
                <p>4. What is the Scalability of this idea?📈</p>
                <label><input type="radio" name="q4" value="2" onclick="enableNext()"> Local only</label>
                <label><input type="radio" name="q4" value="5" onclick="enableNext()"> Can go national</label>
                <label><input type="radio" name="q4" value="10" onclick="enableNext()"> Global domination planned</label>
            </div>
            
            <div class="question">
                <p>5. What's the revenue potential?💰 (Choose multiple)</p>
                <label><input type="checkbox" name="q5" value="2"> Free (for clout)</label>
                <label><input type="checkbox" name="q5" value="5"> Premium pricing</label>
                <label><input type="checkbox" name="q5" value="5"> Subscription</label>
                <label><input type="checkbox" name="q5" value="5"> Ads/Sponsorships</label>
                <label><input type="checkbox" name="q5" value="0"> No plan</label>
            </div>
            
            <button type="button" onclick="nextQuestion()" disabled>Next Question</button>
            <button type="button" onclick="calculateScore()" style="display: none;">Submit</button>
            <button id="restart" type="button" onclick="restartQuiz()">Restart Quiz</button>
        </form>
        
        <h3 id="result"></h3>
        <p id="feedback"></p>
    </div>
    
    <script>
        let currentQuestion = 0;
        let questions = document.querySelectorAll('.question');
        let nextButton = document.querySelector('button');
        let submitButton = document.querySelector('button:nth-of-type(2)');
        let restartButton = document.getElementById('restart');

        function enableNext() {
            nextButton.disabled = false;
        }

        function nextQuestion() {
            if (currentQuestion < questions.length - 1) {
                questions[currentQuestion].classList.remove('active');
                currentQuestion++;
                questions[currentQuestion].classList.add('active');
                nextButton.disabled = true; 
                if (currentQuestion === questions.length - 1) {
                    nextButton.style.display = 'none';
                    submitButton.style.display = 'block';
                }
            }
        }

        function calculateScore() {
            let score = 0;
            let inputs = document.querySelectorAll('input[type=radio]:checked, input[type=checkbox]:checked');

            inputs.forEach(input => score += parseInt(input.value));
            let finalScore = (score / 50) * 10; // Scale to 10

            let resultText = `Your idea's score is:    ${finalScore.toFixed(1)} / 10`;
            let feedbackText = finalScore >= 9 ? "🦄 UNICORN ALERT! Your idea is insane! Investors will chase you." :
                               finalScore >= 7 ? "💵 Solid Potential - Your idea is great, refine it for maximum impact." :
                               finalScore >= 5 ? "💫 Needs More - Your idea has potential, but it's not quite there yet." : 
                               "🚨 Rethink - This idea may not be viable. Back to the drawing board.";

            document.getElementById('result').innerText = resultText;
            document.getElementById('feedback').innerText = feedbackText;

            submitButton.style.display = 'none';
            restartButton.style.display = 'block';
        }

        function restartQuiz() {
            currentQuestion = 0;
            document.getElementById('quizForm').reset();
            questions.forEach(q => q.classList.remove('active'));
            questions[0].classList.add('active');
            document.getElementById('result').innerText = '';
            document.getElementById('feedback').innerText = '';
            nextButton.style.display = 'block';
            submitButton.style.display = 'none';
            restartButton.style.display = 'none';
            nextButton.disabled = true;
        }
    </script>
</body>
</html>
