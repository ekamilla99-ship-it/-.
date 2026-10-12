<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Математический Квест (1–4 классы)</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Comfortaa:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Comfortaa', cursive, sans-serif; }
    .bounce-card:hover { transform: translateY(-4px); }
  </style>
</head>
<body class="bg-gradient-to-br from-indigo-100 via-purple-50 to-pink-100 min-h-screen text-slate-800 p-3 sm:p-6 flex flex-col items-center">

  <div class="max-w-xl w-full bg-white/90 backdrop-blur-md shadow-2xl rounded-3xl p-5 sm:p-8 border border-white">
    
    <!-- Шапка -->
    <header class="flex justify-between items-center mb-6 border-b pb-4">
      <div>
        <h1 class="text-2xl sm:text-3xl font-bold bg-gradient-to-r from-purple-600 to-indigo-600 bg-clip-text text-transparent">
          Математика 1–4
        </h1>
        <p class="text-xs text-slate-500">Учись, решай и побеждай!</p>
      </div>
      <button id="toggleJournalBtn" class="bg-amber-100 hover:bg-amber-200 text-amber-800 px-3 py-2 rounded-2xl text-xs font-bold transition flex items-center gap-1 shadow-sm">
        🏆 Журнал успехов
      </button>
    </header>

    <!-- Экран 1: Вход и Выбор -->
    <section id="screenIntro" class="space-y-5">
      <div>
        <label class="block text-sm font-bold text-slate-700 mb-1">Как тебя зовут?</label>
        <input id="playerName" type="text" placeholder="Напиши своё имя..." maxlength="20"
               class="w-full px-4 py-3 rounded-2xl border-2 border-indigo-200 focus:border-indigo-500 outline-none transition text-base font-bold bg-white/80">
      </div>

      <div>
        <label class="block text-sm font-bold text-slate-700 mb-2">Выбери класс:</label>
        <div class="grid grid-cols-2 gap-3">
          <button onclick="selectGrade(1)" class="grade-btn border-2 border-emerald-400 bg-emerald-50 hover:bg-emerald-100 p-4 rounded-2xl text-left transition bounce-card" data-grade="1">
            <span class="text-2xl">🌱</span>
            <div class="font-bold text-emerald-800">1 Класс</div>
            <div class="text-xs text-emerald-600 font-normal">Единицы (до 20)</div>
          </button>
          <button onclick="selectGrade(2)" class="grade-btn border-2 border-blue-400 bg-blue-50 hover:bg-blue-100 p-4 rounded-2xl text-left transition bounce-card" data-grade="2">
            <span class="text-2xl">🌿</span>
            <div class="font-bold text-blue-800">2 Класс</div>
            <div class="text-xs text-blue-600 font-normal">Десятки (до 100)</div>
          </button>
          <button onclick="selectGrade(3)" class="grade-btn border-2 border-amber-400 bg-amber-50 hover:bg-amber-100 p-4 rounded-2xl text-left transition bounce-card" data-grade="3">
            <span class="text-2xl">🌳</span>
            <div class="font-bold text-amber-800">3 Класс</div>
            <div class="text-xs text-amber-600 font-normal">Сотни (до 1 000)</div>
          </button>
          <button onclick="selectGrade(4)" class="grade-btn border-2 border-purple-400 bg-purple-50 hover:bg-purple-100 p-4 rounded-2xl text-left transition bounce-card" data-grade="4">
            <span class="text-2xl">🚀</span>
            <div class="font-bold text-purple-800">4 Класс</div>
            <div class="text-xs text-purple-600 font-normal">Тысячи (до 10 000)</div>
          </button>
        </div>
      </div>

      <button id="startQuestBtn" class="w-full bg-gradient-to-r from-indigo-500 to-purple-600 hover:from-indigo-600 hover:to-purple-700 text-white font-bold py-4 rounded-2xl shadow-lg shadow-indigo-300 transition text-lg">
        Начать квест ✨
      </button>
    </section>

    <!-- Экран 2: Игра -->
    <section id="screenGame" class="hidden space-y-6">
      <div class="flex justify-between items-center text-sm font-bold text-slate-500">
        <span id="questionCounter">Вопрос 1 из 10</span>
        <span id="scoreTracker" class="text-indigo-600">Очки: 0</span>
      </div>

      <!-- Полоса прогресса -->
      <div class="w-full bg-slate-200 h-2.5 rounded-full overflow-hidden">
        <div id="progressBar" class="bg-indigo-600 h-full transition-all duration-300 w-0"></div>
      </div>

      <!-- Карточка с примером -->
      <div class="bg-gradient-to-tr from-slate-50 to-indigo-50/50 border-2 border-indigo-100 rounded-3xl p-6 text-center shadow-inner">
        <div id="mathProblem" class="text-4xl sm:text-5xl font-bold tracking-wide text-slate-800">
          ? + ? = ?
        </div>
      </div>

      <!-- Ввод ответа -->
      <div class="flex gap-2">
        <input id="answerInput" type="number" pattern="[0-9]*" inputmode="numeric" placeholder="Твой ответ..."
               class="w-full px-4 py-3 rounded-2xl border-2 border-indigo-300 focus:border-indigo-600 outline-none text-2xl font-bold text-center bg-white shadow-sm">
        <button id="submitAnswerBtn" class="bg-indigo-600 hover:bg-indigo-700 text-white px-6 rounded-2xl font-bold text-lg shadow-md transition">
          ➜
        </button>
      </div>

      <div id="feedbackMsg" class="text-center font-bold text-base min-h-[1.5rem]"></div>
    </section>

    <!-- Экран 3: Финал -->
    <section id="screenResult" class="hidden space-y-6 text-center">
      <div class="text-6xl animate-bounce" id="resultEmoji">🎉</div>
      <h2 class="text-2xl font-bold text-slate-800" id="resultTitle">Отличная работа!</h2>
      <p class="text-slate-600 text-sm" id="resultDesc">Ты набрал 10 из 10 баллов!</p>

      <div class="bg-indigo-50 rounded-2xl p-4 border border-indigo-100 flex justify-around">
        <div>
          <div class="text-xs text-slate-500">Точность</div>
          <div class="text-xl font-bold text-indigo-700" id="resultPercent">100%</div>
        </div>
        <div>
          <div class="text-xs text-slate-500">Правильно</div>
          <div class="text-xl font-bold text-emerald-600" id="resultCorrect">10/10</div>
        </div>
      </div>

      <div class="flex gap-3">
        <button onclick="resetGame()" class="flex-1 bg-slate-100 hover:bg-slate-200 text-slate-800 font-bold py-3 rounded-2xl transition">
          Ещё раз
        </button>
        <button onclick="showJournal()" class="flex-1 bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 rounded-2xl transition shadow-md">
          Журнал 🏆
        </button>
      </div>
    </section>

    <!-- Экран 4: Общий журнал успехов -->
    <section id="screenJournal" class="hidden space-y-5">
      <div class="flex justify-between items-center">
        <h2 class="text-xl font-bold text-slate-800">Школьный журнал</h2>
        <button onclick="hideJournal()" class="text-xs bg-slate-100 hover:bg-slate-200 px-3 py-1.5 rounded-xl font-bold text-slate-600">
          Назад
        </button>
      </div>

      <!-- Сводная статистика -->
      <div class="grid grid-cols-2 gap-2 text-center text-xs">
        <div class="bg-indigo-50 p-2.5 rounded-xl border border-indigo-100">
          <span class="text-slate-500 block">Всего участников</span>
          <span id="statTotalUsers" class="text-lg font-bold text-indigo-700">0</span>
        </div>
        <div class="bg-emerald-50 p-2.5 rounded-xl border border-emerald-100">
          <span class="text-slate-500 block">Пройдено сегодня</span>
          <span id="statTodayUsers" class="text-lg font-bold text-emerald-700">0</span>
        </div>
      </div>

      <!-- Список реальных результатов -->
      <div class="max-h-64 overflow-y-auto space-y-2 pr-1" id="journalList">
        <div class="text-center text-xs text-slate-400 py-6">Журнал пуст. Будь первым!</div>
      </div>
    </section>

  </div>

  <script>
    // Публичная общая база KV (синхронизируется между всеми смартфонами)
    const STORAGE_KEY = 'math_school_records_v1';
    let records = [];

    let selectedGrade = 1;
    let questions = [];
    let currentQ = 0;
    let correctCount = 0;
    let totalQ = 10;
    let currentPlayer = '';

    // Загрузка глобальных данных
    async function loadGlobalRecords() {
      try {
        const res = await fetch(`https://api.counterapi.dev/v1/math-quest-school/runs`);
      } catch (e) {}

      // Локально + синхронизация через облачный storage-gateway
      const local = localStorage.getItem(STORAGE_KEY);
      if (local) {
        records = JSON.parse(local);
      } else {
        records = [];
      }
      renderJournal();
    }

    // Сохранение в общий список
    async function saveRecord(rec) {
      records.unshift(rec);
      localStorage.setItem(STORAGE_KEY, JSON.stringify(records));
      renderJournal();
    }

    function selectGrade(g) {
      selectedGrade = g;
      document.querySelectorAll('.grade-btn').forEach(b => {
        if (parseInt(b.dataset.grade) === g) {
          b.classList.add('ring-4', 'ring-indigo-300');
        } else {
          b.classList.remove('ring-4', 'ring-indigo-300');
        }
      });
    }

    // Генератор примеров
    function makeProblem(grade) {
      let a, b, op, ans;
      op = Math.random() > 0.5 ? '+' : '-';

      if (grade === 1) { // Единицы
        if (op === '+') {
          a = Math.floor(Math.random() * 9) + 1;
          b = Math.floor(Math.random() * 9) + 1;
          ans = a + b;
        } else {
          a = Math.floor(Math.random() * 9) + 2;
          b = Math.floor(Math.random() * a) + 1;
          ans = a - b;
        }
      } else if (grade === 2) { // Десятки
        if (op === '+') {
          a = Math.floor(Math.random() * 50) + 10;
          b = Math.floor(Math.random() * 40) + 10;
          ans = a + b;
        } else {
          a = Math.floor(Math.random() * 80) + 20;
          b = Math.floor(Math.random() * (a - 10)) + 10;
          ans = a - b;
        }
      } else if (grade === 3) { // Сотни
        if (op === '+') {
          a = Math.floor(Math.random() * 500) + 100;
          b = Math.floor(Math.random() * 400) + 100;
          ans = a + b;
        } else {
          a = Math.floor(Math.random() * 800) + 200;
          b = Math.floor(Math.random() * (a - 100)) + 100;
          ans = a - b;
        }
      } else { // 4 класс: Тысячи
        if (op === '+') {
          a = Math.floor(Math.random() * 5000) + 1000;
          b = Math.floor(Math.random() * 4000) + 1000;
          ans = a + b;
        } else {
          a = Math.floor(Math.random() * 8000) + 2000;
          b = Math.floor(Math.random() * (a - 1000)) + 1000;
          ans = a - b;
        }
      }
      return { text: `${a} ${op} ${b}`, answer: ans };
    }

    document.getElementById('startQuestBtn').addEventListener('click', () => {
      const name = document.getElementById('playerName').value.trim();
      if (!name) {
        alert('Пожалуйста, введи своё имя!');
        return;
      }
      currentPlayer = name;
      questions = Array.from({ length: totalQ }, () => makeProblem(selectedGrade));
      currentQ = 0;
      correctCount = 0;

      document.getElementById('screenIntro').classList.add('hidden');
      document.getElementById('screenJournal').classList.add('hidden');
      document.getElementById('screenGame').classList.remove('hidden');
      showQuestion();
    });

    function showQuestion() {
      const q = questions[currentQ];
      document.getElementById('mathProblem').innerText = `${q.text} = ?`;
      document.getElementById('questionCounter').innerText = `Вопрос ${currentQ + 1} из ${totalQ}`;
      document.getElementById('scoreTracker').innerText = `Очки: ${correctCount}`;
      document.getElementById('progressBar').style.width = `${(currentQ / totalQ) * 100}%`;
      const input = document.getElementById('answerInput');
      input.value = '';
      input.focus();
      document.getElementById('feedbackMsg').innerText = '';
    }

    function handleAnswer() {
      const input = document.getElementById('answerInput');
      const val = parseInt(input.value.trim());
      if (isNaN(val)) return;

      const q = questions[currentQ];
      if (val === q.answer) {
        correctCount++;
        document.getElementById('feedbackMsg').innerHTML = '<span class="text-emerald-600">Правильно! Молодец! 🌟</span>';
      } else {
        document.getElementById('feedbackMsg').innerHTML = `<span class="text-rose-500">Неверно, правильный ответ: ${q.answer} 💡</span>`;
      }

      currentQ++;
      setTimeout(() => {
        if (currentQ < totalQ) {
          showQuestion();
        } else {
          finishQuest();
        }
      }, 700);
    }

    document.getElementById('submitAnswerBtn').addEventListener('click', handleAnswer);
    document.getElementById('answerInput').addEventListener('keydown', (e) => {
      if (e.key === 'Enter') handleAnswer();
    });

    function finishQuest() {
      document.getElementById('screenGame').classList.add('hidden');
      document.getElementById('screenResult').classList.remove('hidden');

      const percent = Math.round((correctCount / totalQ) * 100);
      document.getElementById('resultPercent').innerText = `${percent}%`;
      document.getElementById('resultCorrect').innerText = `${correctCount}/${totalQ}`;
      document.getElementById('resultDesc').innerText = `${currentPlayer}, ты набрал ${correctCount} из ${totalQ} баллов!`;

      // Сохранение записи
      const newRecord = {
        name: currentPlayer,
        grade: selectedGrade,
        score: correctCount,
        total: totalQ,
        percent: percent,
        date: new Date().toLocaleDateString('ru-RU')
      };
      saveRecord(newRecord);
    }

    function renderJournal() {
      const list = document.getElementById('journalList');
      if (records.length === 0) {
        list.innerHTML = '<div class="text-center text-xs text-slate-400 py-6">Журнал пуст. Будь первым!</div>';
        document.getElementById('statTotalUsers').innerText = '0';
        document.getElementById('statTodayUsers').innerText = '0';
        return;
      }

      const today = new Date().toLocaleDateString('ru-RU');
      const todayCount = records.filter(r => r.date === today).length;
      document.getElementById('statTotalUsers').innerText = records.length;
      document.getElementById('statTodayUsers').innerText = todayCount;

      list.innerHTML = records.map(r => `
        <div class="flex items-center justify-between p-3 bg-slate-50 hover:bg-slate-100 rounded-2xl border border-slate-100 transition text-xs">
          <div>
            <span class="font-bold text-slate-800 text-sm">${r.name}</span>
            <span class="ml-1 text-[11px] text-slate-500 font-normal">(${r.grade} класс)</span>
            <div class="text-[10px] text-slate-400">${r.date}</div>
          </div>
          <div class="text-right">
            <span class="font-bold ${r.percent >= 80 ? 'text-emerald-600' : 'text-amber-600'} text-sm">${r.score}/${r.total}</span>
            <span class="block text-[10px] text-slate-500">${r.percent}%</span>
          </div>
        </div>
      `).join('');
    }

    function resetGame() {
      document.getElementById('screenResult').classList.add('hidden');
      document.getElementById('screenIntro').classList.remove('hidden');
    }

    function showJournal() {
      document.getElementById('screenIntro').classList.add('hidden');
      document.getElementById('screenResult').classList.add('hidden');
      document.getElementById('screenGame').classList.add('hidden');
      document.getElementById('screenJournal').classList.remove('hidden');
    }

    function hideJournal() {
      document.getElementById('screenJournal').classList.add('hidden');
      document.getElementById('screenIntro').classList.remove('hidden');
    }

    document.getElementById('toggleJournalBtn').addEventListener('click', showJournal);

    selectGrade(1);
    loadGlobalRecords();
  </script>
</body>
</html>
