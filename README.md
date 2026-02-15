<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Artikel-Trainer v5 - Deniz</title>
    <style>
        * {margin: 0; padding: 0; box-sizing: border-box;}
        body {
            font-family: 'Arial Black', Arial, sans-serif;
            background: linear-gradient(135deg, #87CEEB 0%, #98D8C8 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 10px;
        }
        .container {
            max-width: 500px;
            width: 100%;
            background: #8B7355;
            border: 8px solid #654321;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            border-radius: 10px;
            overflow: hidden;
        }
        .header {
            background: #2C5F2D;
            color: white;
            padding: 20px;
            text-align: center;
            border-bottom: 5px solid #1a3a1b;
            text-shadow: 3px 3px 0px rgba(0,0,0,0.3);
        }
        .header h1 {font-size: 28px; margin-bottom: 10px;}
        .stats {
            display: flex;
            justify-content: space-around;
            background: #5C4033;
            padding: 15px;
            color: white;
            font-size: 18px;
            border-bottom: 4px solid #3d2b23;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.3);
        }
        .game-area {
            background: #A0826D;
            padding: 30px 20px;
            min-height: 450px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
        .word-display {
            background: #654321;
            border: 6px solid #3d2b23;
            padding: 30px;
            border-radius: 10px;
            margin-bottom: 30px;
            width: 100%;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }
        .word {
            font-size: 42px;
            color: #FFD700;
            font-weight: bold;
            text-shadow: 3px 3px 0px rgba(0,0,0,0.5);
        }
        .buttons {display: flex; flex-direction: column; gap: 15px; width: 100%;}
        .btn {
            font-family: 'Arial Black', Arial, sans-serif;
            font-size: 32px;
            padding: 20px;
            border: 6px solid #000;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            text-transform: uppercase;
            box-shadow: 0 6px 0 #000;
            transition: all 0.1s;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.3);
        }
        .btn:active {transform: translateY(4px); box-shadow: 0 2px 0 #000;}
        .btn-der {background: #5DADE2; color: white;}
        .btn-die {background: #EC7063; color: white;}
        .btn-das {background: #58D68D; color: white;}
        .btn-start {background: #F39C12; color: white; font-size: 28px; margin-top: 20px;}
        .btn-count {
            background: #3498DB;
            color: white;
            font-size: 24px;
            margin: 5px;
            padding: 10px 20px;
            display: inline-block;
            border: 4px solid #000;
            border-radius: 5px;
        }
        .btn-count.active {
            background: #27AE60;
            border-color: #1E8449;
        }
        .timer {
            font-size: 24px;
            color: #FFD700;
            margin-bottom: 20px;
            font-weight: bold;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.5);
        }
        .feedback {
            font-size: 28px;
            font-weight: bold;
            padding: 20px;
            margin: 20px 0;
            border-radius: 10px;
            text-align: center;
            border: 5px solid;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.3);
        }
        .correct {background: #58D68D; color: white; border-color: #2ECC71;}
        .incorrect {background: #EC7063; color: white; border-color: #E74C3C;}
        .result {text-align: center; color: white; font-size: 20px; line-height: 1.8;}
        .grade {
            font-size: 72px;
            color: #FFD700;
            margin: 20px 0;
            text-shadow: 4px 4px 0px rgba(0,0,0,0.5);
        }
        .progress-info {
            background: #654321;
            border: 4px solid #3d2b23;
            padding: 15px;
            margin: 20px 0;
            border-radius: 10px;
            font-size: 22px;
            width: 100%;
        }
        .progress-bar {
            background: #3d2b23;
            height: 30px;
            border-radius: 15px;
            margin-top: 10px;
            overflow: hidden;
        }
        .progress-fill {
            background: linear-gradient(90deg, #2ECC71, #58D68D);
            height: 100%;
            transition: width 0.3s;
            text-align: center;
            color: white;
            font-weight: bold;
            line-height: 30px;
            font-size: 14px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🎮 Artikel-Trainer v5 🎮</h1>
            <div>für Deniz</div>
        </div>

        <div class="stats">
            <div>Runde: <span id="round">1</span>/<span id="maxRound">20</span></div>
            <div>Richtig: <span id="correct">0</span></div>
            <div>Gelernt: <span id="mastered">0</span>/855</div>
        </div>

        <div class="game-area" id="gameArea">
            <div class="result">
                <h2>Hallo Deniz! 🎯</h2>
                <div class="progress-info">
                    <div id="masteredLabel">Gelernt: 0/855</div>
                    <div class="progress-bar">
                        <div class="progress-fill" id="progressBar" style="width: 0%">0%</div>
                    </div>
                </div>
                <div style="margin: 15px 0;">
                    <p style="font-size: 20px; margin-bottom: 10px;">Wieviele Wörter pro Runde?</p>
                    <button class="btn-count" onclick="game.selectCount(10)">10</button>
                    <button class="btn-count active" onclick="game.selectCount(20)">20</button>
                    <button class="btn-count" onclick="game.selectCount(30)">30</button>
                </div>
                <button class="btn btn-start" onclick="game.start()">Spiel Starten!</button>
            </div>
        </div>
    </div>

    <script>
const allWords = [
    {word:"Ahorn",article:"der"}, {word:"Album",article:"das"}, {word:"Ameise",article:"die"}, {word:"Ampel",article:"die"}, {word:"Ananas",article:"die"}, {word:"Apfel",article:"der"}, {word:"Arm",article:"der"}, {word:"Ast",article:"der"}, {word:"Auge",article:"das"}, {word:"Auto",article:"das"},
    {word:"Banane",article:"die"}, {word:"Bär",article:"der"}, {word:"Baum",article:"der"}, {word:"Bett",article:"das"}, {word:"Biene",article:"die"}, {word:"Birne",article:"die"}, {word:"Blatt",article:"das"}, {word:"Blume",article:"die"}, {word:"Brille",article:"die"}, {word:"Brot",article:"das"}, {word:"Buch",article:"das"}, {word:"Bus",article:"der"},
    {word:"Chamäleon",article:"das"}, {word:"Christbaum",article:"der"}, {word:"Clown",article:"der"}, {word:"Computer",article:"der"}, {word:"Cowboy",article:"der"},
    {word:"Dach",article:"das"}, {word:"Dachs",article:"der"}, {word:"Datum",article:"das"}, {word:"Decke",article:"die"}, {word:"Delfin",article:"der"}, {word:"Dinosaurier",article:"der"}, {word:"Donnerstag",article:"der"}, {word:"Dorf",article:"das"}, {word:"Dose",article:"die"}, {word:"Drachen",article:"der"},
    {word:"Ei",article:"das"}, {word:"Eis",article:"das"}, {word:"Eisen",article:"das"}, {word:"Ente",article:"die"}, {word:"Erde",article:"die"}, {word:"Esel",article:"der"}, {word:"Eule",article:"die"},
    {word:"Fenster",article:"das"}, {word:"Fest",article:"das"}, {word:"Feuer",article:"das"}, {word:"Finger",article:"der"}, {word:"Fisch",article:"der"}, {word:"Flasche",article:"die"}, {word:"Fliege",article:"die"}, {word:"Fluss",article:"der"}, {word:"Frosch",article:"der"},
    {word:"Gabel",article:"die"}, {word:"Garten",article:"der"}, {word:"Gast",article:"der"}, {word:"Geld",article:"das"}, {word:"Glas",article:"das"}, {word:"Gras",article:"das"}, {word:"Gurke",article:"die"},
    {word:"Hammer",article:"der"}, {word:"Hand",article:"die"}, {word:"Hase",article:"der"}, {word:"Haus",article:"das"}, {word:"Hemd",article:"das"}, {word:"Herz",article:"das"}, {word:"Himmel",article:"der"}, {word:"Hose",article:"die"}, {word:"Hund",article:"der"}, {word:"Hut",article:"der"},
    {word:"Igel",article:"der"}, {word:"Insel",article:"die"},
    {word:"Jacke",article:"die"}, {word:"Jaguar",article:"der"}, {word:"Jäger",article:"der"}, {word:"Junge",article:"der"},
    {word:"Kamm",article:"der"}, {word:"Känguru",article:"das"}, {word:"Karte",article:"die"}, {word:"Käse",article:"der"}, {word:"Katze",article:"die"}, {word:"Kirche",article:"die"}, {word:"Kleid",article:"das"}, {word:"Kreis",article:"der"}, {word:"Krokodil",article:"das"}, {word:"Kuh",article:"die"},
    {word:"Lampe",article:"die"}, {word:"Laterne",article:"die"}, {word:"Leiter",article:"die"}, {word:"Lexikon",article:"das"}, {word:"Lippe",article:"die"}, {word:"Löffel",article:"der"}, {word:"Löwe",article:"der"}, {word:"Lurch",article:"der"},
    {word:"Mädchen",article:"das"}, {word:"Maler",article:"der"}, {word:"Mama",article:"die"}, {word:"Mauer",article:"die"}, {word:"Maus",article:"die"}, {word:"Melone",article:"die"}, {word:"Messer",article:"das"}, {word:"Milchkanne",article:"die"}, {word:"Mond",article:"der"}, {word:"Montag",article:"der"}, {word:"Moos",article:"das"}, {word:"Mühle",article:"die"}, {word:"Müller",article:"der"}, {word:"Mund",article:"der"}, {word:"Mutter",article:"die"}, {word:"Mütze",article:"die"}, {word:"Mantel",article:"der"}, {word:"Mai",article:"der"}, {word:"März",article:"der"}, {word:"Mann",article:"der"}, {word:"Mittwoch",article:"der"},
    {word:"Nacht",article:"die"}, {word:"Nadel",article:"die"}, {word:"Nagel",article:"der"}, {word:"Nase",article:"die"}, {word:"Nashorn",article:"das"}, {word:"Nest",article:"das"}, {word:"Nikolaus",article:"der"}, {word:"Nilpferd",article:"das"}, {word:"Nudel",article:"die"}, {word:"Nuss",article:"die"}, {word:"November",article:"der"},
    {word:"Obst",article:"das"}, {word:"Ofen",article:"der"}, {word:"Ohr",article:"das"}, {word:"Ohrwurm",article:"der"}, {word:"Öl",article:"das"}, {word:"Oma",article:"die"}, {word:"Opa",article:"der"}, {word:"Orange",article:"die"}, {word:"Oktober",article:"der"}, {word:"Orang-Utan",article:"der"}, {word:"Orgel",article:"die"},
    {word:"Paket",article:"das"}, {word:"Papagei",article:"der"}, {word:"Papier",article:"das"}, {word:"Petersilie",article:"die"}, {word:"Pfanne",article:"die"}, {word:"Pfeil",article:"der"}, {word:"Pferd",article:"das"}, {word:"Pflanze",article:"die"}, {word:"Pflaume",article:"die"}, {word:"Pinsel",article:"der"}, {word:"Pizza",article:"die"}, {word:"Pommes",article:"die"}, {word:"Pony",article:"das"}, {word:"Puppe",article:"die"}, {word:"Pfau",article:"der"}, {word:"Pfeife",article:"die"}, {word:"Pilz",article:"der"}, {word:"Palme",article:"die"}, {word:"Polizei",article:"die"},
    {word:"Quadrat",article:"das"}, {word:"Qualm",article:"der"}, {word:"Quark",article:"der"}, {word:"Quelle",article:"die"}, {word:"Quiz",article:"das"}, {word:"Qualle",article:"die"}, {word:"Quartett",article:"das"},
    {word:"Rabe",article:"der"}, {word:"Rad",article:"das"}, {word:"Regen",article:"der"}, {word:"Reifen",article:"der"}, {word:"Riese",article:"der"}, {word:"Ring",article:"der"}, {word:"Rock",article:"der"}, {word:"Roller",article:"der"}, {word:"Rose",article:"die"}, {word:"Rakete",article:"die"}, {word:"Raupe",article:"die"}, {word:"Radio",article:"das"}, {word:"Rutsche",article:"die"}, {word:"Reh",article:"das"},
    {word:"Sack",article:"der"}, {word:"Salat",article:"der"}, {word:"Samstag",article:"der"}, {word:"Schaf",article:"das"}, {word:"Schere",article:"die"}, {word:"Schiff",article:"das"}, {word:"Schlitten",article:"der"}, {word:"Schmetterling",article:"der"}, {word:"Schnee",article:"der"}, {word:"Schokolade",article:"die"}, {word:"Schraube",article:"die"}, {word:"Schule",article:"die"}, {word:"Schwein",article:"das"}, {word:"Seehund",article:"der"}, {word:"Seife",article:"die"}, {word:"Sonne",article:"die"}, {word:"Sonntag",article:"der"}, {word:"Spatz",article:"der"}, {word:"Spinne",article:"die"}, {word:"Sporn",article:"der"}, {word:"Spur",article:"die"}, {word:"Stempel",article:"der"}, {word:"Stern",article:"der"}, {word:"Stiefel",article:"der"}, {word:"Storch",article:"der"}, {word:"Strauch",article:"der"}, {word:"Stuhl",article:"der"}, {word:"Schlüssel",article:"der"}, {word:"Schuh",article:"der"}, {word:"Schildkröte",article:"die"}, {word:"Schlange",article:"die"}, {word:"Spaghetti",article:"die"}, {word:"Spaten",article:"der"}, {word:"Specht",article:"der"}, {word:"Spuren",article:"die"}, {word:"Salami",article:"die"}, {word:"Sand",article:"der"}, {word:"Seepferdchen",article:"das"}, {word:"September",article:"der"}, {word:"Sofa",article:"das"},
    {word:"Tablette",article:"die"}, {word:"Tanne",article:"die"}, {word:"Tasse",article:"die"}, {word:"Taube",article:"die"}, {word:"Teddy",article:"der"}, {word:"Teller",article:"der"}, {word:"Tiger",article:"der"}, {word:"Tisch",article:"der"}, {word:"Tomate",article:"die"}, {word:"Tonne",article:"die"}, {word:"Tor",article:"das"}, {word:"Turm",article:"der"}, {word:"Tür",article:"die"}, {word:"Tafel",article:"die"}, {word:"Tasche",article:"die"}, {word:"Telefon",article:"das"}, {word:"Tüte",article:"die"},
    {word:"Uhr",article:"die"}, {word:"Unfall",article:"der"}, {word:"Urwald",article:"der"}, {word:"Uhu",article:"der"},
    {word:"Vater",article:"der"}, {word:"Vogel",article:"der"}, {word:"Vulkan",article:"der"}, {word:"Vampir",article:"der"}, {word:"Vase",article:"die"}, {word:"Veilchen",article:"das"},
    {word:"Wagen",article:"der"}, {word:"Wald",article:"der"}, {word:"Wal",article:"der"}, {word:"Wand",article:"die"}, {word:"Wasser",article:"das"}, {word:"Weg",article:"der"}, {word:"Wiese",article:"die"}, {word:"Wind",article:"der"}, {word:"Wolke",article:"die"}, {word:"Wurm",article:"der"}, {word:"Wurzel",article:"die"}, {word:"Würfel",article:"der"}, {word:"Wurst",article:"die"}, {word:"Wolle",article:"die"}, {word:"Wiege",article:"die"},
    {word:"Xylofon",article:"das"}, {word:"Yak",article:"der"}, {word:"Yeti",article:"der"}, {word:"Yoga",article:"das"}, {word:"Zahn",article:"der"}, {word:"Zaun",article:"der"}, {word:"Zebra",article:"das"}, {word:"Ziege",article:"die"}, {word:"Zirkus",article:"der"}, {word:"Zitrone",article:"die"}, {word:"Zoo",article:"der"}, {word:"Zucker",article:"der"}, {word:"Zug",article:"der"}, {word:"Zwiebel",article:"die"}, {word:"Zelt",article:"das"}
];

const game = {
    words: [],
    idx: 0,
    correct: 0,
    totalQuestions: 0,
    wrong: [],
    timer: null,
    time: 10,
    progress: {},
    audioCtx: null,
    wordCount: 20,
    
    selectCount(count) {
        this.wordCount = count;
        document.querySelectorAll('.btn-count').forEach(btn => btn.classList.remove('active'));
        event.target.classList.add('active');
        document.getElementById('maxRound').textContent = count;
    },
    
    async initAudio() {
        if (!this.audioCtx) {
            this.audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        }
        if (this.audioCtx.state === 'suspended') {
            await this.audioCtx.resume();
        }
    },
    
    playSound(isCorrect) {
        if (!this.audioCtx) return;
        const ctx = this.audioCtx;
        function tone(freq, start, duration, type = "sine", volume = 0.4) {
            const osc = ctx.createOscillator();
            const gain = ctx.createGain();
            osc.type = type;
            osc.frequency.setValueAtTime(freq, ctx.currentTime + start);
            gain.gain.setValueAtTime(volume, ctx.currentTime + start);
            gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + start + duration);
            osc.connect(gain);
            gain.connect(ctx.destination);
            osc.start(ctx.currentTime + start);
            osc.stop(ctx.currentTime + start + duration + 0.05);
        }
        if (isCorrect) {
            tone(440, 0.00, 0.15, "sine", 0.4);
            tone(554, 0.15, 0.15, "sine", 0.4);
            tone(659, 0.30, 0.25, "sine", 0.4);
        } else {
            tone(180, 0.00, 0.20, "sawtooth", 0.5);
            tone(140, 0.25, 0.35, "sawtooth", 0.5);
        }
    },
    
    init() {
        try {
            const saved = localStorage.getItem('progressV5');
            this.progress = saved ? JSON.parse(saved) : {};
        } catch(e) {
            this.progress = {};
        }
        allWords.forEach(w => {
            if (!this.progress[w.word]) {
                this.progress[w.word] = {count: 0, error: false, done: false};
            }
        });
        this.updateUI();
    },
    
    updateUI() {
        const done = Object.values(this.progress).filter(p => p.done).length;
        const pct = Math.round((done / allWords.length) * 100);
        const pb = document.getElementById('progressBar');
        if (pb) { pb.style.width = pct + '%'; pb.textContent = pct + '%'; }
        const label = document.getElementById('masteredLabel');
        if (label) label.textContent = `Gelernt: ${done}/855`;
        const masteredStats = document.getElementById('mastered');
        if (masteredStats) masteredStats.textContent = done;
    },
    
    start() {
        this.initAudio().catch(e => console.log("Audio Fehler:", e));
        this.init();
        const active = allWords.filter(w => !this.progress[w.word].done);
        const shuffled = [...active].sort(() => Math.random() - 0.5);
        this.words = shuffled.slice(0, Math.min(this.wordCount, shuffled.length));
        this.idx = 0;
        this.correct = 0;
        this.totalQuestions = this.words.length;
        this.wrong = [];
        
        if (this.words.length === 0) {
            document.getElementById('gameArea').innerHTML = `
                <div class="result">
                    <h2>🎊 Gratuliere! 🎊</h2>
                    <p style="font-size: 24px; margin: 30px 0;">Alle 855 Wörter gelernt! 🏆</p>
                    <button class="btn btn-start" onclick="game.reset()">Neu starten</button>
                </div>`;
            return;
        }
        document.getElementById('maxRound').textContent = this.totalQuestions;
        this.upStats();
        this.show();
    },
    
    reset() {
        if (confirm('Fortschritt zurücksetzen?')) {
            localStorage.removeItem('progressV5');
            location.reload();
        }
    },
    
    show() {
        if (this.idx >= this.words.length) {
            if (this.wrong.length > 0) {
                this.words = this.words.concat(this.wrong);
                this.wrong = [];
            }
            if (this.idx >= this.words.length) {
                this.end();
                return;
            }
        }
        const w = this.words[this.idx];
        document.getElementById('gameArea').innerHTML = `
            <div class="timer">⏱️ Zeit: <span id="time">10</span>s</div>
            <div class="word-display"><div class="word">${w.word}</div></div>
            <div class="buttons">
                <button class="btn btn-der" onclick="game.check('der')">DER</button>
                <button class="btn btn-die" onclick="game.check('die')">DIE</button>
                <button class="btn btn-das" onclick="game.check('das')">DAS</button>
            </div>`;
        this.time = 10;
        this.tick();
        if (this.timer) clearInterval(this.timer);
        this.timer = setInterval(() => {
            this.time--;
            this.tick();
            if (this.time <= 0) {
                clearInterval(this.timer);
                this.check(null);
            }
        }, 1000);
    },
    
    tick() {
        const el = document.getElementById('time');
        if (el) {
            el.textContent = this.time;
            el.style.color = this.time <= 3 ? '#FF4444' : '#FFD700';
        }
    },
    
    check(ans) {
        clearInterval(this.timer);
        const w = this.words[this.idx];
        const ok = ans === w.article;
        const p = this.progress[w.word];
        this.playSound(ok);
        if (ok) {
            if (this.idx < this.totalQuestions) this.correct++;
            p.count++;
            const need = p.error ? 3 : 2;
            if (p.count >= need) p.done = true;
            this.fback(true, w.article, p.done, p.count, need);
            setTimeout(() => { this.idx++; this.upStats(); this.show(); }, 1500);
        } else {
            this.wrong.push(w);
            p.count = 0;
            p.error = true;
            this.fback(false, w.article, false);
            setTimeout(() => { this.idx++; this.upStats(); this.show(); }, 7000);
        }
        localStorage.setItem('progressV5', JSON.stringify(this.progress));
    },
    
    fback(ok, art, done, c, n) {
        const w = this.words[this.idx];
        const cls = ok ? 'correct' : 'incorrect';
        let msg = ok ? (done ? '🎉 Gelernt!' : `✅ Richtig! (${c}/${n})` ) : `❌ Falsch! Richtig: ${art} ${w.word}`;
        document.getElementById('gameArea').innerHTML = `<div class="feedback ${cls}">${msg}</div>`;
    },
    
    upStats() {
        document.getElementById('round').textContent = Math.min(this.idx + 1, this.totalQuestions);
        document.getElementById('correct').textContent = this.correct;
        const done = Object.values(this.progress).filter(p => p.done).length;
        document.getElementById('mastered').textContent = done;
    },
    
    end() {
        const pct = (this.correct / this.totalQuestions * 100).toFixed(1);
        const g = pct >= 96 ? 1 : pct >= 80 ? 2 : pct >= 60 ? 3 : pct >= 45 ? 4 : pct >= 16 ? 5 : 6;
        const txt = ['Sehr gut! 🏆', 'Gut! 🌟', 'Befriedigend! 👍', 'Ausreichend! 💪', 'Mangelhaft 📚', 'Ungenügend 📖'][g-1];
        document.getElementById('gameArea').innerHTML = `
            <div class="result">
                <h2>Runde beendet!</h2>
                <div class="grade">${g}</div>
                <div style="font-size: 24px; margin-bottom: 10px;">${txt}</div>
                <p style="font-size: 22px; margin: 20px 0;">${this.correct} von ${this.totalQuestions} richtig (${pct}%)</p>
                <button class="btn btn-start" onclick="game.start()">Weiter üben!</button>
            </div>`;
    }
};
window.onload = () => game.init();
    </script>
</body>
</html>
