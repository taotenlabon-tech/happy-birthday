<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chúc Mừng 20/11 & Sinh Nhật Mẹ</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@500;600;700&family=Playfair+Display:ital,wght@0,600;0,700;1,600&display=swap');
        body {
            font-family: 'Quicksand', sans-serif;
            background: radial-gradient(circle at top, #fff1f2 0%, #ffe4e6 45%, #fef3c7 100%);
            margin: 0;
            overflow: hidden;
            user-select: none;
        }
        .font-serif-warm { font-family: 'Playfair Display', serif; }
        .glass-card {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(14px);
            border: 1px solid rgba(251, 113, 133, 0.3);
            box-shadow: 0 20px 50px rgba(225, 29, 72, 0.12);
        }
    </style>
</head>
<body class="w-screen h-screen flex items-center justify-center p-3 sm:p-6">

    <!-- MÀN HÌNH CHÀO & TÙY CHỈNH LỜI CHÚC -->
    <div id="startScreen" class="glass-card rounded-3xl max-w-lg w-full p-6 sm:p-8 text-center space-y-5 z-20">
        <div class="text-4xl sm:text-5xl">💐🎂📚</div>
        <div class="space-y-1.5">
            <p class="text-xs font-bold uppercase tracking-widest text-rose-500">20/11 • Ngày Nhà Giáo Việt Nam & Sinh Nhật Mẹ</p>
            <h1 class="font-serif-warm text-2xl sm:text-3xl font-bold text-slate-800">
                Món Quà Nhỏ Tặng Mẹ Yêu
            </h1>
            <p class="text-xs sm:text-sm text-slate-600 leading-relaxed">
                Di chuyển chuột hoặc ngón tay để hứng hoa tươi, điểm 10 và quà sinh nhật cho mẹ. Hứng đủ <span class="font-bold text-rose-600">20 món quà</span> để mở thiệp chúc mừng đặc biệt!
            </p>
        </div>

        <div class="text-left space-y-2 bg-rose-50/80 p-3.5 rounded-2xl border border-rose-200/70">
            <label class="block text-[11px] font-bold text-rose-700">✍️ Lời nhắn riêng cho mẹ (có thể sửa):</label>
            <input id="customWishInput" type="text"
                value="Chúc mẹ 20/11 luôn rạng rỡ trên bục giảng, sinh nhật tuổi mới thật nhiều sức khỏe và bình an!"
                class="w-full px-3 py-2 text-xs sm:text-sm rounded-xl bg-white border border-rose-200 text-slate-700 focus:outline-none focus:border-rose-400">
        </div>

        <div class="flex flex-col sm:flex-row gap-3 pt-1">
            <button onclick="startGame()" class="flex-1 py-3.5 px-6 rounded-2xl bg-gradient-to-r from-rose-500 via-pink-500 to-amber-500 text-white font-bold text-sm shadow-lg hover:brightness-105 active:scale-95 transition cursor-pointer">
                🎁 Bắt Đầu Tặng Quà Cho Mẹ
            </button>
            <button onclick="toggleSound()" id="soundBtn" class="py-3.5 px-4 rounded-2xl bg-white border border-rose-200 text-rose-600 font-bold text-xs hover:bg-rose-50 transition cursor-pointer">
                🔊 Nhạc: Bật
            </button>
        </div>
    </div>

    <!-- MÀN HÌNH CHƠI GAME -->
    <div id="gameScreen" class="hidden relative w-full h-full max-w-4xl max-h-[86vh] glass-card rounded-3xl overflow-hidden flex flex-col">
        <div class="flex items-center justify-between px-4 sm:px-6 py-3 bg-white/70 border-b border-rose-100 z-10">
            <div class="flex items-center gap-4">
                <div>
                    <div class="text-[10px] font-bold uppercase text-rose-500">Quà Đã Hứng</div>
                    <div id="scoreText" class="text-lg sm:text-xl font-bold text-slate-800">0 / 20</div>
                </div>
                <div class="w-28 sm:w-44 h-3 bg-rose-100 rounded-full overflow-hidden">
                    <div id="progressBar" class="h-full bg-gradient-to-r from-rose-500 to-amber-400 transition-all duration-200" style="width: 0%"></div>
                </div>
            </div>
            <button onclick="backToStart()" class="px-3 py-1.5 rounded-xl bg-rose-50 hover:bg-rose-100 text-rose-600 text-xs font-bold transition cursor-pointer">
                ↩ Đổi Lời Chúc
            </button>
        </div>

        <div class="relative flex-1 w-full overflow-hidden">
            <canvas id="giftCanvas" class="w-full h-full block touch-none"></canvas>
            <div id="floatingToast" class="hidden absolute top-4 left-1/2 -translate-x-1/2 px-4 py-1.5 rounded-full bg-white/90 border border-rose-200 text-rose-600 text-xs font-bold shadow">
                ☁️ Đám mây bận rộn lướt qua, tránh nhẹ nha!
            </div>
        </div>
    </div>

    <!-- THIỆP CHÚC MỪNG KHI HOÀN THÀNH -->
    <div id="cardModal" class="hidden fixed inset-0 z-30 bg-rose-950/35 backdrop-blur-sm flex items-center justify-center p-4">
        <div class="glass-card rounded-3xl max-w-md w-full p-6 sm:p-8 text-center space-y-4 relative overflow-hidden">
            <div class="text-5xl">🎉👩‍🏫🎂🌹</div>
            <div class="text-xs font-bold uppercase tracking-widest text-rose-500">Happy Birthday & Happy Teachers' Day</div>
            <h2 class="font-serif-warm text-2xl sm:text-3xl font-bold text-slate-800">
                Gửi Mẹ Yêu Quý!
            </h2>
            <p id="finalWishText" class="text-sm sm:text-base text-slate-700 leading-relaxed italic bg-rose-50/90 p-4 rounded-2xl border border-rose-200/80">
            </p>
            <p class="text-xs text-slate-500">
                Cảm ơn mẹ vì những bài giảng dịu dàng và vòng tay luôn chở che con mỗi ngày.
            </p>
            <div class="flex gap-3 pt-2">
                <button onclick="replayGame()" class="flex-1 py-3 rounded-2xl bg-gradient-to-r from-rose-500 to-amber-500 text-white font-bold text-xs sm:text-sm shadow hover:brightness-105 transition cursor-pointer">
                    🔄 Chơi Lại
                </button>
                <button onclick="backToStart()" class="flex-1 py-3 rounded-2xl bg-white border border-rose-200 text-rose-600 font-bold text-xs sm:text-sm hover:bg-rose-50 transition cursor-pointer">
                    ✉️ Sửa Lời Chúc
                </button>
            </div>
        </div>
    </div>

    <script>
        let audioCtx = null;
        let soundEnabled = true;
        let melodyTimer = null;

        function ensureAudio() {
            if (!audioCtx) {
                const Ctx = window.AudioContext || window.webkitAudioContext;
                audioCtx = new Ctx();
            }
            if (audioCtx.state === 'suspended') {
                audioCtx.resume();
            }
        }

        function playTone(freq, duration = 0.25, type = 'sine', volume = 0.08) {
            if (!soundEnabled || !audioCtx) return;
            const now = audioCtx.currentTime;
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.type = type;
            osc.frequency.setValueAtTime(freq, now);
            gain.gain.setValueAtTime(0.001, now);
            gain.gain.linearRampToValueAtTime(volume, now + 0.03);
            gain.gain.exponentialRampToValueAtTime(0.0001, now + duration);
            osc.connect(gain);
            gain.connect(audioCtx.destination);
            osc.start(now);
            osc.stop(now + duration + 0.02);
        }

        function playCollectSound() {
            playTone(523.25, 0.14, 'triangle', 0.1);
            setTimeout(() => playTone(659.25, 0.18, 'triangle', 0.1), 70);
        }

        function playFanfareSound() {
            const notes = [523.25, 659.25, 783.99, 1046.5];
            notes.forEach((n, idx) => {
                setTimeout(() => playTone(n, 0.35, 'triangle', 0.12), idx * 130);
            });
        }

        function startGentleMelody() {
            stopGentleMelody();
            if (!soundEnabled) return;
            const scale = [523.25, 587.33, 659.25, 783.99, 880.00, 783.99, 659.25, 587.33];
            let i = 0;
            melodyTimer = setInterval(() => {
                if (isPlaying && soundEnabled) {
                    playTone(scale[i % scale.length], 0.4, 'sine', 0.045);
                    i++;
                }
            }, 650);
        }

        function stopGentleMelody() {
            if (melodyTimer) {
                clearInterval(melodyTimer);
                melodyTimer = null;
            }
        }

        function toggleSound() {
            soundEnabled = !soundEnabled;
            document.getElementById('soundBtn').innerText = soundEnabled ? '🔊 Nhạc: Bật' : '🔇 Nhạc: Tắt';
            if (soundEnabled && isPlaying) {
                ensureAudio();
                startGentleMelody();
            } else {
                stopGentleMelody();
            }
        }

        const TARGET_GIFTS = 20;
        const goodItems = ['🌹', '🎂', '🌸', '🎁', '⭐', '💯', '💐'];
        const canvas = document.getElementById('giftCanvas');
        const ctx = canvas.getContext('2d');

        let isPlaying = false;
        let score = 0;
        let animId = null;
        let spawnTimer = 0;
        let fallingItems = [];
        let sparkles = [];
        let basket = { x: 200, y: 0, width: 88, height: 42 };

        function resizeCanvas() {
            const rect = canvas.parentElement.getBoundingClientRect();
            canvas.width = rect.width;
            canvas.height = rect.height;
            basket.y = canvas.height - 56;
            if (!basket.x) basket.x = canvas.width / 2;
        }

        function updatePointerX(clientX) {
            const rect = canvas.getBoundingClientRect();
            const relX = clientX - rect.left;
            basket.x = Math.max(basket.width / 2 + 8, Math.min(canvas.width - basket.width / 2 - 8, relX));
        }

        canvas.addEventListener('mousemove', (e) => {
            if (isPlaying) updatePointerX(e.clientX);
        });

        canvas.addEventListener('touchmove', (e) => {
            if (isPlaying && e.touches.length > 0) {
                e.preventDefault();
                updatePointerX(e.touches[0].clientX);
            }
        }, { passive: false });

        function startGame() {
            ensureAudio();
            document.getElementById('startScreen').classList.add('hidden');
            document.getElementById('cardModal').classList.add('hidden');
            document.getElementById('gameScreen').classList.remove('hidden');

            resizeCanvas();
            score = 0;
            fallingItems = [];
            sparkles = [];
            spawnTimer = 0;
            basket.x = canvas.width / 2;
            isPlaying = true;
            updateScoreUI();
            startGentleMelody();

            if (animId) cancelAnimationFrame(animId);
            loop();
        }

        function replayGame() {
            document.getElementById('cardModal').classList.add('hidden');
            startGame();
        }

        function backToStart() {
            isPlaying = false;
            stopGentleMelody();
            if (animId) cancelAnimationFrame(animId);
            document.getElementById('gameScreen').classList.add('hidden');
            document.getElementById('cardModal').classList.add('hidden');
            document.getElementById('startScreen').classList.remove('hidden');
        }

        function updateScoreUI() {
            document.getElementById('scoreText').innerText = `${score} / ${TARGET_GIFTS}`;
            const pct = Math.min(100, (score / TARGET_GIFTS) * 100);
            document.getElementById('progressBar').style.width = `${pct}%`;
        }

        function showToast() {
            const toast = document.getElementById('floatingToast');
            toast.classList.remove('hidden');
            clearTimeout(toast._t);
            toast._t = setTimeout(() => toast.classList.add('hidden'), 1100);
        }

        function spawnItem() {
            const isCloud = Math.random() < 0.2;
            const emoji = isCloud ? '☁️' : goodItems[Math.floor(Math.random() * goodItems.length)];
            fallingItems.push({
                x: 36 + Math.random() * Math.max(40, canvas.width - 72),
                y: -28,
                vy: (isCloud ? 2.1 : 2.3) + Math.random() * 1.4,
                emoji,
                isCloud,
                size: isCloud ? 30 : 28,
                sway: Math.random() * Math.PI * 2
            });
        }

        function addSparkles(x, y, color = '#f43f5e') {
            for (let i = 0; i < 10; i++) {
                const angle = (Math.PI * 2 * i) / 10;
                sparkles.push({
                    x,
                    y,
                    vx: Math.cos(angle) * (1.5 + Math.random() * 2),
                    vy: Math.sin(angle) * (1.5 + Math.random() * 2),
                    life: 1,
                    color
                });
            }
        }

        function finishCelebration() {
            isPlaying = false;
            stopGentleMelody();
            playFanfareSound();
            const customWish = document.getElementById('customWishInput').value.trim();
            document.getElementById('finalWishText').innerText =
                `“${customWish || 'Chúc mẹ 20/11 và sinh nhật tuổi mới thật nhiều sức khỏe, niềm vui và hạnh phúc bên gia đình!'}”`;
            document.getElementById('cardModal').classList.remove('hidden');
        }

        function loop() {
            if (!isPlaying) return;
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            spawnTimer++;
            if (spawnTimer >= 36) {
                spawnTimer = 0;
                spawnItem();
            }

            // Vẽ giỏ quà của mẹ
            ctx.save();
            const bx = basket.x - basket.width / 2;
            const by = basket.y - basket.height / 2;
            ctx.fillStyle = '#fb7185';
            ctx.beginPath();
            ctx.roundRect(bx, by, basket.width, basket.height, 14);
            ctx.fill();
            ctx.strokeStyle = '#fff1f2';
            ctx.lineWidth = 2.5;
            ctx.stroke();

            ctx.font = '20px sans-serif';
            ctx.textAlign = 'center';
            ctx.textBaseline = 'middle';
            ctx.fillText('🧺', basket.x, basket.y + 1);
            ctx.restore();

            // Cập nhật vật phẩm rơi
            for (let i = fallingItems.length - 1; i >= 0; i--) {
                const item = fallingItems[i];
                item.y += item.vy;
                item.sway += 0.05;
                item.x += Math.sin(item.sway) * 0.6;

                ctx.font = `${item.size}px sans-serif`;
                ctx.textAlign = 'center';
                ctx.textBaseline = 'middle';
                ctx.fillText(item.emoji, item.x, item.y);

                const hitX = Math.abs(item.x - basket.x) < basket.width * 0.55;
                const hitY = Math.abs(item.y - basket.y) < basket.height * 0.65;

                if (hitX && hitY) {
                    if (item.isCloud) {
                        score = Math.max(0, score - 1);
                        updateScoreUI();
                        addSparkles(item.x, item.y, '#94a3b8');
                        showToast();
                    } else {
                        score++;
                        updateScoreUI();
                        playCollectSound();
                        addSparkles(item.x, item.y, '#f43f5e');
                        if (score >= TARGET_GIFTS) {
                            finishCelebration();
                            return;
                        }
                    }
                    fallingItems.splice(i, 1);
                    continue;
                }

                if (item.y > canvas.height + 35) {
                    fallingItems.splice(i, 1);
                }
            }

            // Hiệu ứng lấp lánh
            for (let i = sparkles.length - 1; i >= 0; i--) {
                const s = sparkles[i];
                s.x += s.vx;
                s.y += s.vy;
                s.life -= 0.04;
                if (s.life <= 0) {
                    sparkles.splice(i, 1);
                    continue;
                }
                ctx.save();
                ctx.globalAlpha = Math.max(0, s.life);
                ctx.fillStyle = s.color;
                ctx.beginPath();
                ctx.arc(s.x, s.y, 4, 0, Math.PI * 2);
                ctx.fill();
                ctx.restore();
            }

            animId = requestAnimationFrame(loop);
        }

        window.addEventListener('resize', () => {
            if (isPlaying) resizeCanvas();
        });
    </script>
</body>
</html>
