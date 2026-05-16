<!DOCTYPE html>
<html lang="ar" dir="rtl">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>لعبة بناء الجسر التعليمية</title>
    <!-- تضمين مكتبة Tailwind CSS للتنسيق المتجاوب والأنيق -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- تضمين خط Cairo الجميل المخصص للأطفال -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700;900&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Cairo', sans-serif;
            background-image: radial-gradient(#d1d5db 1px, transparent 1px);
            background-size: 40px 40px;
        }

        @keyframes shake {

            0%,
            100% {
                transform: translateX(0);
            }

            25% {
                transform: translateX(-6px);
            }

            75% {
                transform: translateX(6px);
            }
        }

        .animate-shake {
            animation: shake 0.2s ease-in-out infinite;
        }

        .animate-bounce-slow {
            animation: bounce 1.5s infinite;
        }
    </style>
</head>

<body
    class="min-h-screen bg-cover bg-center flex flex-col items-center justify-between p-3 sm:p-6 relative overflow-hidden transition-all duration-500"
    style="background-image: linear-gradient(rgba(255,255,255,0.2), rgba(255,255,255,0.2)), url('https://img.freepik.com/free-vector/nature-forest-landscape-background-scene_1308-72433.jpg');">

    <!-- شاشة البداية (Intro Screen) -->
    <div id="intro-screen"
        class="my-auto bg-white/95 p-6 sm:p-8 rounded-[2rem] sm:rounded-[2.5rem] shadow-2xl text-center max-w-sm w-full border-8 border-yellow-400 animate-in zoom-in duration-300 z-10">
        <div class="text-5xl sm:text-6xl mb-4 animate-bounce text-blue-500">🏃‍♂️</div>
        <h1 class="text-2xl sm:text-3xl font-black text-blue-600 mb-3">بناء الجسر العجيب</h1>
        <p class="text-gray-600 mb-6 font-bold text-sm sm:text-base">ساعد صديقنا ماريو في عبور النهر!</p>
        <button id="start-btn"
            class="w-full sm:w-auto bg-green-500 hover:bg-green-600 text-white font-black py-3.5 px-8 rounded-2xl text-lg sm:text-xl shadow-[0_6px_0_rgb(21,128,61)] active:shadow-none active:translate-y-1.5 transition-all">
            إبدأ المغامرة!
        </button>
    </div>

    <!-- منطقة اللعب (Game Area) - مخفية افتراضياً -->
    <div id="game-screen" class="hidden w-full max-w-2xl flex flex-col gap-3 sm:gap-4 my-auto z-10">

        <!-- لوحة الأسئلة المتجاوبة -->
        <div
            class="bg-white/95 backdrop-blur-sm rounded-2xl sm:rounded-3xl shadow-xl p-4 sm:p-6 border-b-8 border-blue-400 relative">
            <div
                class="absolute -top-3 right-6 sm:right-8 bg-blue-500 text-white px-3 sm:px-4 py-1 rounded-full text-[10px] sm:text-xs font-bold flex items-center gap-1.5">
                <span>سؤال <span id="question-number">1</span></span>
                <!-- أيقونة الصوت تظهر وتنبض عند التحدث -->
                <svg id="speaker-icon" class="w-3.5 h-3.5 text-white hidden animate-pulse" fill="none"
                    stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5"
                        d="M15.536 8.464a5 5 0 010 7.072M18.364 5.636a9 9 0 010 12.728M12 18.75V5.25L7.75 9.5H4.5v5h3.25L12 18.75z" />
                </svg>
            </div>

            <h2 id="question-text"
                class="text-lg sm:text-xl md:text-2xl font-bold text-gray-800 mb-4 sm:mb-6 text-center mt-2">
                جاري تحميل السؤال...
            </h2>

            <!-- خيارات الإجابة -->
            <div id="options-container" class="grid grid-cols-2 gap-2 sm:gap-3">
                <!-- سيتم توليد الأزرار ديناميكياً بواسطة الجافاسكربت -->
            </div>
        </div>

        <!-- مشهد الجسر والنهر المتجاوب -->
        <div
            class="relative h-32 sm:h-40 md:h-48 bg-blue-400/30 backdrop-blur-[2px] rounded-[1.5rem] sm:rounded-[2rem] overflow-hidden border-4 border-white shadow-lg flex items-end">
            <!-- الضفة اليسرى -->
            <div class="w-12 sm:w-16 h-full bg-green-500 z-10 shadow-lg"></div>

            <!-- مساحة النهر والجسر -->
            <div
                class="flex-1 h-3/4 relative flex items-center justify-start bg-gradient-to-b from-cyan-400/40 to-blue-500/40">
                <!-- الجسر -->
                <div id="bridge-element"
                    class="h-3 sm:h-4 bg-yellow-800 flex items-center absolute left-0 z-10 transition-all duration-700 shadow-md"
                    style="width: 0%;">
                    <div id="bridge-lines" class="w-full h-full border-y-2 border-yellow-950 flex justify-around px-1">
                        <!-- تضاف العوارض الخشبية تلقائياً -->
                    </div>
                </div>

                <!-- ماريو وحركته المتناسقة -->
                <div id="mario-character" class="absolute z-20 transition-all duration-1000 ease-in-out transform"
                    style="left: calc(0% - 20px); bottom: 8px;">
                    <div id="mario-emoji" class="text-3xl sm:text-4xl md:text-5xl drop-shadow-xl animate-bounce-slow">
                        🚶‍♂️</div>
                </div>
            </div>

            <!-- الضفة اليمنى -->
            <div class="w-12 sm:w-16 h-full bg-green-500 z-10 flex items-center justify-center text-2xl sm:text-3xl">🚩
            </div>

            <!-- تغذية صح أو خطأ -->
            <div id="feedback-overlay"
                class="absolute inset-0 z-50 flex items-center justify-center bg-white/20 hidden">
                <!-- أيقونة صح -->
                <svg id="correct-icon"
                    class="w-14 h-14 sm:w-20 sm:h-20 text-green-500 bg-white rounded-full p-2 shadow-2xl animate-bounce hidden"
                    fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 13l4 4L19 7" />
                </svg>
                <!-- أيقونة خطأ -->
                <svg id="wrong-icon"
                    class="w-14 h-14 sm:w-20 sm:h-20 text-red-500 bg-white rounded-full p-2 shadow-2xl animate-shake hidden"
                    fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M6 18L18 6M6 6l12 12" />
                </svg>
            </div>
        </div>
    </div>

    <!-- شاشة الفوز (Finished Screen) - مخفية افتراضياً -->
    <div id="win-screen"
        class="hidden my-auto bg-white/95 p-6 sm:p-8 rounded-[2rem] sm:rounded-[2.5rem] shadow-2xl text-center max-w-sm w-full border-8 border-yellow-400 animate-in zoom-in duration-300 z-10">
        <svg class="w-16 h-16 sm:w-20 sm:h-20 text-yellow-500 mx-auto mb-4 animate-pulse" fill="none"
            stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M12 8v13m0-13V6a2 2 0 112 2h-2zm0 0V5a2 2 0 10-2 2h2zm0 0h4m-4 0H8m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />
        </svg>
        <h1 class="text-xl sm:text-2xl font-black text-blue-700 mb-6">أحسنت يا بطل!</h1>
        <button id="restart-btn"
            class="flex items-center justify-center gap-2 w-full bg-blue-600 text-white font-black py-3.5 rounded-2xl text-lg sm:text-xl shadow-[0_6px_0_rgb(30,58,138)] active:shadow-none active:translate-y-1.5 transition-all">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3"
                    d="M4 4v5h.582m15.356 2A8.001 8.001 0 1121.21 8H17" />
            </svg>
            العب مرة ثانية
        </button>
    </div>

    <!-- تذييل الصفحة -->
    <div class="text-[10px] sm:text-xs text-white/80 font-bold bg-black/30 px-3 py-1 rounded-full z-10 mb-2">
        لعبة بناء الجسر للأطفال 🎮
    </div>

    <!-- منطق اللعبة والربط البرمجي الكامل مع واجهة Gemini TTS -->
    <script>
        // مفتاح الـ API الخاص بك
        const apiKey = "AIzaSyDRvPqkaO-wymRxaA6OOk9sBSCy_xfW5wA";

        // الأسئلة والخيارات
        const questions = [
            {
                question: "ما هو ناتج 5 + 5؟",
                options: ["8", "10", "12", "15"],
                correct: 1
            },
            {
                question: "ما هو لون السماء؟",
                options: ["أحمر", "أزرق", "أخضر", "أصفر"],
                correct: 1
            },
            {
                question: "كم عدد أيام الأسبوع؟",
                options: ["5", "6", "7", "8"],
                correct: 2
            },
            {
                question: "عاصمة مصر هي مدينة...",
                options: ["الإسكندرية", "أسوان", "القاهرة", "طنطا"],
                correct: 2
            },
            {
                question: "سفينة الصحراء هو...",
                options: ["الحصان", "الجمل", "الأسد", "الفيل"],
                correct: 1
            }
        ];

        // حالة اللعبة الحالية
        let currentStep = 0;
        let currentQuestionIndex = 0;
        let isSpeaking = false;
        let audioPlayer = null;
        const totalSteps = questions.length;

        // عناصر واجهة المستخدم
        const introScreen = document.getElementById('intro-screen');
        const gameScreen = document.getElementById('game-screen');
        const winScreen = document.getElementById('win-screen');
        const startBtn = document.getElementById('start-btn');
        const restartBtn = document.getElementById('restart-btn');
        const questionText = document.getElementById('question-text');
        const questionNumber = document.getElementById('question-number');
        const optionsContainer = document.getElementById('options-container');
        const bridgeElement = document.getElementById('bridge-element');
        const bridgeLines = document.getElementById('bridge-lines');
        const marioCharacter = document.getElementById('mario-character');
        const marioEmoji = document.getElementById('mario-emoji');
        const speakerIcon = document.getElementById('speaker-icon');
        const feedbackOverlay = document.getElementById('feedback-overlay');
        const correctIcon = document.getElementById('correct-icon');
        const wrongIcon = document.getElementById('wrong-icon');

        // دالة نطق الكلام باستخدام Gemini TTS
        async function speakText(text) {
            if (!text || !apiKey) return;
            try {
                isSpeaking = true;
                toggleSpeakerAnimation(true);
                disableButtons(true);

                const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-tts:generateContent?key=${apiKey}`, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({
                        contents: [{ parts: [{ text: `بصوت مبهج جداً للأطفال، انطق بوضوح ورتم متوسط: ${text}` }] }],
                        generationConfig: {
                            responseModalities: ["AUDIO"],
                            speechConfig: {
                                voiceConfig: {
                                    prebuiltVoiceConfig: { voiceName: "Kore" }
                                }
                            }
                        }
                    })
                });

                const result = await response.json();
                const audioData = result.candidates?.[0]?.content?.parts?.[0]?.inlineData?.data;

                if (audioData) {
                    const audioBlob = await pcmToWav(audioData, 24000);
                    const audioUrl = URL.createObjectURL(audioBlob);

                    if (audioPlayer) {
                        audioPlayer.pause();
                    }

                    audioPlayer = new Audio(audioUrl);
                    audioPlayer.onended = () => {
                        isSpeaking = false;
                        toggleSpeakerAnimation(false);
                        disableButtons(false);
                    };
                    await audioPlayer.play();
                } else {
                    isSpeaking = false;
                    toggleSpeakerAnimation(false);
                    disableButtons(false);
                }
            } catch (error) {
                console.error("TTS Error:", error);
                isSpeaking = false;
                toggleSpeakerAnimation(false);
                disableButtons(false);
            }
        }

        // مساعد تحويل PCM إلى WAV للتشغيل الفوري في المتصفح
        async function pcmToWav(base64Pcm, sampleRate) {
            const pcmData = Uint8Array.from(atob(base64Pcm), c => c.charCodeAt(0)).buffer;
            const wavHeader = new ArrayBuffer(44);
            const view = new DataView(wavHeader);
            const writeString = (offset, string) => {
                for (let i = 0; i < string.length; i++) view.setUint8(offset + i, string.charCodeAt(i));
            };
            writeString(0, 'RIFF');
            view.setUint32(4, 32 + pcmData.byteLength, true);
            writeString(8, 'WAVE');
            writeString(12, 'fmt ');
            view.setUint32(16, 16, true);
            view.setUint16(20, 1, true);
            view.setUint16(22, 1, true);
            view.setUint32(24, sampleRate, true);
            view.setUint32(28, sampleRate * 2, true);
            view.setUint16(32, 2, true);
            view.setUint16(34, 16, true);
            writeString(36, 'data');
            view.setUint32(40, pcmData.byteLength, true);
            return new Blob([wavHeader, pcmData], { type: 'audio/wav' });
        }

        // إظهار وإخفاء أيقونة مكبر الصوت المنبض
        function toggleSpeakerAnimation(show) {
            if (show) {
                speakerIcon.classList.remove('hidden');
            } else {
                speakerIcon.classList.add('hidden');
            }
        }

        // تعطيل/تفعيل أزرار الإجابات أثناء التحدث
        function disableButtons(disable) {
            const buttons = optionsContainer.querySelectorAll('button');
            buttons.forEach(btn => {
                if (disable) {
                    btn.disabled = true;
                    btn.classList.add('opacity-50', 'cursor-not-allowed');
                } else {
                    btn.disabled = false;
                    btn.classList.remove('opacity-50', 'cursor-not-allowed');
                }
            });
        }

        // تحميل سؤال جديد وتحديث الواجهة
        function loadQuestion() {
            const q = questions[currentQuestionIndex];
            questionNumber.textContent = currentQuestionIndex + 1;
            questionText.textContent = q.question;

            // توليد خيارات الإجابة
            optionsContainer.innerHTML = '';
            q.options.forEach((option, idx) => {
                const btn = document.createElement('button');
                btn.className = "py-2.5 sm:py-3.5 px-3 sm:px-4 rounded-xl text-sm sm:text-base md:text-lg font-bold transition-all duration-150 touch-manipulation bg-blue-50 hover:bg-yellow-100 text-blue-700 border-2 border-blue-200 border-b-4 active:border-b-0 active:translate-y-1 shadow-sm";
                btn.textContent = option;
                btn.onclick = () => handleAnswer(idx);
                optionsContainer.appendChild(btn);
            });

            // تحديث حركة الجسر وماريو
            updateBridgeAndMario();

            // نطق السؤال والخيارات
            const textToSpeak = `${q.question}. الخيارات هي: ${q.options.join("... ")}`;
            speakText(textToSpeak);
        }

        // تحديث بناء الجسر وموضع ماريو
        function updateBridgeAndMario() {
            const percentage = (currentStep / totalSteps) * 100;
            bridgeElement.style.width = `${percentage}%`;
            marioCharacter.style.left = `calc(${percentage}% - 20px)`;

            // إعادة رسم عوارض الخشب داخل الجسر لتتناسب مع الطول
            bridgeLines.innerHTML = '';
            const numLines = Math.max(1, currentStep * 5);
            for (let i = 0; i < numLines; i++) {
                const line = document.createElement('div');
                line.className = "w-0.5 sm:w-1 h-full bg-yellow-950/30";
                bridgeLines.appendChild(line);
            }
        }

        // معالجة اختيار الإجابة
        function handleAnswer(index) {
            if (isSpeaking) return;

            const q = questions[currentQuestionIndex];
            if (index === q.correct) {
                // إجابة صحيحة
                showFeedback('correct');
                marioEmoji.textContent = '🏃‍♂️';
                speakText("إجابة صحيحة! أحسنت يا بطل، أنت ذكي جداً");

                setTimeout(() => {
                    hideFeedback();
                    marioEmoji.textContent = '🚶‍♂️';
                    currentStep += 1;
                    if (currentQuestionIndex < questions.length - 1) {
                        currentQuestionIndex += 1;
                        loadQuestion();
                    } else {
                        // الفوز باللعبة
                        endGame();
                    }
                }, 2000);
            } else {
                // إجابة خاطئة
                showFeedback('wrong');
                marioEmoji.textContent = '😲';
                speakText("أوووه! حاول مرة ثانية، أنا أعرف أنك تستطيع");

                setTimeout(() => {
                    hideFeedback();
                    marioEmoji.textContent = '🚶‍♂️';
                }, 2000);
            }
        }

        // إظهار علامات التقييم البصري للطفل
        function showFeedback(type) {
            feedbackOverlay.classList.remove('hidden');
            if (type === 'correct') {
                correctIcon.classList.remove('hidden');
                wrongIcon.classList.add('hidden');
            } else {
                wrongIcon.classList.remove('hidden');
                correctIcon.classList.add('hidden');
            }
        }

        function hideFeedback() {
            feedbackOverlay.classList.add('hidden');
            correctIcon.classList.add('hidden');
            wrongIcon.classList.add('hidden');
        }

        // بدء اللعبة من شاشة الترحيب
        startBtn.onclick = () => {
            introScreen.classList.add('hidden');
            gameScreen.classList.remove('hidden');
            speakText("هيا بنا لنبدأ مغامرة بناء الجسر العجيبة!");
            loadQuestion();
        };

        // نهاية اللعبة بنجاح
        function endGame() {
            updateBridgeAndMario(); // تأكيد اكتمال الجسر تماماً
            gameScreen.classList.add('hidden');
            winScreen.classList.remove('hidden');
            speakText("مبروك! لقد بنيت الجسر بالكامل وساعدت ماريو في العبور. أنت رائع!");
        }

        // إعادة تشغيل اللعبة
        restartBtn.onclick = () => {
            currentStep = 0;
            currentQuestionIndex = 0;
            winScreen.classList.add('hidden');
            gameScreen.classList.remove('hidden');
            loadQuestion();
        };
    </script>
</body>

</html>
