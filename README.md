<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
    <title>English Quiz - Test Your Level</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Arial', 'Helvetica', sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 15px;
        }
        
        .quiz-container {
            width: 100%;
            max-width: 550px;
            background: #ffffff;
            border-radius: 30px;
            padding: 25px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.15);
            border: 1px solid rgba(255,255,255,0.3);
        }
        
        .quiz-header {
            text-align: center;
            margin-bottom: 25px;
        }
        
        .quiz-title {
            color: #2c3e50;
            font-size: 42px;
            font-weight: 800;
            letter-spacing: 1px;
            margin-bottom: 10px;
            text-transform: uppercase;
            background: linear-gradient(135deg, #3498db, #2c3e50);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .level-indicator {
            background: #3498db;
            color: white;
            font-size: 18px;
            font-weight: 600;
            padding: 8px 25px;
            border-radius: 50px;
            display: inline-block;
            box-shadow: 0 4px 10px rgba(52,152,219,0.3);
        }
        
        .timer-container {
            text-align: center;
            margin-bottom: 20px;
        }
        
        .timer {
            display: inline-block;
            background: #2c3e50;
            color: white;
            font-size: 36px;
            font-weight: bold;
            padding: 12px 30px;
            border-radius: 60px;
            box-shadow: 0 4px 15px rgba(44,62,80,0.3);
        }
        
        .question-area {
            background: #f8f9fa;
            border-radius: 20px;
            padding: 30px 20px;
            margin-bottom: 25px;
            border-left: 5px solid #3498db;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
        }
        
        .question-text {
            color: #2c3e50;
            font-size: 22px;
            font-weight: 600;
            text-align: center;
            line-height: 1.5;
        }
        
        .options-container {
            display: flex;
            flex-direction: column;
            gap: 12px;
            margin-bottom: 25px;
        }
        
        .option-btn {
            background: white;
            border: 2px solid #e0e0e0;
            border-radius: 15px;
            padding: 18px 20px;
            color: #2c3e50;
            font-size: 18px;
            font-weight: 500;
            text-align: left;
            cursor: pointer;
            transition: all 0.2s ease;
            width: 100%;
            display: block;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
        }
        
        .option-btn:hover:not(:disabled) {
            background: #f0f7ff;
            border-color: #3498db;
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(52,152,219,0.15);
        }
        
        .option-btn.selected {
            background: #e3f2fd;
            border-color: #3498db;
            box-shadow: 0 4px 0 #2980b9;
        }
        
        .option-btn.correct {
            background: #4CAF50;
            border-color: #45a049;
            color: white;
            box-shadow: 0 4px 0 #2d6a2d;
        }
        
        .option-btn.incorrect {
            background: #f44336;
            border-color: #d32f2f;
            color: white;
            box-shadow: 0 4px 0 #9a2828;
        }
        
        .option-btn:disabled {
            opacity: 0.9;
            cursor: default;
            transform: none;
        }
        
        .option-prefix {
            display: inline-block;
            width: 35px;
            height: 35px;
            background: #3498db;
            color: white;
            border-radius: 10px;
            text-align: center;
            line-height: 35px;
            font-size: 20px;
            font-weight: bold;
            margin-right: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .loading-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255,255,255,0.95);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            display: none;
        }
        
        .loading-content {
            background: white;
            padding: 40px;
            border-radius: 30px;
            text-align: center;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
        }
        
        .loading-spinner {
            width: 60px;
            height: 60px;
            border: 6px solid #f0f0f0;
            border-top-color: #3498db;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        .result-screen {
            text-align: center;
        }
        
        .final-score {
            background: linear-gradient(135deg, #3498db, #2c3e50);
            border-radius: 25px;
            padding: 35px;
            margin: 20px 0;
            color: white;
        }
        
        .score-number {
            font-size: 90px;
            font-weight: bold;
            line-height: 1;
            margin: 15px 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }
        
        .score-label {
            font-size: 28px;
            opacity: 0.9;
        }
        
        .level-result {
            font-size: 26px;
            margin: 20px 0;
            padding: 15px;
            background: rgba(255,255,255,0.15);
            border-radius: 60px;
        }
        
        .action-btn {
            background: white;
            border: none;
            border-radius: 15px;
            padding: 18px;
            color: #2c3e50;
            font-size: 22px;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            margin: 12px 0;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            border: 2px solid #e0e0e0;
            transition: all 0.2s ease;
        }
        
        .action-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 15px rgba(52,152,219,0.3);
            border-color: #3498db;
        }
        
        .action-btn.secondary {
            background: #f8f9fa;
        }
        
        .name-input {
            width: 100%;
            padding: 15px;
            font-size: 18px;
            border-radius: 15px;
            border: 2px solid #e0e0e0;
            margin: 10px 0;
            transition: all 0.2s ease;
        }
        
        .name-input:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 0 3px rgba(52,152,219,0.2);
        }
        
        @media (max-width: 480px) {
            .quiz-title { font-size: 36px; }
            .question-text { font-size: 20px; }
            .option-btn { font-size: 16px; padding: 15px; }
            .score-number { font-size: 70px; }
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <div id="quizContent"></div>
    </div>

    <div id="loading" class="loading-overlay">
        <div class="loading-content">
            <div class="loading-spinner"></div>
            <div style="font-size: 20px; color: #2c3e50;">Carregando...</div>
        </div>
    </div>

    <script>
        // CONFIGURE AQUI OS LINKS DE REDIRECIONAMENTO
        const SHOPEE_LINK = "https://s.shopee.com.br/70DpcjasH2"; // Link para "FAZER OUTRA ETAPA"
        const RESULTADOS_LINK = "https://s.shopee.com.br/70DpcjasH2"; // Link para "VER RESULTADOS"

        // ===== 20 PERGUNTAS DE INGLÊS =====
        const questions = [
            // BÁSICO (1-7)
            {
                question: "🇬🇧 What is the correct answer? 'She ___ to school every day.'",
                options: ["go", "goes", "going", "went"],
                answer: 2,
                level: "Básico"
            },
            {
                question: "🇬🇧 Choose the correct article: '___ apple a day keeps the doctor away.'",
                options: ["A", "An", "The", "None"],
                answer: 2,
                level: "Básico"
            },
            {
                question: "🇬🇧 What's the past of 'eat'?",
                options: ["eated", "ate", "eaten", "eat"],
                answer: 2,
                level: "Básico"
            },
            {
                question: "🇬🇧 Complete: 'I ___ a student.'",
                options: ["is", "are", "am", "be"],
                answer: 3,
                level: "Básico"
            },
            {
                question: "🇬🇧 What's the opposite of 'hot'?",
                options: ["warm", "cold", "cool", "chilly"],
                answer: 2,
                level: "Básico"
            },
            {
                question: "🇬🇧 Choose: 'They ___ playing football now.'",
                options: ["is", "am", "are", "be"],
                answer: 3,
                level: "Básico"
            },
            {
                question: "🇬🇧 What's this? '___' (book)",
                options: ["It's a book", "This are a book", "These is book", "It book"],
                answer: 1,
                level: "Básico"
            },
            
            // INTERMEDIÁRIO (8-14)
            {
                question: "🇬🇧 If I ___ you, I would study more.",
                options: ["was", "were", "am", "is"],
                answer: 2,
                level: "Intermediário"
            },
            {
                question: "🇬🇧 She's been working here ___ 2010.",
                options: ["for", "since", "from", "ago"],
                answer: 2,
                level: "Intermediário"
            },
            {
                question: "🇬🇧 By the time we arrived, they ___ dinner.",
                options: ["already had", "had already had", "have already had", "already have"],
                answer: 2,
                level: "Intermediário"
            },
            {
                question: "🇬🇧 I wish I ___ taller.",
                options: ["was", "were", "am", "is"],
                answer: 2,
                level: "Intermediário"
            },
            {
                question: "🇬🇧 The movie ___ by Spielberg.",
                options: ["directed", "was directed", "directs", "is direct"],
                answer: 2,
                level: "Intermediário"
            },
            {
                question: "🇬🇧 She suggested ___ to the cinema.",
                options: ["to go", "going", "go", "went"],
                answer: 2,
                level: "Intermediário"
            },
            {
                question: "🇬🇧 If he had studied, he ___ the test.",
                options: ["would pass", "would have passed", "will pass", "passed"],
                answer: 2,
                level: "Intermediário"
            },
            
            // AVANÇADO (15-20)
            {
                question: "🇬🇧 Never before ___ such a beautiful sunset.",
                options: ["I have seen", "have I seen", "I saw", "did I see"],
                answer: 2,
                level: "Avançado"
            },
            {
                question: "🇬🇧 Had I known, I ___ differently.",
                options: ["would have acted", "would act", "will act", "acted"],
                answer: 1,
                level: "Avançado"
            },
            {
                question: "🇬🇧 Not only ___ late, but she also forgot the documents.",
                options: ["she arrived", "did she arrive", "arrived she", "she did arrive"],
                answer: 2,
                level: "Avançado"
            },
            {
                question: "🇬🇧 The committee ___ in disagreement for weeks.",
                options: ["has been", "have been", "is being", "are being"],
                answer: 1,
                level: "Avançado"
            },
            {
                question: "🇬🇧 Were she to arrive early, we ___ the meeting.",
                options: ["would start", "will start", "would have started", "start"],
                answer: 1,
                level: "Avançado"
            },
            {
                question: "🇬🇧 Her writing is comparable ___ that of a professional author.",
                options: ["with", "to", "as", "like"],
                answer: 2,
                level: "Avançado"
            }
        ];

        let current = 0;
        let score = 0;
        let answered = false;
        let userAnswers = [];
        let timer;
        let timeLeft = 45;

        function getLevel(currentIndex) {
            if (currentIndex < 7) return "BÁSICO";
            if (currentIndex < 14) return "INTERMEDIÁRIO";
            return "AVANÇADO";
        }

        function startTimer() {
            clearInterval(timer);
            timeLeft = 45;
            updateTimerDisplay();
            
            timer = setInterval(() => {
                timeLeft--;
                updateTimerDisplay();
                
                if (timeLeft <= 0) {
                    clearInterval(timer);
                    if (!answered) {
                        userAnswers.push(0);
                        nextQuestion();
                    }
                }
            }, 1000);
        }

        function updateTimerDisplay() {
            const timerEl = document.getElementById('timer');
            if (timerEl) timerEl.textContent = `⏳ ${timeLeft}s`;
        }

        function showQuestion() {
            answered = false;
            const q = questions[current];
            const currentLevel = getLevel(current);
            
            let html = `
                <div class="quiz-header">
                    <div class="quiz-title">ENGLISH QUIZ</div>
                    <div class="level-indicator">${currentLevel}</div>
                </div>
                
                <div class="timer-container">
                    <div class="timer" id="timer">⏳ 45s</div>
                </div>
                
                <div class="question-area">
                    <div class="question-text">${q.question}</div>
                </div>
                
                <div class="options-container" id="optionsContainer">
            `;
            
            const letters = ['A', 'B', 'C', 'D'];
            q.options.forEach((opt, i) => {
                html += `
                    <button class="option-btn" onclick="selectOption(${i+1})">
                        <span class="option-prefix">${letters[i]}</span>
                        ${opt}
                    </button>
                `;
            });
            
            html += `</div>`;
            
            document.getElementById('quizContent').innerHTML = html;
            startTimer();
        }

        function selectOption(selected) {
            if (answered) return;
            answered = true;
            clearInterval(timer);
            
            const correct = questions[current].answer;
            const buttons = document.querySelectorAll('.option-btn');
            
            buttons.forEach(b => b.classList.remove('selected', 'correct', 'incorrect'));
            buttons[selected-1].classList.add('selected');
            
            setTimeout(() => {
                buttons.forEach((btn, i) => {
                    if (i+1 === correct) {
                        btn.classList.add('correct');
                    } else if (i+1 === selected && selected !== correct) {
                        btn.classList.add('incorrect');
                    }
                    btn.disabled = true;
                });
                
                userAnswers.push(selected);
                if (selected === correct) {
                    score++;
                    confetti({
                        particleCount: 30,
                        spread: 50,
                        colors: ['#3498db', '#f1c40f']
                    });
                }
                
                setTimeout(nextQuestion, 800);
            }, 300);
        }

        function nextQuestion() {
            current++;
            if (current < questions.length) {
                showQuestion();
            } else {
                showFinalScreen();
            }
        }

        function showFinalScreen() {
            let levelMessage = "";
            let levelEmoji = "";
            
            if (score >= 15) {
                levelMessage = "AVANÇADO - Excellent! 🌟";
                levelEmoji = "🏆";
                confetti({
                    particleCount: 200,
                    spread: 120,
                    colors: ['#3498db', '#f1c40f']
                });
            } else if (score >= 8) {
                levelMessage = "INTERMEDIÁRIO - Good job! 👍";
                levelEmoji = "📚";
                confetti({
                    particleCount: 100,
                    spread: 80,
                    colors: ['#f1c40f']
                });
            } else {
                levelMessage = "BÁSICO - Keep studying! 💪";
                levelEmoji = "📝";
            }
            
            let html = `
                <div class="quiz-header">
                    <div class="quiz-title">ENGLISH QUIZ</div>
                </div>
                
                <div class="result-screen">
                    <div class="final-score">
                        <div class="score-label">Your Score</div>
                        <div class="score-number">${score}/${questions.length}</div>
                        <div class="level-result">${levelEmoji} ${levelMessage}</div>
                    </div>
                    
                    <button class="action-btn" onclick="redirectToResultados()">
                        🔗 VER RESULTADOS
                    </button>
                    
                    <button class="action-btn secondary" onclick="redirectToShopee()">
                        🚀 FAZER OUTRA ETAPA
                    </button>
                    
                    <input type="text" class="name-input" id="participantName" 
                           placeholder="Digite seu nome">
                    <button class="action-btn secondary" onclick="sendResults()">
                        💾 SALVAR RESULTADO
                    </button>
                </div>
            `;
            
            document.getElementById('quizContent').innerHTML = html;
        }

        function redirectToResultados() {
            window.open(RESULTADOS_LINK, '_blank');
        }

        function redirectToShopee() {
            window.open(SHOPEE_LINK, '_blank');
        }

        function sendResults() {
            const name = document.getElementById('participantName').value.trim();
            if (!name) {
                alert('Por favor, digite seu nome');
                return;
            }
            
            document.getElementById('loading').style.display = 'flex';
            
            setTimeout(() => {
                document.getElementById('loading').style.display = 'none';
                alert(`Thank you ${name}! Your score: ${score}/${questions.length}`);
            }, 1000);
        }

        // Inicia o quiz
        showQuestion();
    </script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
</body>
</html>
