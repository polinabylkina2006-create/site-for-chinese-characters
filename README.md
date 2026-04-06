<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Игра: 214 ключей китайских иероглифов | 部首记忆</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
        }

        body {
            background: linear-gradient(145deg, #eaf7ed 0%, #c8e0d2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', 'Noto Sans SC', 'Microsoft YaHei', 'WenQuanYi Micro Hei', sans-serif;
            padding: 20px;
        }

        .game-container {
            max-width: 800px;
            width: 100%;
            background: #fffef7;
            border-radius: 64px 64px 80px 80px;
            box-shadow: 0 25px 45px rgba(40, 70, 50, 0.25), inset 0 1px 4px rgba(255,255,240,0.9);
            overflow: hidden;
            border: 1px solid rgba(140, 190, 150, 0.5);
        }

        .ornament-top {
            height: 12px;
            background: repeating-linear-gradient(90deg, #6f9e7c, #6f9e7c 20px, #8bba9a 20px, #8bba9a 40px);
        }

        .game-header {
            padding: 1.5rem 2rem 0.5rem;
            text-align: center;
            background: #fefcf0;
        }

        h1 {
            font-size: 1.8rem;
            color: #2f6b47;
            letter-spacing: 2px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            flex-wrap: wrap;
        }

        h1 span {
            background: #e2f0e8;
            padding: 0 12px;
            border-radius: 60px;
            font-size: 1.2rem;
            color: #3c7b5a;
        }

        .sub {
            color: #628b72;
            margin-top: 8px;
            font-size: 0.9rem;
            border-top: 1px dashed #cbe3d6;
            display: inline-block;
            padding-top: 8px;
        }

        .stats-bar {
            display: flex;
            justify-content: space-between;
            background: #eef4e8;
            margin: 20px 25px 0;
            padding: 12px 24px;
            border-radius: 60px;
            gap: 15px;
            flex-wrap: wrap;
            font-weight: 600;
            color: #2a5c43;
            box-shadow: inset 0 1px 3px #bdd0c1, 0 2px 4px rgba(0,0,0,0.02);
        }

        .stat {
            background: white;
            padding: 5px 16px;
            border-radius: 30px;
            display: flex;
            gap: 10px;
            align-items: baseline;
        }

        .stat-value {
            font-size: 1.6rem;
            font-weight: 800;
            color: #2c7a4b;
            line-height: 1;
        }

        .quiz-card {
            background: #ffffffea;
            margin: 30px 25px 20px;
            border-radius: 56px;
            padding: 35px 20px;
            text-align: center;
            box-shadow: 0 12px 25px rgba(0, 0, 0, 0.05), inset 0 1px 0 white;
            border: 1px solid #caddcf;
        }

        .question-key {
            font-size: 7rem;
            font-family: 'Noto Sans SC', 'KaiTi', monospace;
            background: #f9fef6;
            display: inline-block;
            padding: 0.2em 0.6em;
            border-radius: 70px;
            margin-bottom: 20px;
            letter-spacing: 8px;
            color: #1f543d;
            text-shadow: 2px 2px 6px rgba(0,0,0,0.02);
        }

        .question-prompt {
            font-size: 1.1rem;
            color: #5a826b;
            margin-top: 6px;
        }

        .options-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 16px;
            margin: 20px 25px 30px;
        }

        .option-btn {
            background: #f4faf5;
            border: 2px solid #cfe2d4;
            border-radius: 60px;
            padding: 14px 8px;
            font-size: 1rem;
            font-weight: 500;
            color: #2d5d45;
            cursor: pointer;
            transition: all 0.2s;
            text-align: center;
            font-family: inherit;
        }

        .option-btn:hover:not(:disabled) {
            background: #e2f0e6;
            border-color: #77aa89;
            transform: scale(0.98);
        }

        .option-correct {
            background: #b8dfc5 !important;
            border-color: #2f8b55 !important;
            color: #144d31;
            pointer-events: none;
        }

        .option-wrong {
            background: #f3dbd4 !important;
            border-color: #c97e62 !important;
            color: #8b3c2c;
            text-decoration: line-through;
            pointer-events: none;
        }

        .feedback-area {
            margin: 0 25px 20px;
            text-align: center;
            font-size: 1rem;
            font-weight: 500;
            padding: 12px;
            border-radius: 40px;
            background: #fef7e0;
            color: #b46f3a;
        }

        .next-btn {
            background: #4c9f70;
            border: none;
            color: white;
            font-size: 1.2rem;
            font-weight: bold;
            padding: 14px 20px;
            margin: 5px 25px 35px;
            width: calc(100% - 50px);
            border-radius: 80px;
            cursor: pointer;
            transition: 0.2s;
        }

        .next-btn:hover {
            background: #3a8260;
            transform: translateY(-2px);
        }

        .reset-btn {
            background: none;
            border: 1px solid #bdd3c4;
            color: #547b64;
            padding: 8px 18px;
            border-radius: 40px;
            cursor: pointer;
            margin-bottom: 20px;
            transition: 0.2s;
            font-size: 0.8rem;
        }

        .reset-btn:hover {
            background: #e1efe6;
        }

        footer {
            text-align: center;
            font-size: 0.7rem;
            padding: 1rem 2rem 2rem;
            color: #8baa97;
            background: #fefcf0;
        }

        .progress-info {
            text-align: center;
            font-size: 0.75rem;
            color: #7faa8b;
            margin-top: -10px;
            margin-bottom: 10px;
        }

        @media (max-width: 550px) {
            .question-key { font-size: 4rem; letter-spacing: 4px; }
            .options-grid { grid-template-columns: 1fr; }
            .stat-value { font-size: 1.2rem; }
        }
    </style>
</head>
<body>

<div class="game-container">
    <div class="ornament-top"></div>
    <div class="game-header">
        <h1>
            📖 部首记忆 
            <span>214 ключей</span>
        </h1>
        <div class="sub">выбери правильное название китайского радикала</div>
    </div>

    <div class="stats-bar">
        <div class="stat">🎯 Счёт: <span class="stat-value" id="scoreValue">0</span></div>
        <div class="stat">📊 Вопросов: <span class="stat-value" id="totalAsked">0</span></div>
        <div class="stat">🏆 Лучший: <span class="stat-value" id="bestStreak">0</span></div>
    </div>

    <div class="quiz-card">
        <div class="question-key" id="currentKey">一</div>
        <div class="question-prompt">🔽 что означает этот ключ?</div>
    </div>

    <div id="optionsContainer" class="options-grid"></div>

    <div id="feedbackMsg" class="feedback-area">✨ нажми на вариант ответа</div>

    <button id="nextBtn" class="next-btn">➡️ следующий ключ</button>
    <div style="display: flex; justify-content: center; margin-bottom: 8px;">
        <button id="resetGameBtn" class="reset-btn">⟳ сбросить прогресс</button>
    </div>
    <div class="progress-info">🎋 база содержит все 214 ключей из списка Канси</div>
    <footer>
        214 радикалов · изучение через игру · статистика в браузере
    </footer>
</div>

<script>
    // --------------------------------------------------------------
    // БАЗА ДАННЫХ: 214 КЛЮЧЕЙ (исключительно из вашего списка)
    // Формат: [основной_символ, русское_название, альтернативные_формы]
    // Альтернативные формы используются только для отображения, но в вопросе показываем основной
    // --------------------------------------------------------------
    const KEYS_DATA = [
        ["一", "единица"],
        ["丨", "вертикальная"],
        ["丶", "точка"],
        ["丿", "откидная влево"],
        ["乙", "второй (цикличный знак)"],
        ["亅", "вертикальная с крюком"],
        ["二", "два"],
        ["亠", "горизонтальная с точкой"],
        ["人", "человек"],
        ["儿", "идущий человек"],
        ["入", "входить"],
        ["八", "восемь; делить"],
        ["冂", "границы"],
        ["冖", "крышка"],
        ["冫", "лёд"],
        ["几", "столик; несколько"],
        ["凵", "яма"],
        ["刀", "нож"],
        ["力", "сила"],
        ["勹", "обёртывать"],
        ["匕", "черпак; кинжал"],
        ["匚", "ящик; короб"],
        ["匸", "прятать"],
        ["十", "десять"],
        ["卜", "гадать"],
        ["卩", "печать; власть"],
        ["厂", "обрыв; круча"],
        ["厶", "частный; личный"],
        ["又", "правая рука; опять"],
        ["口", "рот"],
        ["囗", "окружать; ограда"],
        ["土", "земля"],
        ["士", "воин"],
        ["夂", "шагать вперед; продвигаться"],
        ["夊", "медленно идти; волочить ноги"],
        ["夕", "вечер"],
        ["大", "большой"],
        ["女", "женщина"],
        ["子", "ребёнок; сын"],
        ["宀", "крыша с точкой; крыша"],
        ["寸", "вершок"],
        ["小", "маленький"],
        ["尢", "хромой"],
        ["尸", "труп"],
        ["屮", "росток"],
        ["山", "гора"],
        ["川", "поток; река"],
        ["工", "работа"],
        ["己", "сам"],
        ["巾", "полотенце; салфетка"],
        ["干", "щит; вмешиваться"],
        ["幺", "незрелый; младший"],
        ["广", "навес"],
        ["廴", "двигаться вперед; тащить"],
        ["廾", "соединить руки"],
        ["弋", "стрелять из лука"],
        ["弓", "лук"],
        ["彐", "голова свиньи"],
        ["彡", "перья; длинная шерсть"],
        ["彳", "шаг (левой ногой)"],
        ["心", "сердце"],
        ["戈", "копье; клевец"],
        ["户", "двор"],
        ["手", "рука"],
        ["支", "ветка"],
        ["攴", "бить; ударять"],
        ["文", "текст; письмена"],
        ["斗", "ковш; хлебная мерка"],
        ["斤", "топор"],
        ["方", "квадрат; сторона"],
        ["无", "не; без"],
        ["日", "солнце"],
        ["曰", "говорить"],
        ["月", "луна"],
        ["木", "дерево"],
        ["欠", "недоставать"],
        ["止", "стопа; останавливаться"],
        ["歹", "злой; плохой"],
        ["殳", "бамбуковая пика"],
        ["毋", "нет; нельзя"],
        ["比", "сравнивать"],
        ["毛", "шерсть; волосы"],
        ["氏", "род; клан"],
        ["气", "воздух; газ"],
        ["水", "вода"],
        ["火", "огонь"],
        ["爪", "когти"],
        ["父", "отец"],
        ["爻", "воздействие; влияние"],
        ["爿", "доска; кровать"],
        ["片", "карточка; щепка"],
        ["牙", "зуб"],
        ["牛", "корова; бык"],
        ["犬", "собака"],
        ["玄", "темный; тайный"],
        ["玉", "яшма"],
        ["瓜", "дыня; тыква"],
        ["瓦", "черепица"],
        ["甘", "сладкий"],
        ["生", "рождаться; сырой"],
        ["用", "применять; использовать"],
        ["田", "поле"],
        ["疋", "нога; колено"],
        ["疒", "болезнь"],
        ["癶", "ноги врозь"],
        ["白", "белый"],
        ["皮", "кожа; шкура"],
        ["皿", "блюдо; посуда"],
        ["目", "глаз"],
        ["矛", "копье"],
        ["矢", "стрела"],
        ["石", "камень"],
        ["示", "алтарь; демонстрировать"],
        ["禸", "след зверя"],
        ["禾", "хлеб на корню"],
        ["穴", "пещера"],
        ["立", "стоять"],
        ["竹", "бамбук"],
        ["米", "рис"],
        ["糸", "нить; шелк"],
        ["缶", "глиняная посуда; керамика"],
        ["网", "сеть"],
        ["羊", "баран"],
        ["羽", "перья; крылья"],
        ["老", "старый"],
        ["而", "а; но"],
        ["耒", "плуг; соха"],
        ["耳", "ухо"],
        ["聿", "кисть для письма"],
        ["肉", "мясо"],
        ["臣", "подданный"],
        ["自", "сам; нос"],
        ["至", "достигать; прибывать"],
        ["臼", "ступа"],
        ["舌", "язык"],
        ["舛", "ошибка; неудача"],
        ["舟", "лодка; корабль"],
        ["艮", "твердый; крепкий"],
        ["色", "цвет"],
        ["艸", "трава"],
        ["虍", "тигр"],
        ["虫", "насекомое; ядовитая змея"],
        ["血", "кровь"],
        ["行", "идти; ряд"],
        ["衣", "одежда"],
        ["襾", "накрывать; крышка"],
        ["見", "видеть; смотреть"],
        ["角", "рог; угол"],
        ["言", "речь"],
        ["谷", "долина"],
        ["豆", "бобы"],
        ["豕", "свинья"],
        ["豸", "единорог"],
        ["貝", "раковина; сокровище"],
        ["赤", "красный"],
        ["走", "ходить; уходить"],
        ["足", "нога"],
        ["身", "тело (человека)"],
        ["車", "телега; повозка"],
        ["辛", "горький"],
        ["辰", "время (циклический знак)"],
        ["辵", "идти быстро"],
        ["邑", "город"],
        ["酉", "сосуд для вина"],
        ["釆", "различать; сортировать"],
        ["里", "верста; деревня"],
        ["金", "золото; металл"],
        ["長", "длинный; старший"],
        ["門", "ворота"],
        ["阜", "холм"],
        ["隶", "достигать; поймать"],
        ["隹", "короткохвостая птица"],
        ["雨", "дождь"],
        ["青", "синий; зелёный"],
        ["非", "не быть; отрицать"],
        ["面", "лицо"],
        ["革", "сырая кожа"],
        ["韋", "выделанная кожа"],
        ["韭", "дикий чеснок"],
        ["音", "звук"],
        ["頁", "страница"],
        ["風", "ветер"],
        ["飛", "летать"],
        ["食", "еда; пища"],
        ["首", "голова; глава"],
        ["香", "аромат"],
        ["馬", "лошадь"],
        ["骨", "кости"],
        ["高", "высокий"],
        ["髟", "волосы"],
        ["鬥", "борьба"],
        ["鬯", "жертвенное вино"],
        ["鬲", "кувшин; трипод"],
        ["鬼", "черт"],
        ["魚", "рыба"],
        ["鳥", "птица"],
        ["鹵", "соляная мель; солончак"],
        ["鹿", "олень"],
        ["麥", "пшеница"],
        ["麻", "конопля"],
        ["黃", "желтый"],
        ["黍", "просо"],
        ["黑", "черный"],
        ["黹", "вышивка"],
        ["黽", "лягушка; жаба"],
        ["鼎", "бронзовый треножник"],
        ["鼓", "барабан"],
        ["鼠", "мышь"],
        ["鼻", "нос"],
        ["齊", "ровный; одинаковый"],
        ["齒", "зубы"],
        ["龍", "дракон"],
        ["龜", "черепаха"],
        ["龠", "флейта"]
    ];

    // Преобразуем в удобный массив объектов
    const allKeys = KEYS_DATA.map(([symbol, meaning]) => ({ symbol, meaning }));

    // Игровое состояние
    let currentQuestion = { symbol: "", correctMeaning: "" };
    let currentOptions = [];
    let answered = false;
    let currentScore = 0;
    let totalQuestions = 0;
    let bestStreak = 0;

    // DOM элементы
    const currentKeySpan = document.getElementById("currentKey");
    const optionsContainer = document.getElementById("optionsContainer");
    const feedbackDiv = document.getElementById("feedbackMsg");
    const scoreSpan = document.getElementById("scoreValue");
    const totalAskedSpan = document.getElementById("totalAsked");
    const bestStreakSpan = document.getElementById("bestStreak");
    const nextBtn = document.getElementById("nextBtn");
    const resetBtn = document.getElementById("resetGameBtn");

    // Загрузка статистики из localStorage
    function loadStats() {
        const savedScore = localStorage.getItem("keyGame214_score");
        const savedTotal = localStorage.getItem("keyGame214_total");
        const savedBest = localStorage.getItem("keyGame214_best");
        if (savedScore !== null) currentScore = parseInt(savedScore);
        if (savedTotal !== null) totalQuestions = parseInt(savedTotal);
        if (savedBest !== null) bestStreak = parseInt(savedBest);
        updateStatsUI();
    }

    function saveStats() {
        localStorage.setItem("keyGame214_score", currentScore);
        localStorage.setItem("keyGame214_total", totalQuestions);
        localStorage.setItem("keyGame214_best", bestStreak);
    }

    function updateStatsUI() {
        scoreSpan.innerText = currentScore;
        totalAskedSpan.innerText = totalQuestions;
        bestStreakSpan.innerText = bestStreak;
    }

    // Генерация случайного ключа
    function getRandomKey() {
        const randomIndex = Math.floor(Math.random() * allKeys.length);
        return { symbol: allKeys[randomIndex].symbol, meaning: allKeys[randomIndex].meaning };
    }

    // Генерация 3 случайных неправильных значений
    function getRandomDistractors(correctMeaning, count = 3) {
        const distractors = new Set();
        const otherMeanings = allKeys.filter(k => k.meaning !== correctMeaning).map(k => k.meaning);
        
        while (distractors.size < count && otherMeanings.length > 0) {
            const rand = otherMeanings[Math.floor(Math.random() * otherMeanings.length)];
            distractors.add(rand);
        }
        
        return Array.from(distractors);
    }

    // Создание нового вопроса
    function generateNewQuestion() {
        const { symbol, meaning } = getRandomKey();
        currentQuestion = { symbol: symbol, correctMeaning: meaning };
        const wrongOptions = getRandomDistractors(meaning, 3);
        currentOptions = [meaning, ...wrongOptions];
        
        // Перемешиваем варианты
        for (let i = currentOptions.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [currentOptions[i], currentOptions[j]] = [currentOptions[j], currentOptions[i]];
        }
        
        answered = false;
        renderQuestionUI();
    }

    function renderQuestionUI() {
        currentKeySpan.innerText = currentQuestion.symbol;
        optionsContainer.innerHTML = "";
        
        currentOptions.forEach(opt => {
            const btn = document.createElement("button");
            btn.className = "option-btn";
            btn.innerText = opt;
            btn.addEventListener("click", () => handleAnswer(opt, btn));
            optionsContainer.appendChild(btn);
        });
        
        feedbackDiv.innerHTML = "🤔 выберите значение ключа";
        feedbackDiv.style.background = "#fef7e0";
        feedbackDiv.style.color = "#b46f3a";
        nextBtn.disabled = false;
        nextBtn.style.opacity = "1";
    }

    // Обработка ответа
    function handleAnswer(selected, btnElement) {
        if (answered) {
            feedbackDiv.innerHTML = "⏳ уже отвечено! нажми 'следующий ключ'";
            return;
        }
        
        answered = true;
        totalQuestions++;
        const isCorrect = (selected === currentQuestion.correctMeaning);
        
        if (isCorrect) {
            currentScore++;
            feedbackDiv.innerHTML = `✅ Верно! «${currentQuestion.symbol}» — это ${currentQuestion.correctMeaning}. +1 очко`;
            feedbackDiv.style.background = "#d9f0e0";
            feedbackDiv.style.color = "#1f6e43";
        } else {
            feedbackDiv.innerHTML = `❌ Ошибка. «${currentQuestion.symbol}» — это ${currentQuestion.correctMeaning}. Вы выбрали: ${selected}`;
            feedbackDiv.style.background = "#ffe0d4";
            feedbackDiv.style.color = "#bc5a3c";
        }

        // Подсветка кнопок
        const allOptionsBtns = document.querySelectorAll(".option-btn");
        allOptionsBtns.forEach(btn => {
            btn.disabled = true;
            if (btn.innerText === currentQuestion.correctMeaning) {
                btn.classList.add("option-correct");
            }
            if (btn.innerText === selected && !isCorrect) {
                btn.classList.add("option-wrong");
            }
        });

        // Обновляем лучший результат
        if (currentScore > bestStreak) {
            bestStreak = currentScore;
        }
        
        updateStatsUI();
        saveStats();
    }

    function resetGame() {
        if (confirm("Сбросить всю статистику и начать сначала?")) {
            currentScore = 0;
            totalQuestions = 0;
            bestStreak = 0;
            updateStatsUI();
            saveStats();
            generateNewQuestion();
            feedbackDiv.innerHTML = "✨ Статистика сброшена. Начинаем новую игру!";
            feedbackDiv.style.background = "#eef3ea";
        }
    }

    function loadNextQuestion() {
        if (!answered) {
            feedbackDiv.innerHTML = "⚠️ сначала ответьте на текущий вопрос!";
            feedbackDiv.style.background = "#ffe6c7";
            return;
        }
        generateNewQuestion();
    }

    // Инициализация
    function initGame() {
        loadStats();
        generateNewQuestion();
        nextBtn.addEventListener("click", loadNextQuestion);
        resetBtn.addEventListener("click", resetGame);
    }

    initGame();
</script>
</body>
</html>
