<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Project Gerbera</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600&family=Playfair+Display:ital,wght@0,400;0,500;1,400&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #FDFBF7; /* Cream */
            color: #4A4A4A;
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
        }
        .serif-text {
            font-family: 'Playfair Display', serif;
        }
        .glass-card {
            background: rgba(255, 255, 255, 0.45);
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            border: 1px solid rgba(255, 255, 255, 0.6);
        }
        /* Page Transition System */
        .chapter-section {
            display: none;
            opacity: 0;
            transition: opacity 1.2s ease-in-out;
        }
        .chapter-section.active {
            display: flex;
            opacity: 1;
        }
        /* Candle flame animation */
        @keyframes flicker {
            0%, 100% { transform: scale(1); opacity: 0.9; }
            50% { transform: scale(1.15) translate(-1px, -2px); opacity: 1; filter: drop-shadow(0 0 10px #f59e0b); }
        }
        .flame {
            animation: flicker 0.6s infinite alternate;
        }
        /* Custom scrollbar for message jar */
        .custom-scroll::-webkit-scrollbar {
            width: 4px;
        }
        .custom-scroll::-webkit-scrollbar-thumb {
            background: #fbcfe8;
            border-radius: 10px;
        }
    </style>
</head>
<body class="relative min-h-screen select-none flex flex-col justify-between overflow-hidden">

    <!-- AUDIO ELEMENTS -->
    <!-- Catatan: Silakan ganti link src di bawah ini dengan link lagu/audio pilihanmu sendiri -->
    <audio id="audio-ambience" loop src="https://assets.mixkit.co/active_storage/sfx/2433/2433-84.wav"></audio>
    <audio id="audio-bgm" loop src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3"></audio>

    <!-- LOGO UNTUK DEV ROOM TRIGGER (Pojok Kiri Atas) -->
    <div id="dev-trigger" class="absolute top-6 left-6 text-[10px] tracking-widest text-pink-300 opacity-40 cursor-pointer z-50 hover:opacity-100 transition-opacity">
        PROJECT GERBERA
    </div>

    <!-- GERBERA HUNT COUNTER PANEL (Pojok Kiri Bawah) -->
    <div id="hunt-counter-ui" class="hidden absolute bottom-6 left-6 glass-card px-4 py-1.5 rounded-full text-[11px] text-pink-500 z-50 tracking-wider">
        🌼 <span id="hunt-count">0</span>/5 Terkumpul
    </div>

    <!-- MAIN CONTENT CONTAINER -->
    <main class="flex-grow w-full max-w-lg mx-auto relative flex flex-col justify-center px-6 py-20">

        <!-- ========================================== -->
        <!-- CHAPTER 1: THE ENTRANCE                    -->
        <!-- ========================================== -->
        <section id="ch-1" class="chapter-section active flex-col items-center justify-center text-center space-y-6">
            <p class="text-[11px] tracking-widest text-neutral-400 italic">“A place where memories quietly bloom.”</p>
            <div class="h-16 flex items-center justify-center">
                <h1 id="entrance-text" class="serif-text text-xl italic text-neutral-600 transition-opacity duration-700">hey...</h1>
            </div>
            <button id="btn-open-gift" class="opacity-0 scale-95 pointer-events-none transition-all duration-1000 glass-card px-8 py-3 rounded-full text-xs tracking-widest text-neutral-500 border border-pink-200 hover:bg-white hover:text-pink-400">
                🌼 Open Gift
            </button>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 2: THE GIFT                         -->
        <!-- ========================================== -->
        <section id="ch-2" class="chapter-section flex-col items-center justify-center text-center space-y-6 relative">
            <!-- Hidden Gerbera 1 -->
            <span class="absolute -top-10 -left-2 text-xl opacity-10 hover:opacity-100 cursor-pointer transition-opacity" onclick="collectGerbera(1, this)">🌼</span>
            
            <div id="gift-box" class="w-24 h-24 glass-card rounded-2xl flex items-center justify-center border-pink-100 cursor-pointer shadow-sm hover:scale-105 transition-transform duration-500">
                <span class="text-3xl animate-bounce">🎁</span>
            </div>
            <div id="gift-message" class="hidden space-y-4 max-w-xs opacity-0 transition-opacity duration-1000">
                <p class="serif-text text-lg text-neutral-600 italic">Not every gift comes in a box.</p>
                <p class="text-xs text-neutral-400 leading-relaxed">Some come as a little place<br><span class="italic font-medium text-pink-400">made just for one person.</span></p>
                <button onclick="changeChapter(3)" class="text-[11px] tracking-widest text-neutral-400 border-b border-neutral-300 pb-0.5 pt-4 hover:text-pink-400 hover:border-pink-400 transition-colors">Continue</button>
            </div>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 3: THE LETTER                       -->
        <!-- ========================================== -->
        <section id="ch-3" class="chapter-section flex-col items-center justify-center">
            <div class="glass-card w-full p-8 rounded-2xl border-white shadow-sm space-y-4 text-left">
                <span class="text-[10px] tracking-widest text-pink-300 block">💌 THE LETTER</span>
                <div class="min-h-[100px] text-xs text-neutral-600 leading-relaxed serif-text italic" id="typewriter-text"></div>
                <div class="text-right opacity-0 transition-opacity duration-700" id="letter-nav">
                    <button onclick="changeChapter(4)" class="text-[11px] tracking-widest text-neutral-400 hover:text-pink-400 transition-colors">Go to the Garden →</button>
                </div>
            </div>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 4: THE GARDEN                       -->
        <!-- ========================================== -->
        <section id="ch-4" class="chapter-section flex-col items-center justify-center text-center space-y-8 relative">
            <!-- Hidden Gerbera 2 -->
            <span class="absolute top-0 right-4 text-xl opacity-10 hover:opacity-100 cursor-pointer transition-opacity" onclick="collectGerbera(2, this)">🌼</span>
            
            <div class="space-y-2">
                <h2 class="serif-text text-xl italic text-neutral-700">The Garden</h2>
                <p class="text-[11px] text-neutral-400">Ketuk bunga untuk mendengarkan bisikannya.</p>
            </div>
            
            <!-- Garden Flowers Visual Grid -->
            <div class="flex justify-center space-x-8 py-4">
                <div onclick="tapGardenFlower('don’t forget to rest. 🤍')" class="cursor-pointer text-center group">
                    <div class="text-4xl filter drop-shadow-sm transition-transform duration-500 group-hover:scale-110 group-hover:rotate-12">🌼</div>
                    <span class="text-[10px] text-neutral-400 block mt-1">Gerbera</span>
                </div>
                <div onclick="tapGardenFlower('i’m proud of you. ✨')" class="cursor-pointer text-center group">
                    <div class="text-4xl filter drop-shadow-sm transition-transform duration-500 group-hover:scale-110 group-hover:-rotate-12">🌸</div>
                    <span class="text-[10px] text-neutral-400 block mt-1">Jepun</span>
                </div>
                <div onclick="tapGardenFlower('thank you for being here. 💕')" class="cursor-pointer text-center group">
                    <div class="text-4xl filter drop-shadow-sm transition-transform duration-500 group-hover:scale-110 group-hover:rotate-6">🌼</div>
                    <span class="text-[10px] text-neutral-400 block mt-1">Gerbera</span>
                </div>
            </div>

            <!-- Speech Bubble Popup -->
            <div id="garden-bubble" class="opacity-0 transition-opacity duration-500 glass-card px-6 py-2.5 rounded-full text-xs text-neutral-600 italic">
                ...
            </div>

            <button onclick="changeChapter(5)" class="text-[11px] tracking-widest text-neutral-400 border-b border-neutral-300 pb-0.5 hover:text-pink-400 hover:border-pink-400 transition-colors pt-4">Lihat Kenangan Kita →</button>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 5: OUR MEMORIES                    -->
        <!-- ========================================== -->
        <section id="ch-5" class="chapter-section flex-col items-center justify-center text-center space-y-6 relative">
            <h2 class="serif-text text-xl italic text-neutral-700">Our Memories</h2>
            
            <!-- Polaroid Frame Stack Container -->
            <div class="w-64 h-80 relative flex items-center justify-center" id="polaroid-container">
                <!-- Polaroid Card 1 -->
                <div onclick="developPolaroid(this)" class="polaroid-card absolute w-full h-full bg-white p-4 pb-12 shadow-md rounded-sm transform -rotate-2 cursor-pointer transition-all duration-700 hover:rotate-0 z-20">
                    <div class="w-full h-full bg-neutral-200 transition-colors duration-2000 flex items-center justify-center text-xs text-neutral-400 overflow-hidden relative">
                        <!-- Masukkan URL Fotomu di src di bawah jika ada -->
                        <img class="photo-img opacity-0 transition-opacity duration-2000 absolute inset-0 w-full h-full object-cover" src="https://images.unsplash.com/photo-1516589178581-6cd7833ae3b2?q=80&w=600" alt="Memory 1">
                        <span class="develop-prompt">Ketuk untuk mencetak</span>
                    </div>
                    <p class="serif-text text-xs text-neutral-500 italic text-center mt-3">one of my favorite days.</p>
                </div>
                <!-- Polaroid Card 2 (Di belakang) -->
                <div onclick="this.style.transform='translateX(300px) rotate(15deg)'; this.style.opacity='0'; setTimeout(()=> {this.remove()}, 700)" class="absolute w-full h-full bg-white p-4 pb-12 shadow-sm rounded-sm transform rotate-3 cursor-pointer transition-all duration-700 z-10">
                    <div class="w-full h-full bg-neutral-300 flex items-center justify-center text-xs text-neutral-400 overflow-hidden">
                        <img class="w-full h-full object-cover" src="https://images.unsplash.com/photo-1494972308805-463bc619d34e?q=80&w=600" alt="Memory 2">
                    </div>
                    <p class="serif-text text-xs text-neutral-400 italic text-center mt-3">Geser kartu ini...</p>
                </div>
            </div>

            <button onclick="changeChapter(6)" class="text-[11px] tracking-widest text-neutral-400 border-b border-neutral-300 pb-0.5 hover:text-pink-400 hover:border-pink-400 transition-colors">Kirim Harapan →</button>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 6: FLOATING WISHES                 -->
        <!-- ========================================== -->
        <section id="ch-6" class="chapter-section flex-col items-center justify-center text-center space-y-8 relative">
            <!-- Hidden Gerbera 3 -->
            <span class="absolute top-1/2 -left-6 text-xl opacity-10 hover:opacity-100 cursor-pointer transition-opacity" onclick="collectGerbera(3, this)">🌼</span>
            
            <div class="space-y-1">
                <h2 class="serif-text text-xl italic text-neutral-700">Floating Wishes</h2>
                <p class="text-[11px] text-neutral-400">Ketuk balon hati untuk melepaskan doa.</p>
            </div>

            <div class="flex justify-center space-x-4 py-6">
                <button onclick="popWish('stay healthy. 🎈', this)" class="w-14 h-14 rounded-full bg-pink-100 border border-pink-200 text-lg flex items-center justify-center cursor-pointer hover:scale-110 transition-transform">💖</button>
                <button onclick="popWish('dream big. ✨', this)" class="w-14 h-14 rounded-full bg-pink-100 border border-pink-200 text-lg flex items-center justify-center cursor-pointer hover:scale-110 transition-transform">💖</button>
                <button onclick="popWish('keep smiling. 😊', this)" class="w-14 h-14 rounded-full bg-pink-100 border border-pink-200 text-lg flex items-center justify-center cursor-pointer hover:scale-110 transition-transform">💖</button>
                <button onclick="popWish('always loved. 🥺', this)" class="w-14 h-14 rounded-full bg-pink-100 border border-pink-200 text-lg flex items-center justify-center cursor-pointer hover:scale-110 transition-transform">💖</button>
            </div>

            <div id="wish-display" class="h-6 text-xs text-pink-400 serif-text italic font-medium"></div>

            <button onclick="changeChapter(7)" class="text-[11px] tracking-widest text-neutral-400 border-b border-neutral-300 pb-0.5 hover:text-pink-400 hover:border-pink-400 transition-colors">Menatap Langit →</button>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 7: THE OBSERVATORY                 -->
        <!-- ========================================== -->
        <section id="ch-7" class="chapter-section flex-col items-center justify-center text-center space-y-6 relative">
            <!-- Hidden Gerbera 4 -->
            <span class="absolute bottom-4 right-0 text-xl opacity-10 hover:opacity-100 cursor-pointer transition-opacity" onclick="collectGerbera(4, this)">🌼</span>

            <div class="space-y-1 z-10">
                <h2 class="serif-text text-xl italic text-neutral-700">The Observatory</h2>
                <p class="text-[11px] text-neutral-400">Ketuk area kosong untuk melahirkan bintang baru.</p>
            </div>

            <!-- Night sky simulation box -->
            <div id="sky-canvas" class="w-full h-56 bg-gradient-to-b from-neutral-950 to-neutral-800 rounded-2xl relative overflow-hidden shadow-inner cursor-crosshair">
                <div class="absolute inset-0 flex items-center justify-center pointer-events-none">
                    <span id="star-message" class="text-[10px] tracking-widest text-white/40 italic">Ketuk di sini...</span>
                </div>
            </div>

            <div class="flex space-x-4">
                <button onclick="promptHiddenRoom()" class="text-[11px] tracking-widest text-neutral-400 hover:text-neutral-600 transition-colors">🔐 Ruang Rahasia</button>
                <span class="text-neutral-300">|</span>
                <button onclick="changeChapter(10)" class="text-[11px] tracking-widest text-pink-400 font-medium hover:text-pink-500 transition-colors">Lanjutkan Perjalanan →</button>
            </div>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 9: THE HIDDEN ROOM                 -->
        <!-- ========================================== -->
        <section id="ch-9" class="chapter-section flex-col items-center justify-center text-center space-y-6 bg-neutral-950 text-neutral-100 fixed inset-0 p-6 z-40 transition-colors duration-1000">
            <div class="space-y-4 max-w-xs">
                <p class="text-[11px] tracking-widest text-neutral-500 uppercase">Secret Room Unlocked</p>
                <h2 class="serif-text text-xl italic text-neutral-200">welcome.<br><span class="text-sm text-neutral-400">i’ve been waiting.</span></h2>
                
                <div class="py-6">
                    <span onclick="enterFromHidden()" class="text-5xl cursor-pointer filter drop-shadow-[0_0_15px_rgba(255,255,255,0.4)] hover:scale-110 transition-transform block animate-pulse">🌼</span>
                    <span class="text-[10px] text-neutral-500 block mt-2">Ketuk gerbera untuk masuk kembali</span>
                </div>
            </div>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 10: JAR OF HEARTS                  -->
        <!-- ========================================== -->
        <section id="ch-10" class="chapter-section flex-col items-center justify-center text-center space-y-6 relative">
            <!-- Hidden Gerbera 5 -->
            <span class="absolute top-1/2 -right-4 text-xl opacity-10 hover:opacity-100 cursor-pointer transition-opacity" onclick="collectGerbera(5, this)">🌼</span>

            <div class="space-y-1">
                <h2 class="serif-text text-xl italic text-neutral-700">Jar of Hearts</h2>
                <p class="text-[11px] text-neutral-400">Buka toples untuk melihat pesan acak hari ini.</p>
            </div>

            <!-- Jar Graphic Box -->
            <div onclick="openHeartJar()" class="w-28 h-36 border-2 border-pink-200 bg-white/40 rounded-t-3xl rounded-b-xl mx-auto flex flex-col justify-between p-2 shadow-sm cursor-pointer hover:scale-105 transition-all duration-500 relative">
                <div class="w-12 h-3 bg-pink-200 mx-auto rounded-full -mt-4 border-b border-pink-300"></div>
                <div class="flex flex-wrap gap-1 justify-center overflow-hidden h-24 pt-4 opacity-70">
                    <span>❤️</span><span>💖</span><span>❤️</span><span>💕</span><span>💖</span><span>❤️</span><span>💕</span><span>❤️</span><span>💖</span>
                </div>
                <div class="text-[10px] text-pink-400 font-medium tracking-wide">AMBIL PESAN</div>
            </div>

            <!-- Pop up Message from Jar -->
            <div id="jar-message-display" class="min-h-[40px] text-xs text-neutral-600 serif-text italic max-w-xs px-4"></div>

            <button onclick="changeChapter(11)" class="text-[11px] tracking-widest text-neutral-400 border-b border-neutral-300 pb-0.5 hover:text-pink-400 hover:border-pink-400 transition-colors">Kotak Masa Depan →</button>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 11: THE FUTURE                      -->
        <!-- ========================================== -->
        <section id="ch-11" class="chapter-section flex-col items-center justify-center text-center space-y-6">
            <div class="space-y-1">
                <h2 class="serif-text text-xl italic text-neutral-700">The Future Box</h2>
                <p class="text-[11px] text-neutral-400">Do Not Open Until...</p>
            </div>

            <div class="glass-card p-6 rounded-2xl border-white w-full max-w-xs space-y-4">
                <!-- Indikator Target Waktu Konten Spesial (Ulang Tahun) -->
                <div class="text-sm font-medium tracking-widest text-pink-400">🎂 HARI ULANG TAHUN</div>
                <div id="lock-status-ui" class="text-xs text-neutral-500">Mengecek gerbang waktu...</div>
                
                <!-- Tombol Akses Waktu -->
                <button id="btn-open-future" class="hidden w-full py-2.5 rounded-xl text-xs bg-pink-100 text-pink-500 border border-pink-200 font-medium tracking-wider hover:bg-pink-200 transition-colors">
                    Buka Kotak Hadiah 🎁
                </button>
            </div>

            <button onclick="changeChapter(13)" class="text-[11px] tracking-widest text-neutral-400 hover:text-neutral-500 transition-colors">Lewati & Selesaikan →</button>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 12: BIRTHDAY UPDATE (SPECIAL)      -->
        <!-- ========================================== -->
        <section id="ch-12" class="chapter-section flex-col items-center justify-center text-center space-y-8 animate-bloom">
            <div class="space-y-2">
                <span class="text-3xl animate-bounce block">✨🎉🎂</span>
                <h2 class="serif-text text-2xl italic text-pink-500 font-medium">Happy Birthday for You!</h2>
                <p class="text-xs text-neutral-400 max-w-xs mx-auto">Hari ini duniamu dipenuhi kebahagiaan. Aku punya kue kecil berisikan harapan tulus khusus untukmu.</p>
            </div>

            <!-- Interactive Cake Component -->
            <div id="birthday-cake" onclick="blowCandle()" class="cursor-pointer relative py-6 flex flex-col items-center">
                <!-- Candle Flame -->
                <div id="candle-flame" class="flame w-3 h-5 bg-amber-400 rounded-full absolute top-0 filter blur-[0.5px]"></div>
                <!-- Candle Wick & Body -->
                <div class="w-1.5 h-6 bg-pink-300 -mt-1 rounded-t-sm"></div>
                <!-- Cake Base -->
                <div class="w-32 h-14 bg-white border border-pink-100 shadow-sm rounded-xl flex items-center justify-center relative mt-0.5">
                    <div class="absolute inset-x-0 top-3 h-2 bg-pink-100"></div>
                    <span class="text-xs text-pink-400 font-medium tracking-widest serif-text z-10">MAKE A WISH</span>
                </div>
                <div class="text-[10px] text-neutral-400 tracking-wider mt-4" id="cake-instruction">Tiup lilin dengan mengetuk kuenya!</div>
            </div>

            <!-- Hidden Celebration Wish Content -->
            <div id="birthday-wishes-box" class="hidden glass-card p-6 rounded-2xl border-white text-left space-y-3 max-w-sm opacity-0 transition-opacity duration-1000">
                <span class="text-[10px] tracking-widest text-pink-400 font-semibold block">💌 A SPECIAL NOTE FOR YOU:</span>
                <p class="text-xs text-neutral-600 leading-relaxed serif-text italic">
                    "Selamat ulang tahun ya. Terima kasih banyak sudah bertahan, bertumbuh, dan berjalan sejauh ini. Semoga langkahmu ke depan selalu dipenuhi kehangatan dan senyuman indah. You deserve all the love in the universe."
                </p>
                <div class="pt-2 text-right">
                    <button onclick="changeChapter(13)" class="text-[11px] tracking-widest text-pink-400 font-medium hover:underline">Menuju Akhir Halaman →</button>
                </div>
            </div>
        </section>

        <!-- ========================================== -->
        <!-- CHAPTER 13: THE ENDING                     -->
        <!-- ========================================== -->
        <section id="ch-13" class="chapter-section flex-col items-center justify-center text-center space-y-6">
            <div id="ending-content" class="space-y-4 max-w-xs transition-opacity duration-1000">
                <h2 class="serif-text text-xl italic text-neutral-700">Thank you for taking your time.</h2>
                <p class="text-xs text-neutral-400 leading-relaxed">I hope this little place made you smile.</p>
                <button onclick="triggerOneLastClick()" class="glass-card px-6 py-2.5 rounded-full text-xs tracking-widest text-pink-400 font-medium hover:bg-white transition-colors mt-4">
                    ❤️ One Last Click
                </button>
            </div>
            
            <div id="final-message" class="hidden opacity-0 space-y-3 max-w-xs transition-opacity duration-2000">
                <p class="serif-text text-sm text-neutral-600 italic">There are millions of websites on the internet.</p>
                <p class="text-xs text-pink-400 font-medium tracking-wide">But this one only exists because of you.</p>
            </div>
        </section>

        <!-- ========================================== -->
        <!-- DEVELOPER ROOM (SECRET AREA)               -->
        <!-- ========================================== -->
        <section id="ch-dev" class="chapter-section flex-col items-center justify-center text-center space-y-6">
            <div class="glass-card p-8 rounded-2xl border-white w-full max-w-xs text-left space-y-4">
                <h3 class="serif-text text-sm font-semibold tracking-wider text-neutral-700">🛠️ DEVELOPER ROOM</h3>
                <div class="border-l-2 border-pink-200 pl-4 space-y-3 text-xs text-neutral-500">
                    <div>
                        <span class="block text-[10px] uppercase text-neutral-400 tracking-wider">Project Name</span>
                        <span class="font-medium text-neutral-700">Project Gerbera</span>
                    </div>
                    <div>
                        <span class="block text-[10px] uppercase text-neutral-400 tracking-wider">Started Date</span>
                        <span class="font-medium text-neutral-700">15 July 2026</span>
                    </div>
                    <div>
                        <span class="block text-[10px] uppercase text-neutral-400 tracking-wider">Created By</span>
                        <span class="font-medium text-neutral-700">Valentino_</span>
                    </div>
                </div>
                <button onclick="changeChapter(1)" class="w-full text-center text-[10px] text-neutral-400 tracking-widest pt-2 hover:text-pink-400 transition-colors">Kembali ke Beranda</button>
            </div>
        </section>

    </main>

    <!-- FOOTER MOTO SUBTITLE -->
    <footer class="w-full text-center py-6 text-[10px] tracking-widest text-neutral-300">
        Made with time, not just code.
    </footer>

    <!-- INTERACTIVE APP JAVASCRIPT LOGIC -->
    <script>
        // System State
        let currentChapter = 1;
        let collectedGerberas = new Set();
        let devClicks = 0;
        
        // DOM Handles
        const ambienceAudio = document.getElementById('audio-ambience');
        const bgmAudio = document.getElementById('audio-bgm');

        // --- CHAPTER 1 TIMELINE LOGIC ---
        const introTexts = ["hey...", "i made something.", "just for you.", "take your time."];
        let introIdx = 0;

        function playIntroSequence() {
            // Trigger audio ambience hujan pada interaksi ketukan pertama di layar
            document.body.addEventListener('click', () => {
                if(ambienceAudio.paused) ambienceAudio.play().catch(e => console.log("Audio play blocked"));
            }, { once: true });

            const interval = setInterval(() => {
                introIdx++;
                const el = document.getElementById('entrance-text');
                if (introIdx < introTexts.length) {
                    el.style.opacity = 0;
                    setTimeout(() => {
                        el.textContent = introTexts[introIdx];
                        el.style.opacity = 1;
                    }, 600);
                } else {
                    clearInterval(interval);
                    const btn = document.getElementById('btn-open-gift');
                    btn.classList.remove('pointer-events-none');
                    btn.style.opacity = 1;
                    btn.classList.remove('scale-95');
                }
            }, 3200);
        }

        // Initialize Intro
        window.addEventListener('DOMContentLoaded', () => {
            playIntroSequence();
            checkFutureTimeline();
        });

        // Open Gift Button Click Action
        document.getElementById('btn-open-gift').addEventListener('click', () => {
            fadeOutAudio(ambienceAudio, 1500);
            setTimeout(() => {
                bgmAudio.volume = 0;
                bgmAudio.play().catch(e => console.log("BGM Audio blocked"));
                fadeInAudio(bgmAudio, 2500);
            }, 800);
            changeChapter(2);
        });

        // --- GLOBAL CHAPTER CORE NAVIGATION ---
        function changeChapter(targetChNum) {
            const currentEl = document.getElementById(`ch-${currentChapter}`);
            const targetEl = document.getElementById(`ch-${targetChNum}`);

            if(currentEl) currentEl.style.opacity = 0;
            
            setTimeout(() => {
                if(currentEl) currentEl.classList.remove('active');
                if(targetEl) {
                    targetEl.classList.add('active');
                    // Trigger reflow untuk animasi transition opacity Tailwind
                    targetEl.offsetHeight; 
                    targetEl.style.opacity = 1;
                    currentChapter = targetChNum;
                    executeChapterCallback(targetChNum);
                }
            }, 1200);
        }

        // Lifecycle Callback Tiap Masuk Halaman Baru
        function executeChapterCallback(ch) {
            if (ch === 2) {
                const box = document.getElementById('gift-box');
                const msg = document.getElementById('gift-message');
                box.addEventListener('click', () => {
                    box.style.transform = 'scale(0)';
                    box.style.opacity = 0;
                    setTimeout(() => {
                        box.classList.add('hidden');
                        msg.classList.remove('hidden');
                        msg.offsetHeight;
                        msg.style.opacity = 1;
                    }, 500);
                }, { once: true });
            }
            if (ch === 3) {
                runTypewriterAnimation("Hi.\nMakasih ya.\nKarena tanpa kamu.\nWebsite ini nggak akan pernah ada.");
            }
        }

        // --- CHAPTER 3: TYPEWRITER LOGIC ---
        function runTypewriterAnimation(str) {
            const container = document.getElementById('typewriter-text');
            container.innerHTML = "";
            let i = 0;
            function type() {
                if (i < str.length) {
                    container.innerHTML += str.charAt(i) === '\n' ? '<br>' : str.charAt(i);
                    i++;
                    setTimeout(type, 65);
                } else {
                    const nav = document.getElementById('letter-nav');
                    nav.style.opacity = 1;
                }
            }
            type();
        }

        // --- CHAPTER 4: INTERACTIVE GARDEN POPUP ---
        function tapGardenFlower(phrase) {
            const bubble = document.getElementById('garden-bubble');
            bubble.textContent = phrase;
            bubble.style.opacity = 1;
            setTimeout(() => { bubble.style.opacity = 0; }, 3000);
        }

        // --- CHAPTER 5: POLAROID PHOTO DEVELOPMENT ---
        function developPolaroid(cardEl) {
            const innerBg = cardEl.querySelector('.bg-neutral-200');
            const img = cardEl.querySelector('.photo-img');
            const prompt = cardEl.querySelector('.develop-prompt');
            
            if (prompt) prompt.style.opacity = 0;
            if (innerBg) innerBg.style.backgroundColor = '#ffffff';
            if (img) img.style.opacity = 1;
        }

        // --- CHAPTER 6: WISH BALLOON SYSTEMS ---
        function popWish(text, btnEl) {
            document.getElementById('wish-display').textContent = text;
            btnEl.style.transform = 'scale(0.2)';
            btnEl.style.opacity = '0';
            btnEl.style.pointerEvents = 'none';
        }

        // --- CHAPTER 7: STAR OBSERVATORY GENERATOR ---
        const starPhrases = ["you’re enough. ✨", "i’m proud of you. 🤍", "don’t overthink. 🌌", "thank you. 💕"];
        let starIdx = 0;

        document.getElementById('sky-canvas').addEventListener('click', function(e) {
            const rect = this.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;

            // Buat elemen bintang baru berbentuk HTML bulat kecil
            const star = document.createElement('div');
            star.className = 'absolute w-1.5 h-1.5 bg-white rounded-full transition-opacity duration-1000 animate-ping';
            star.style.left = `${x}px`;
            star.style.top = `${y}px`;
            this.appendChild(star);

            document.getElementById('star-message').textContent = starPhrases[starIdx];
            starIdx = (starIdx + 1) % starPhrases.length;
        });

        // --- CHAPTER 8 & 9: HIDDEN ROOM & GERBERA HUNT SYSTEM ---
        function collectGerbera(id, el) {
            if (!collectedGerberas.has(id)) {
                collectedGerberas.add(id);
                el.style.opacity = "1";
                el.style.color = "#ec4899"; // Warnai pink cerah menandakan terambil
                
                const counterUI = document.getElementById('hunt-counter-ui');
                counterUI.classList.remove('hidden');
                document.getElementById('hunt-count').textContent = collectedGerberas.size;

                if (collectedGerberas.size === 5) {
                    alert("You found something... Secret unlocked! 🌼");
                    changeChapter(9);
                }
            }
        }

        function promptHiddenRoom() {
            const pass = prompt("Masukkan kata sandi khusus:");
            if(pass && pass.toLowerCase() === 'gerbera') {
                changeChapter(9);
            } else if (pass) {
                alert("Kata sandi salah... Coba cari bunga tersembunyi!");
            }
        }

        function enterFromHidden() {
            // Kembali ke halaman normal setelah membuka hidden room
            changeChapter(10);
        }

        // --- CHAPTER 10: JAR OF HEARTS (100 MESSAGES RANDOM) ---
        const randomMessages = [
            "i’m always rooting for you. 🤍",
            "don’t skip your meals. 🍳",
            "thank you for being born. ✨",
            "i’m proud of you. 💕",
            "kamu berharga, jangan lupa ya. 🥺",
            "take it easy, satu langkah demi satu langkah. 🍃",
            "semoga harimu menyenangkan hari ini! ☀️",
            "i believe in you, always. 🌸"
            // Kamu bisa memperbanyak isi array ini sampai 100 pesan sesuai keinginan
        ];

        function openHeartJar() {
            const randIdx = Math.floor(Math.random() * randomMessages.length);
            const display = document.getElementById('jar-message-display');
            display.style.opacity = 0;
            setTimeout(() => {
                display.textContent = randomMessages[randIdx];
                display.style.opacity = 1;
            }, 300);
        }

        // --- CHAPTER 11 & 12: FUTURE GATE & INTERACTIVE BIRTHDAY CAKE ---
        function checkFutureTimeline() {
            // Kita atur target rilis, misalnya tanggal 15 Juli 2026
            const targetDate = new Date('2026-07-15T00:00:00');
            const currentDate = new Date();

            const statusUI = document.getElementById('lock-status-ui');
            const openBtn = document.getElementById('btn-open-future');

            if (currentDate >= targetDate) {
                statusUI.textContent = "Waktunya tiba! Kotak hadiah masa depan bisa dibuka.";
                openBtn.classList.remove('hidden');
                openBtn.onclick = () => { changeChapter(12); };
            } else {
                statusUI.innerHTML = "Not yet.<br><span class='text-[10px] text-neutral-400'>See you soon.</span>";
            }
        }

        function blowCandle() {
            const flame = document.getElementById('candle-flame');
            const instruction = document.getElementById('cake-instruction');
            const wishBox = document.getElementById('birthday-wishes-box');

            if(flame) {
                flame.style.display = 'none';
                instruction.textContent = "Lilin telah padam, harapanmu terkirim. ✨";
                
                // Munculkan surat ucapan ulang tahun di bawahnya
                wishBox.classList.remove('hidden');
                wishBox.offsetHeight;
                wishBox.style.opacity = 1;
            }
        }

        // --- CHAPTER 13: ENDING ANIMATION CLOSING ---
        function triggerOneLastClick() {
            document.getElementById('ending-content').style.opacity = 0;
            setTimeout(() => {
                document.getElementById('ending-content').classList.add('hidden');
                const finalMsg = document.getElementById('final-message');
                finalMsg.classList.remove('hidden');
                finalMsg.offsetHeight;
                finalMsg.style.opacity = 1;
            }, 1000);
        }

        // --- DEVELOPER ROOM ENGINE TRIGGER (7 Clicks) ---
        document.getElementById('dev-trigger').addEventListener('click', () => {
            devClicks++;
            if(devClicks === 7) {
                devClicks = 0;
                changeChapter('dev');
            }
        });

        // --- UTILITY AUDIO FADE MECHANISMS ---
        function fadeOutAudio(audio, ms) {
            let startVol = audio.volume;
            let step = startVol / (ms / 30);
            let timer = setInterval(() => {
                if (audio.volume > step) {
                    audio.volume -= step;
                } else {
                    audio.volume = 0;
                    audio.pause();
                    clearInterval(timer);
                }
            }, 30);
        }

        function fadeInAudio(audio, ms) {
            let targetVol = 0.4; // Batas volume aman
            audio.volume = 0;
            let step = targetVol / (ms / 30);
            let timer = setInterval(() => {
                if (audio.volume < targetVol) {
                    audio.volume += step;
                } else {
                    audio.volume = targetVol;
                    clearInterval(timer);
                }
            }, 30);
        }
    </script>
</body>
</html>
