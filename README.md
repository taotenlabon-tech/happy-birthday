<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bức Thư Gửi Mẹ • 20/11 & Sinh Nhật Mẹ</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@400;500;600;700&family=Playfair+Display:ital,wght@0,500;0,700;1,500&display=swap');
        body {
            font-family: 'Quicksand', sans-serif;
            background: radial-gradient(circle at top, #fff1f2 0%, #ffe4e6 50%, #fef3c7 100%);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        .font-letter {
            font-family: 'Playfair Display', serif;
        }
        .petal {
            position: fixed;
            top: -30px;
            pointer-events: none;
            z-index: 5;
            animation: fallPetal linear forwards;
        }
        @keyframes fallPetal {
            0% {
                transform: translateY(-20px) translateX(0) rotate(0deg);
                opacity: 0.9;
            }
            100% {
                transform: translateY(105vh) translateX(45px) rotate(360deg);
                opacity: 0;
            }
        }
        .letter-line {
            opacity: 0;
            transform: translateY(12px);
            transition: opacity 0.9s ease, transform 0.9s ease;
        }
        .letter-line.visible {
            opacity: 1;
            transform: translateY(0);
        }
        .envelope-card {
            background: rgba(255, 255, 255, 0.88);
            backdrop-filter: blur(14px);
            border: 1px solid rgba(251, 113, 133, 0.35);
            box-shadow: 0 24px 60px rgba(225, 29, 72, 0.14);
        }
    </style>
</head>
<body class="flex items-center justify-center p-4 sm:p-6">

    <!-- MÀN HÌNH PHONG THƯ CHỜ BẤM MỞ -->
    <div id="envelopeScreen" class="envelope-card rounded-3xl max-w-md w-full p-7 sm:p-9 text-center space-y-6 z-10">
        <div class="inline-flex items-center justify-center w-24 h-24 rounded-3xl bg-gradient-to-br from-rose-100 to-amber-100 border border-rose-200 shadow-inner text-5xl">
            ✉️
        </div>

        <div class="space-y-2">
            <p class="text-[11px] font-bold uppercase tracking-[0.2em] text-rose-500">
                20/11 • Ngày Nhà Giáo & Sinh Nhật Mẹ
            </p>
            <h1 class="font-letter text-2xl sm:text-3xl font-bold text-slate-800">
                Một Bức Thư Nhỏ Gửi Mẹ
            </h1>
            <p class="text-xs sm:text-sm text-slate-600 leading-relaxed">
                Bấm vào phong thư để mở nhạc nhẹ và đọc từng dòng nhắn gửi tới mẹ.
            </p>
        </div>

        <button onclick="openLetter()" class="w-full py-3.5 px-6 rounded-2xl bg-gradient-to-r from-rose-500 via-pink-500 to-amber-500 text-white font-bold text-sm shadow-lg hover:brightness-105 active:scale-95 transition cursor-pointer">
            💌 Mở Thư & Bật Nhạc
        </button>

        <button onclick="toggleEditor()" class="text-xs font-semibold text-rose-600 hover:underline cursor-pointer">
            ✏️ Tùy chỉnh nội dung bức thư
        </button>

        <div id="editorBox" class="hidden text-left space-y-3 pt-2 border-t border-rose-100">
            <div>
                <label class="block text-[11px] font-bold text-slate-600 mb-1">Các dòng thư (mỗi dòng là một đoạn hiện dần):</label>
                <textarea id="linesInput" rows="6" class="w-full p-3 text-xs rounded-xl bg-white border border-rose-200 text-slate-700 focus:outline-none focus:border-rose-400">Mẹ kính yêu,
Nhân ngày 20/11 và cũng là ngày sinh nhật của mẹ, con muốn gửi tới mẹ thật nhiều yêu thương.
Cảm ơn mẹ vì bao năm tận tụy trên bục giảng, dìu dắt biết bao thế hệ học trò bằng sự kiên nhẫn và ấm áp.
Và trên hết, cảm ơn mẹ vì luôn là người mẹ hiền hậu, vất vả lo cho gia đình và cho con khôn lớn từng ngày.
Chúc cô giáo của chúng con và mẹ yêu của con tuổi mới thật nhiều sức khỏe, bình an và luôn mỉm cười rạng rỡ.
Con yêu mẹ rất nhiều!</textarea>
            </div>
            <div>
                <label class="block text-[11px] font-bold text-slate-600 mb-1">Lời ký tên ở cuối thư:</label>
                <input id="signInput" type="text" value="Người con luôn thương mẹ" class="w-full px-3 py-2 text-xs rounded-xl bg-white border border-rose-200 text-slate-700 focus:outline-none focus:border-rose-400">
            </div>
        </div>
    </div>

    <!-- MÀN HÌNH ĐỌC BỨC THƯ -->
    <div id="letterScreen" class="hidden envelope-card rounded-3xl max-w-2xl w-full p-6 sm:p-10 space-y-6 z-10 my-4">
        <div class="flex items-center justify-between border-b border-rose-100 pb-4">
            <div class="flex items-center gap-2.5">
                <span class="text-2xl">🌹🎂</span>
                <div>
                    <div class="text-[10px] font-bold uppercase tracking-widest text-rose-500">20/11 • Happy Birthday Mom</div>
                    <div class="font-letter text-lg font-bold text-slate-800">Thư Gửi Mẹ Yêu</div>
                </div>
            </div>

            <div class="flex items-center gap-2">
                <button onclick="toggleMusic()" id="musicToggleBtn" class="px-3 py-1.5 rounded-xl bg-rose-50 hover:bg-rose-100 text-rose-600 text-xs font-bold transition cursor-pointer">
                    🔊 Nhạc: Bật
                </button>
                <button onclick="replayLetter()" class="px-3 py-1.5 rounded-xl bg-amber-50 hover:bg-amber-100 text-amber-700 text-xs font-bold transition cursor-pointer">
                    ↻ Đọc Lại
                </button>
                <button onclick="backToEnvelope()" class="px-3 py-1.5 rounded-xl bg-slate-100 hover:bg-slate-200 text-slate-600 text-xs font-bold transition cursor-pointer">
                    ✉️ Đóng Thư
                </button>
            </div>
        </div>

        <div id="letterBody" class="font-letter text-base sm:text-lg text-slate-700 leading-relaxed space-y-4 min-h-[240px]"></div>

        <div id="letterSignature" class="letter-line pt-4 border-t border-rose-100 flex items-end justify-between">
            <div class="text-xs text-slate-400">💐 Chúc mừng 20/11 & Sinh nhật mẹ</div>
            <div id="signatureText" class="font-letter italic text-lg sm:text-xl font-semibold text-rose-600">
                Người con luôn thương mẹ
            </div>
        </div>
    </div>

    <script>
        let audioCtx = null;
        let isMusicOn = true;
        let isLetterOpen = false;
        let musicLoop = null;
        let petalLoop = null;
        let lineTimeouts = [];

        const notes = [
            { freq: 523.25, dur: 0.9 },
            { freq: 659.25, dur: 0.9 },
            { freq: 783.99, dur: 1.1 },
            { freq: 659.25, dur: 0.9 },
            { freq: 587.33, dur: 0.9 },
            { freq: 440.00, dur: 1.1 },
            { freq: 587.33, dur: 0.9 },
            { freq: 783.99, dur: 1.2 }
        ];

        function initAudio() {
            if (!audioCtx) {
                const AudioContext = window.AudioContext || window.webkitAudioContext;
                audioCtx = new AudioContext();
            }
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
        }

        function playSoftNote(freq, duration) {
            if (!audioCtx || !isMusicOn || !isLetterOpen) return;
            const now = audioCtx.currentTime;
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();

            osc.type = 'sine';
            osc.frequency.setValueAtTime(freq, now);

            gain.gain.setValueAtTime(0.0001, now);
            gain.gain.linearRampToValueAtTime(0.065, now + 0.14);
            gain.gain.exponentialRampToValueAtTime(0.0001, now + duration);

            osc.connect(gain);
            gain.connect(audioCtx.destination);

            osc.start(now);
            osc.stop(now + duration + 0.05);
        }

        function startMusic() {
            stopMusic();
            if (!isMusicOn) return;
            let idx = 0;
            const step = () => {
                if (!isMusicOn || !isLetterOpen) return;
                const item = notes[idx % notes.length];
                playSoftNote(item.freq, item.dur);
                idx++;
                musicLoop = setTimeout(step, item.dur * 850);
            };
            step();
        }

        function stopMusic() {
            if (musicLoop) {
                clearTimeout(musicLoop);
                musicLoop = null;
            }
        }

        function toggleMusic() {
            isMusicOn = !isMusicOn;
            document.getElementById('musicToggleBtn').innerText = isMusicOn ? '🔊 Nhạc: Bật' : '🔇 Nhạc: Tắt';
            if (isMusicOn && isLetterOpen) {
                initAudio();
                startMusic();
            } else {
                stopMusic();
            }
        }

        function toggleEditor() {
            document.getElementById('editorBox').classList.toggle('hidden');
        }

        function spawnPetal() {
            if (!isLetterOpen) return;
            const emojis = ['🌸', '🌹', '✨', '💖'];
            const el = document.createElement('div');
            el.className = 'petal text-lg sm:text-xl';
            el.innerText = emojis[Math.floor(Math.random() * emojis.length)];
            el.style.left = Math.random() * 100 + 'vw';
            const duration = 5 + Math.random() * 4;
            el.style.animationDuration = duration + 's';
            document.body.appendChild(el);
            setTimeout(() => el.remove(), duration * 1000);
        }

        function startPetals() {
            stopPetals();
            petalLoop = setInterval(spawnPetal, 650);
        }

        function stopPetals() {
            if (petalLoop) {
                clearInterval(petalLoop);
                petalLoop = null;
            }
        }

        function clearLineTimers() {
            lineTimeouts.forEach(t => clearTimeout(t));
            lineTimeouts = [];
        }

        function revealLetterLines() {
            clearLineTimers();
            const bodyEl = document.getElementById('letterBody');
            const sigEl = document.getElementById('letterSignature');
            const signInputVal = document.getElementById('signInput').value.trim() || 'Người con luôn thương mẹ';
            document.getElementById('signatureText').innerText = signInputVal;

            sigEl.classList.remove('visible');
            bodyEl.innerHTML = '';

            const rawLines = document.getElementById('linesInput').value
                .split('\n')
                .map(line => line.trim())
                .filter(line => line.length > 0);

            rawLines.forEach((text, index) => {
                const p = document.createElement('p');
                p.className = 'letter-line';
                p.innerText = text;
                bodyEl.appendChild(p);

                const showTimer = setTimeout(() => {
                    p.classList.add('visible');
                }, 450 + index * 1350);
                lineTimeouts.push(showTimer);
            });

            const sigTimer = setTimeout(() => {
                sigEl.classList.add('visible');
            }, 450 + rawLines.length * 1350 + 300);
            lineTimeouts.push(sigTimer);
        }

        function openLetter() {
            initAudio();
            isLetterOpen = true;
            document.getElementById('envelopeScreen').classList.add('hidden');
            document.getElementById('letterScreen').classList.remove('hidden');
            revealLetterLines();
            startMusic();
            startPetals();
        }

        function replayLetter() {
            revealLetterLines();
        }

        function backToEnvelope() {
            isLetterOpen = false;
            stopMusic();
            stopPetals();
            clearLineTimers();
            document.getElementById('letterScreen').classList.add('hidden');
            document.getElementById('envelopeScreen').classList.remove('hidden');
        }
    </script>
</body>
</html>
