<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FOUR BEASTS</title>

    <style>
        * {
            box-sizing: border-box;
        }

        html,
        body {
            margin: 0;
            padding: 0;
            width: 100%;
            min-height: 100%;
        }

        body {
            font-family: Arial, "Noto Sans KR", sans-serif;
            background:
                radial-gradient(circle at center, #8f1717 0%, #4d0808 45%, #190303 100%);
            color: #ffd95a;
            overflow-x: hidden;
        }

        /* 전체 배경 장식 */
        body::before {
            content: "";
            position: fixed;
            inset: 0;
            pointer-events: none;
            opacity: 0.18;
            background-image:
                radial-gradient(circle, #ffd700 1px, transparent 2px),
                radial-gradient(circle, #ffffff 1px, transparent 2px);
            background-size: 55px 55px, 83px 83px;
            background-position: 0 0, 20px 30px;
        }

        .game-wrapper {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 30px 15px;
        }

        /* 슬롯머신 본체 */
        .machine {
            position: relative;
            width: min(1000px, 96vw);
            padding: 35px 35px 45px;

            background:
                linear-gradient(
                    135deg,
                    #8f0d0d,
                    #d02020 25%,
                    #760909 50%,
                    #b81818 75%,
                    #620606
                );

            border: 8px solid #e7b72e;
            border-radius: 28px;

            box-shadow:
                0 0 0 5px #651008,
                0 0 0 9px #f6d45c,
                0 20px 60px rgba(0, 0, 0, 0.8),
                inset 0 0 35px rgba(0, 0, 0, 0.65);

            overflow: hidden;
        }

        /* 금색 장식 */
        .machine::before {
            content: "";
            position: absolute;
            inset: 12px;
            border: 2px solid rgba(255, 224, 102, 0.65);
            border-radius: 18px;
            pointer-events: none;
        }

        .machine::after {
            content: "☁  ✦  ☁  ✦  ☁  ✦  ☁";
            position: absolute;
            top: 8px;
            left: 0;
            width: 100%;
            text-align: center;
            font-size: 18px;
            color: #ffe88a;
            opacity: 0.8;
            pointer-events: none;
        }

        /* 제목 */
        .title-area {
            position: relative;
            text-align: center;
            margin-bottom: 28px;
            z-index: 2;
        }

        .title {
            margin: 0;
            font-size: clamp(34px, 6vw, 68px);
            font-weight: 900;
            letter-spacing: 7px;

            color: #fff2a8;

            text-shadow:
                0 2px 0 #8b4b00,
                0 4px 0 #6b2600,
                0 0 8px #ffd700,
                0 0 20px #ffae00,
                0 0 35px #ff7b00;
        }

        .subtitle {
            margin-top: 5px;
            font-size: 13px;
            letter-spacing: 6px;
            color: #ffd65a;
            text-shadow: 0 0 10px #ff9d00;
        }

        /* 장식선 */
        .gold-line {
            display: flex;
            align-items: center;
            gap: 12px;
            margin: 0 auto 25px;
            max-width: 750px;
        }

        .gold-line::before,
        .gold-line::after {
            content: "";
            flex: 1;
            height: 3px;
            background: linear-gradient(
                90deg,
                transparent,
                #ffd700,
                #fff3a0,
                #ffd700,
                transparent
            );
            box-shadow: 0 0 10px #ffd700;
        }

        .gold-line span {
            color: #fff0a0;
            font-size: 22px;
        }

        /* 릴 전체 프레임 */
        .reels-frame {
            position: relative;
            padding: 17px;

            background:
                linear-gradient(
                    135deg,
                    #6b3500,
                    #ffd84a,
                    #8e4a00,
                    #ffe36b,
                    #6c3200
                );

            border: 5px solid #ffe98a;
            border-radius: 18px;

            box-shadow:
                inset 0 0 18px rgba(0, 0, 0, 0.8),
                0 0 25px rgba(255, 190, 0, 0.5);
        }

        /* 슬롯 영역 */
        .reels {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;

            padding: 16px;

            background:
                linear-gradient(
                    180deg,
                    #260202,
                    #100000,
                    #260202
                );

            border: 4px solid #8f5b08;
            border-radius: 12px;

            box-shadow:
                inset 0 0 30px rgba(0, 0, 0, 0.95);
        }

        /* 각 슬롯 */
        .reel-window {
            position: relative;
            height: clamp(150px, 20vw, 230px);
            min-height: 130px;

            overflow: hidden;

            background:
                linear-gradient(
                    180deg,
                    #fff,
                    #f3f3f3 45%,
                    #d4d4d4
                );

            border: 5px solid #e8b92e;
            border-radius: 10px;

            box-shadow:
                inset 0 0 25px rgba(0, 0, 0, 0.55),
                0 0 12px rgba(255, 215, 0, 0.45);
        }

        /* 슬롯 중앙 표시 영역 */
        .reel-window::before,
        .reel-window::after {
            content: "";
            position: absolute;
            left: 0;
            width: 100%;
            height: 25%;
            z-index: 5;
            pointer-events: none;
        }

        .reel-window::before {
            top: 0;
            background: linear-gradient(
                180deg,
                rgba(0, 0, 0, 0.45),
                transparent
            );
        }

        .reel-window::after {
            bottom: 0;
            background: linear-gradient(
                0deg,
                rgba(0, 0, 0, 0.45),
                transparent
            );
        }

        /* 중앙 라인 */
        .center-line {
            position: absolute;
            left: 0;
            right: 0;
            top: 50%;
            height: 4px;
            transform: translateY(-50%);
            z-index: 8;

            background: rgba(255, 193, 7, 0.7);
            box-shadow:
                0 0 6px #ffbf00,
                0 0 15px #ff9900;

            pointer-events: none;
        }

        /* 실제 릴 */
        .reel {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;

            display: flex;
            flex-direction: column;
            align-items: center;

            transform: translateY(0);
            will-change: transform;
        }

        .symbol {
            width: 100%;
            height: clamp(150px, 20vw, 230px);
            min-height: 130px;

            flex-shrink: 0;

            display: flex;
            align-items: center;
            justify-content: center;

            font-size: clamp(70px, 10vw, 125px);
            line-height: 1;

            user-select: none;

            filter:
                drop-shadow(0 4px 2px rgba(0, 0, 0, 0.35))
                drop-shadow(0 0 8px rgba(255, 180, 0, 0.25));
        }

        /* 회전 중 */
        .reel.spinning .symbol {
            filter:
                blur(2px)
                drop-shadow(0 0 12px rgba(255, 190, 0, 0.6));
        }

        /* 정지할 때 */
        .reel.stopping {
            animation: stopShake 0.22s ease-out;
        }

        @keyframes stopShake {
            0% {
                transform: translateY(0);
            }

            25% {
                transform: translateY(5px);
            }

            50% {
                transform: translateY(-3px);
            }

            75% {
                transform: translateY(2px);
            }

            100% {
                transform: translateY(0);
            }
        }

        /* GO 버튼 */
        .button-area {
            display: flex;
            justify-content: center;
            margin-top: 30px;
        }

        .go-button {
            position: relative;

            width: 220px;
            height: 78px;

            border: 5px solid #ffe36b;
            border-radius: 18px;

            background:
                linear-gradient(
                    180deg,
                    #ffef7b 0%,
                    #f5b51b 35%,
                    #b96500 100%
                );

            color: #681000;

            font-size: 34px;
            font-weight: 1000;
            letter-spacing: 5px;

            cursor: pointer;

            box-shadow:
                0 8px 0 #713000,
                0 12px 25px rgba(0, 0, 0, 0.55),
                0 0 25px rgba(255, 211, 52, 0.7),
                inset 0 3px 5px rgba(255, 255, 255, 0.8);

            transition:
                transform 0.08s,
                filter 0.15s;
        }

        .go-button::before {
            content: "";
            position: absolute;
            top: 7px;
            left: 15%;
            width: 70%;
            height: 18px;

            border-radius: 50%;

            background: rgba(255, 255, 255, 0.35);
            filter: blur(4px);
        }

        .go-button:hover {
            filter: brightness(1.15);
            box-shadow:
                0 8px 0 #713000,
                0 12px 30px rgba(0, 0, 0, 0.55),
                0 0 35px rgba(255, 226, 80, 0.9);
        }

        .go-button:active {
            transform: translateY(7px);
            box-shadow:
                0 1px 0 #713000,
                0 5px 12px rgba(0, 0, 0, 0.5);
        }

        .go-button:disabled {
            cursor: not-allowed;
            filter: grayscale(0.35) brightness(0.7);
        }

        /* 결과 메시지 */
        .result {
            min-height: 58px;

            margin-top: 25px;

            display: flex;
            align-items: center;
            justify-content: center;

            text-align: center;

            font-size: 25px;
            font-weight: 900;
            letter-spacing: 3px;

            color: #ffe66d;

            text-shadow:
                0 0 8px #ffae00,
                0 0 18px #ff7300;

            transition: all 0.2s;
        }

        .result.jackpot {
            font-size: clamp(28px, 5vw, 52px);
            color: #fff4a5;

            animation:
                jackpotText 0.7s infinite alternate,
                jackpotShake 0.4s infinite;
        }

        @keyframes jackpotText {
            from {
                text-shadow:
                    0 0 8px #ffd700,
                    0 0 20px #ff9500;
            }

            to {
                text-shadow:
                    0 0 10px #ffffff,
                    0 0 25px #ffd700,
                    0 0 45px #ff7300;
            }
        }

        @keyframes jackpotShake {
            0% {
                transform: translateX(0);
            }

            25% {
                transform: translateX(-3px);
            }

            50% {
                transform: translateX(3px);
            }

            75% {
                transform: translateX(-2px);
            }

            100% {
                transform: translateX(0);
            }
        }

        /* 잭팟 효과 */
        .jackpot-effect {
            position: fixed;
            inset: 0;

            display: flex;
            align-items: center;
            justify-content: center;

            pointer-events: none;

            opacity: 0;
            z-index: 100;
        }

        .jackpot-effect.active {
            animation: jackpotOverlay 1.8s ease-out;
        }

        @keyframes jackpotOverlay {
            0% {
                opacity: 0;
                background: rgba(255, 215, 0, 0);
            }

            20% {
                opacity: 1;
                background: rgba(255, 215, 0, 0.25);
            }

            40% {
                opacity: 0.8;
                background: rgba(255, 255, 255, 0.12);
            }

            100% {
                opacity: 0;
                background: rgba(255, 215, 0, 0);
            }
        }

        /* 반짝이는 별 */
        .sparkles {
            position: absolute;
            inset: 0;
            pointer-events: none;
            overflow: hidden;
        }

        .sparkle {
            position: absolute;
            color: #fff5a0;
            font-size: 20px;
            opacity: 0;

            animation: sparkleMove 2.5s infinite;
            text-shadow: 0 0 10px #ffd700;
        }

        .sparkle:nth-child(1) {
            left: 8%;
            top: 15%;
            animation-delay: 0s;
        }

        .sparkle:nth-child(2) {
            left: 20%;
            top: 70%;
            animation-delay: 0.8s;
        }

        .sparkle:nth-child(3) {
            left: 45%;
            top: 10%;
            animation-delay: 1.4s;
        }

        .sparkle:nth-child(4) {
            left: 75%;
            top: 20%;
            animation-delay: 0.4s;
        }

        .sparkle:nth-child(5) {
            left: 90%;
            top: 70%;
            animation-delay: 1.8s;
        }

        @keyframes sparkleMove {
            0% {
                opacity: 0;
                transform: scale(0.2) rotate(0deg);
            }

            30% {
                opacity: 1;
            }

            60% {
                opacity: 0.8;
                transform: scale(1.3) rotate(90deg);
            }

            100% {
                opacity: 0;
                transform: scale(0.2) rotate(180deg);
            }
        }

        /* 모바일 */
        @media (max-width: 650px) {
            .machine {
                padding: 25px 15px 35px;
                border-width: 5px;
                border-radius: 20px;
            }

            .reels-frame {
                padding: 9px;
                border-width: 3px;
            }

            .reels {
                gap: 5px;
                padding: 8px;
            }

            .reel-window {
                border-width: 3px;
                border-radius: 7px;
            }

            .go-button {
                width: 180px;
                height: 65px;
                font-size: 27px;
            }

            .subtitle {
                letter-spacing: 3px;
            }
        }
    </style>
</head>

<body>

    <div class="game-wrapper">

        <main class="machine">

            <div class="sparkles">
                <span class="sparkle">✦</span>
                <span class="sparkle">✧</span>
                <span class="sparkle">✦</span>
                <span class="sparkle">✧</span>
                <span class="sparkle">✦</span>
            </div>

            <section class="title-area">
                <h1 class="title">FOUR BEASTS</h1>
                <div class="subtitle">龍 · 虎 · 玄武 · 鳳凰</div>
            </section>

            <div class="gold-line">
                <span>✦</span>
            </div>

            <!-- 슬롯 -->
            <section class="reels-frame">

                <div class="reels">

                    <div class="reel-window">
                        <div class="center-line"></div>
                        <div class="reel" id="reel0"></div>
                    </div>

                    <div class="reel-window">
                        <div class="center-line"></div>
                        <div class="reel" id="reel1"></div>
                    </div>

                    <div class="reel-window">
                        <div class="center-line"></div>
                        <div class="reel" id="reel2"></div>
                    </div>

                    <div class="reel-window">
                        <div class="center-line"></div>
                        <div class="reel" id="reel3"></div>
                    </div>

                </div>

            </section>

            <!-- 결과 -->
            <div class="result" id="result">
                운명을 시험해보세요
            </div>

            <!-- GO -->
            <div class="button-area">
                <button class="go-button" id="goButton">
                    GO
                </button>
            </div>

        </main>

    </div>

    <div class="jackpot-effect" id="jackpotEffect"></div>

    <script>

        /*
         * ==========================================
         * FOUR BEASTS SLOT MACHINE
         * ==========================================
         */

        const symbols = [
            "🐉",
            "🐯",
            "🐢",
            "🔥"
        ];

        /*
         * 릴 확률
         *
         * 같은 심볼을 여러 번 넣어서
         * 실제 슬롯머신처럼 출현 빈도를 조절한다.
         *
         * 🐉 = 40%
         * 🐯 = 30%
         * 🐢 = 20%
         * 🔥 = 10%
         */
        const reelSymbols = [
            "🐉", "🐉", "🐉", "🐉",
            "🐉", "🐉", "🐉", "🐉",

            "🐯", "🐯", "🐯", "🐯",
            "🐯", "🐯",

            "🐢", "🐢", "🐢", "🐢",

            "🔥", "🔥"
        ];

        const reels = [
            document.getElementById("reel0"),
            document.getElementById("reel1"),
            document.getElementById("reel2"),
            document.getElementById("reel3")
        ];

        const goButton = document.getElementById("goButton");
        const result = document.getElementById("result");
        const jackpotEffect = document.getElementById("jackpotEffect");

        let spinning = false;

        /*
         * 현재 결과
         */
        let currentResults = [
            "🐉",
            "🐯",
            "🐢",
            "🔥"
        ];

        /*
         * 랜덤 심볼 선택
         */
        function getRandomSymbol() {
            const index = Math.floor(
                Math.random() * reelSymbols.length
            );

            return reelSymbols[index];
        }

        /*
         * 릴 하나 생성
         *
         * 실제 슬롯처럼 위아래로 긴 릴을 만든다.
         */
        function createReel(reelElement, finalSymbol = null) {

            reelElement.innerHTML = "";

            /*
             * 충분히 많은 심볼을 만들어서
             * 빠르게 지나가는 느낌을 만든다.
             */
            const items = [];

            for (let i = 0; i < 35; i++) {
                items.push(getRandomSymbol());
            }

            /*
             * 마지막에는 원하는 결과를 넣는다.
             */
            if (finalSymbol) {
                items.push(finalSymbol);
            }

            items.forEach(symbol => {

                const div = document.createElement("div");

                div.className = "symbol";
                div.textContent = symbol;

                reelElement.appendChild(div);

            });

            return items.length - 1;
        }

        /*
         * 초기 슬롯 표시
         */
        function initialize() {

            reels.forEach((reel, index) => {

                createReel(
                    reel,
                    currentResults[index]
                );

                reel.style.transition = "none";
                reel.style.transform = "translateY(0)";

            });

        }

        /*
         * 릴 하나 돌리기
         */
        function spinReel(
            reel,
            finalSymbol,
            duration
        ) {

            return new Promise(resolve => {

                /*
                 * 릴 재생성
                 */
                const finalIndex = createReel(
                    reel,
                    finalSymbol
                );

                const symbolHeight =
                    reel.querySelector(".symbol").offsetHeight;

                /*
                 * 마지막 심볼이
                 * 중앙에 오도록 이동
                 */
                const targetY =
                    -(finalIndex * symbolHeight);

                /*
                 * 시작 위치
                 */
                reel.style.transition = "none";
                reel.style.transform = "translateY(0)";

                /*
                 * 브라우저가 위치를 적용하도록
                 * 강제로 레이아웃 계산
                 */
                reel.offsetHeight;

                reel.classList.add("spinning");

                /*
                 * 슬롯이 빠르게 회전하는 느낌
                 */
                reel.style.transition = `
                    transform ${duration}ms cubic-bezier(
                        0.12,
                        0.75,
                        0.18,
                        1
                    )
                `;

                reel.style.transform =
                    `translateY(${targetY}px)`;

                setTimeout(() => {

                    reel.classList.remove("spinning");

                    reel.classList.add("stopping");

                    setTimeout(() => {
                        reel.classList.remove("stopping");
                    }, 250);

                    resolve();

                }, duration);

            });

        }

        /*
         * GO
         */
        async function spin() {

            if (spinning) {
                return;
            }

            spinning = true;

            goButton.disabled = true;

            result.classList.remove("jackpot");
            result.textContent = "GOOD LUCK...";

            /*
             * 최종 결과를 먼저 결정한다.
             *
             * 애니메이션은 그 결과까지 이동하는 과정이다.
             */
            const finalResults = [
                getRandomSymbol(),
                getRandomSymbol(),
                getRandomSymbol(),
                getRandomSymbol()
            ];

            /*
             * 현재 결과 저장
             */
            currentResults = finalResults;

            /*
             * 4개의 슬롯을 순서대로 정지
             */

            // 1번 슬롯
            await spinReel(
                reels[0],
                finalResults[0],
                1800
            );

            // 잠깐 간격
            await wait(350);

            // 2번 슬롯
            await spinReel(
                reels[1],
                finalResults[1],
                1800
            );

            await wait(350);

            // 3번 슬롯
            await spinReel(
                reels[2],
                finalResults[2],
                1800
            );

            await wait(350);

            // 4번 슬롯
            await spinReel(
                reels[3],
                finalResults[3],
                1800
            );

            /*
             * 결과 판정
             */
            checkResult(finalResults);

            spinning = false;

            goButton.disabled = false;
        }

        /*
         * 결과 판정
         */
        function checkResult(results) {

            const allSame =
                results.every(
                    symbol => symbol === results[0]
                );

            if (allSame) {

                /*
                 * JACKPOT
                 */
                result.textContent =
                    `🎉 JACKPOT! ${results[0]} ${results[0]} ${results[0]} ${results[0]} 🎉`;

                result.classList.add("jackpot");

                triggerJackpot();

            } else {

                /*
                 * 꽝
                 */
                result.textContent =
                    `${results.join("   ")}  —  다시 도전!`;

            }

        }

        /*
         * 잭팟 연출
         */
        function triggerJackpot() {

            jackpotEffect.classList.remove("active");

            /*
             * 애니메이션 재실행
             */
            void jackpotEffect.offsetWidth;

            jackpotEffect.classList.add("active");

            /*
             * 슬롯 전체 흔들기
             */
            const machine =
                document.querySelector(".machine");

            machine.animate(
                [
                    {
                        transform: "scale(1)"
                    },
                    {
                        transform: "scale(1.015) rotate(-0.5deg)"
                    },
                    {
                        transform: "scale(1.02) rotate(0.5deg)"
                    },
                    {
                        transform: "scale(1.015) rotate(-0.3deg)"
                    },
                    {
                        transform: "scale(1)"
                    }
                ],
                {
                    duration: 700,
                    easing: "ease-out"
                }
            );

        }

        /*
         * 시간 대기
         */
        function wait(ms) {

            return new Promise(
                resolve => setTimeout(resolve, ms)
            );

        }

        /*
         * 버튼 이벤트
         */
        goButton.addEventListener(
            "click",
            spin
        );

        /*
         * 최초 화면
         */
        initialize();

    </script>

</body>
</html>
