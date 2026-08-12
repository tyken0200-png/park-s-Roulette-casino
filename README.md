<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- GitHub Pages 기본 페이지 -->
    <title>FOUR BEASTS SLOT</title>

    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;

            font-family:
                Arial,
                "Noto Sans KR",
                sans-serif;

            background:
                radial-gradient(
                    circle at center,
                    #a51d1d 0%,
                    #5d0808 45%,
                    #1b0202 100%
                );

            overflow-x: hidden;
        }

        /* 배경 금빛 입자 */
        body::before {
            content: "";
            position: fixed;
            inset: 0;
            pointer-events: none;

            background-image:
                radial-gradient(
                    circle,
                    rgba(255, 220, 80, 0.8) 1px,
                    transparent 2px
                );

            background-size: 70px 70px;
            opacity: 0.18;
        }

        /* =========================
           슬롯머신 본체
        ========================= */

        .machine {
            position: relative;

            width: min(1000px, 95vw);

            padding: 35px;

            border: 8px solid #f1c83b;
            border-radius: 30px;

            background:
                linear-gradient(
                    135deg,
                    #650808,
                    #c51d1d,
                    #750808,
                    #b91616,
                    #580505
                );

            box-shadow:
                0 0 0 4px #5c1700,
                0 0 0 8px #f8d75b,
                0 25px 70px rgba(0, 0, 0, 0.8),
                inset 0 0 40px rgba(0, 0, 0, 0.6);
        }

        .machine::before {
            content: "";

            position: absolute;
            inset: 12px;

            border: 2px solid rgba(255, 225, 100, 0.6);
            border-radius: 20px;

            pointer-events: none;
        }

        /* =========================
           제목
        ========================= */

        .title {
            text-align: center;

            margin-bottom: 8px;

            font-size: clamp(35px, 6vw, 70px);
            font-weight: 900;

            letter-spacing: 7px;

            color: #fff0a0;

            text-shadow:
                0 3px 0 #8b4200,
                0 6px 0 #5c2100,
                0 0 10px #ffd700,
                0 0 25px #ff9d00,
                0 0 40px #ff5e00;
        }

        .subtitle {
            text-align: center;

            margin-bottom: 25px;

            color: #ffd85a;

            font-size: 14px;
            letter-spacing: 7px;

            text-shadow:
                0 0 10px #ff9d00;
        }

        /* 장식 */
        .decoration {
            display: flex;
            align-items: center;
            gap: 15px;

            margin-bottom: 25px;
        }

        .decoration::before,
        .decoration::after {
            content: "";

            height: 3px;
            flex: 1;

            background:
                linear-gradient(
                    90deg,
                    transparent,
                    #ffd700,
                    #fff2a0,
                    #ffd700,
                    transparent
                );

            box-shadow:
                0 0 10px #ffd700;
        }

        .decoration span {
            color: #fff0a0;
            font-size: 24px;
        }

        /* =========================
           슬롯 외부 프레임
        ========================= */

        .slot-frame {
            padding: 15px;

            border: 5px solid #ffe37b;
            border-radius: 18px;

            background:
                linear-gradient(
                    135deg,
                    #6a3300,
                    #f5c62f,
                    #7d3b00,
                    #ffdc4c,
                    #652c00
                );

            box-shadow:
                inset 0 0 20px rgba(0, 0, 0, 0.8),
                0 0 30px rgba(255, 200, 0, 0.5);
        }

        /* =========================
           슬롯 4개
        ========================= */

        .slots {
            display: grid;

            grid-template-columns:
                repeat(4, 1fr);

            gap: 12px;

            padding: 15px;

            background:
                linear-gradient(
                    180deg,
                    #230000,
                    #080000,
                    #230000
                );

            border: 4px solid #8d5805;
            border-radius: 12px;

            box-shadow:
                inset 0 0 30px rgba(0, 0, 0, 0.95);
        }

        /* =========================
           슬롯 창
        ========================= */

        .slot {
            position: relative;

            height: clamp(150px, 20vw, 230px);

            overflow: hidden;

            background:
                linear-gradient(
                    180deg,
                    #ffffff,
                    #eeeeee 50%,
                    #d2d2d2
                );

            border: 5px solid #e5b62c;
            border-radius: 10px;

            box-shadow:
                inset 0 0 25px rgba(0, 0, 0, 0.55),
                0 0 15px rgba(255, 210, 0, 0.4);
        }

        /* 위/아래 그림자 */
        .slot::before,
        .slot::after {
            content: "";

            position: absolute;
            left: 0;
            right: 0;

            height: 28%;

            z-index: 10;

            pointer-events: none;
        }

        .slot::before {
            top: 0;

            background:
                linear-gradient(
                    180deg,
                    rgba(0, 0, 0, 0.45),
                    transparent
                );
        }

        .slot::after {
            bottom: 0;

            background:
                linear-gradient(
                    0deg,
                    rgba(0, 0, 0, 0.45),
                    transparent
                );
        }

        /* 중앙 당첨선 */
        .payline {
            position: absolute;

            left: 0;
            right: 0;

            top: 50%;

            height: 4px;

            transform: translateY(-50%);

            z-index: 20;

            background: rgba(255, 194, 0, 0.8);

            box-shadow:
                0 0 8px #ffbf00,
                0 0 20px #ff8500;

            pointer-events: none;
        }

        /* =========================
           실제 릴
        ========================= */

        .reel {
            position: absolute;

            width: 100%;
            left: 0;
            top: 0;

            display: flex;
            flex-direction: column;
            align-items: center;

            will-change: transform;
        }

        .symbol {
            width: 100%;

            height: clamp(150px, 20vw, 230px);

            flex-shrink: 0;

            display: flex;
            align-items: center;
            justify-content: center;

            font-size: clamp(70px, 10vw, 125px);

            user-select: none;

            filter:
                drop-shadow(
                    0 5px 3px rgba(0, 0, 0, 0.35)
                );
        }

        /* 회전 중 */
        .reel.spinning .symbol {
            filter:
                blur(2px)
                drop-shadow(
                    0 0 12px rgba(255, 180, 0, 0.7)
                );
        }

        /* 정지 순간 */
        .reel.stop-effect {
            animation: stopShake 0.25s ease-out;
        }

        @keyframes stopShake {
            0% {
                transform: translateY(0);
            }

            30% {
                transform: translateY(5px);
            }

            60% {
                transform: translateY(-3px);
            }

            100% {
                transform: translateY(0);
            }
        }

        /* =========================
           GO 버튼
        ========================= */

        .button-container {
            display: flex;
            justify-content: center;

            margin-top: 30px;
        }

        #goButton {
            position: relative;

            width: 230px;
            height: 80px;

            border: 5px solid #ffe47b;
            border-radius: 18px;

            background:
                linear-gradient(
                    180deg,
                    #fff083,
                    #f0b51d 40%,
                    #a95700
                );

            color: #680b00;

            font-size: 34px;
            font-weight: 1000;

            letter-spacing: 6px;

            cursor: pointer;

            box-shadow:
                0 8px 0 #681f00,
                0 12px 30px rgba(0, 0, 0, 0.6),
                0 0 30px rgba(255, 210, 50, 0.7),
                inset 0 4px 7px rgba(255, 255, 255, 0.8);

            transition:
                transform 0.08s,
                filter 0.15s;
        }

        #goButton:hover {
            filter: brightness(1.15);

            box-shadow:
                0 8px 0 #681f00,
                0 12px 30px rgba(0, 0, 0, 0.6),
                0 0 45px rgba(255, 220, 70, 1);
        }

        #goButton:active {
            transform: translateY(7px);

            box-shadow:
                0 1px 0 #681f00,
                0 5px 15px rgba(0, 0, 0, 0.5);
        }

        #goButton:disabled {
            cursor: not-allowed;
            filter: brightness(0.65);
        }

        /* =========================
           결과
        ========================= */

        #result {
            min-height: 55px;

            margin-top: 22px;

            display: flex;
            align-items: center;
            justify-content: center;

            text-align: center;

            color: #ffe66b;

            font-size: 24px;
            font-weight: 900;

            letter-spacing: 3px;

            text-shadow:
                0 0 10px #ffb000,
                0 0 20px #ff7000;
        }

        /* =========================
           JACKPOT
        ========================= */

        #result.jackpot {
            font-size: clamp(30px, 5vw, 55px);

            color: #fff8b0;

            animation:
                jackpotGlow 0.6s infinite alternate,
                jackpotShake 0.4s infinite;
        }

        @keyframes jackpotGlow {
            from {
                text-shadow:
                    0 0 10px #ffd700,
                    0 0 20px #ff8c00;
            }

            to {
                text-shadow:
                    0 0 15px #ffffff,
                    0 0 30px #ffd700,
                    0 0 50px #ff6500;
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

        /* =========================
           잭팟 화면 효과
        ========================= */

        .jackpot-overlay {
            position: fixed;

            inset: 0;

            pointer-events: none;

            opacity: 0;

            z-index: 100;

            background:
                radial-gradient(
                    circle,
                    rgba(255, 230, 80, 0.35),
                    transparent 60%
                );
        }

        .jackpot-overlay.active {
            animation: jackpotFlash 1.5s ease-out;
        }

        @keyframes jackpotFlash {
            0% {
                opacity: 0;
            }

            20% {
                opacity: 1;
            }

            40% {
                opacity: 0.5;
            }

            100% {
                opacity: 0;
            }
        }

        /* =========================
           반응형
        ========================= */

        @media (max-width: 650px) {

            .machine {
                padding: 22px 12px 30px;

                border-width: 5px;
                border-radius: 20px;
            }

            .slots {
                gap: 5px;
                padding: 7px;
            }

            .slot {
                border-width: 3px;
            }

            .slot-frame {
                padding: 8px;
                border-width: 3px;
            }

            #goButton {
                width: 180px;
                height: 65px;

                font-size: 28px;
            }

            .subtitle {
                letter-spacing: 3px;
            }
        }
    </style>
</head>

<body>

    <!-- =========================
         슬롯머신
    ========================= -->

    <main class="machine">

        <h1 class="title">
            FOUR BEASTS
        </h1>

        <div class="subtitle">
            龍 · 虎 · 玄武 · 鳳凰
        </div>

        <div class="decoration">
            <span>✦</span>
        </div>

        <!-- 슬롯 -->
        <section class="slot-frame">

            <div class="slots">

                <div class="slot">
                    <div class="payline"></div>
                    <div class="reel" id="reel0"></div>
                </div>

                <div class="slot">
                    <div class="payline"></div>
                    <div class="reel" id="reel1"></div>
                </div>

                <div class="slot">
                    <div class="payline"></div>
                    <div class="reel" id="reel2"></div>
                </div>

                <div class="slot">
                    <div class="payline"></div>
                    <div class="reel" id="reel3"></div>
                </div>

            </div>

        </section>

        <!-- 결과 -->
        <div id="result">
            운명을 시험해보세요
        </div>

        <!-- GO -->
        <div class="button-container">
            <button id="goButton">
                GO
            </button>
        </div>

    </main>

    <!-- 잭팟 효과 -->
    <div
        class="jackpot-overlay"
        id="jackpotOverlay">
    </div>


    <script>

        /* =====================================================
           FOUR BEASTS SLOT MACHINE
           ===================================================== */


        /*
         * 슬롯 심볼
         */
        const symbols = [
            "🐉",
            "🐯",
            "🐢",
            "🔥"
        ];


        /*
         * 실제 슬롯 릴의 구성
         *
         * 용     40%
         * 호랑이 30%
         * 거북이 20%
         * 피닉스 10%
         *
         * 같은 그림을 여러 개 넣어
         * 출현 확률을 조절한다.
         */
        const reelTable = [

            "🐉", "🐉", "🐉", "🐉",
            "🐉", "🐉", "🐉", "🐉",

            "🐯", "🐯", "🐯", "🐯",
            "🐯", "🐯",

            "🐢", "🐢", "🐢", "🐢",

            "🔥", "🔥"

        ];


        /*
         * DOM
         */
        const reels = [

            document.getElementById("reel0"),
            document.getElementById("reel1"),
            document.getElementById("reel2"),
            document.getElementById("reel3")

        ];


        const goButton =
            document.getElementById("goButton");


        const result =
            document.getElementById("result");


        const jackpotOverlay =
            document.getElementById("jackpotOverlay");


        /*
         * 게임 상태
         */
        let isSpinning = false;


        /*
         * 랜덤 심볼
         */
        function randomSymbol() {

            const index =
                Math.floor(
                    Math.random() *
                    reelTable.length
                );

            return reelTable[index];
        }


        /*
         * 릴 만들기
         */
        function buildReel(
            reel,
            finalSymbol
        ) {

            reel.innerHTML = "";


            /*
             * 많은 심볼을 넣어서
             * 빠르게 지나가는 느낌을 만든다.
             */
            const list = [];


            for (let i = 0; i < 40; i++) {

                list.push(
                    randomSymbol()
                );

            }


            /*
             * 마지막에는
             * 실제 결과 심볼을 넣는다.
             */
            list.push(
                finalSymbol
            );


            list.forEach(symbol => {

                const element =
                    document.createElement("div");

                element.className =
                    "symbol";

                element.textContent =
                    symbol;

                reel.appendChild(
                    element
                );

            });


            return list.length - 1;
        }


        /*
         * 릴 초기화
         */
        function initializeReels() {

            const initialSymbols = [
                "🐉",
                "🐯",
                "🐢",
                "🔥"
            ];


            reels.forEach(
                (reel, index) => {

                    buildReel(
                        reel,
                        initialSymbols[index]
                    );

                    reel.style.transition =
                        "none";

                    reel.style.transform =
                        "translateY(0)";

                }
            );

        }


        /*
         * 릴 하나 회전
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
                const finalIndex =
                    buildReel(
                        reel,
                        finalSymbol
                    );


                /*
                 * 실제 심볼 높이
                 */
                const symbol =
                    reel.querySelector(
                        ".symbol"
                    );


                const symbolHeight =
                    symbol.offsetHeight;


                /*
                 * 마지막 심볼까지 이동
                 */
                const targetY =
                    -(
                        finalIndex *
                        symbolHeight
                    );


                /*
                 * 처음 위치
                 */
                reel.style.transition =
                    "none";

                reel.style.transform =
                    "translateY(0)";


                /*
                 * 브라우저에게
                 * 위치 변경을 반영시키기
                 */
                reel.offsetHeight;


                /*
                 * 회전 상태
                 */
                reel.classList.add(
                    "spinning"
                );


                /*
                 * 감속하면서 정지
                 */
                reel.style.transition = `
                    transform ${duration}ms
                    cubic-bezier(
                        0.08,
                        0.78,
                        0.15,
                        1
                    )
                `;


                reel.style.transform =
                    `translateY(${targetY}px)`;


                /*
                 * 정지
                 */
                setTimeout(() => {

                    reel.classList.remove(
                        "spinning"
                    );


                    reel.classList.add(
                        "stop-effect"
                    );


                    setTimeout(() => {

                        reel.classList.remove(
                            "stop-effect"
                        );

                    }, 250);


                    resolve();

                }, duration);

            });

        }


        /*
         * 잠시 기다리기
         */
        function wait(ms) {

            return new Promise(
                resolve =>
                    setTimeout(
                        resolve,
                        ms
                    )
            );

        }


        /*
         * 게임 시작
         */
        async function spin() {

            /*
             * 이미 돌아가는 중이면
             * 아무것도 하지 않는다.
             */
            if (isSpinning) {
                return;
            }


            isSpinning = true;

            goButton.disabled = true;


            /*
             * 결과 초기화
             */
            result.classList.remove(
                "jackpot"
            );

            result.textContent =
                "GOOD LUCK...";


            /*
             * 최종 결과를 결정
             */
            const finalResults = [

                randomSymbol(),
                randomSymbol(),
                randomSymbol(),
                randomSymbol()

            ];


            /*
             * ==========================
             * 1번 슬롯
             * ==========================
             */

            await spinReel(
                reels[0],
                finalResults[0],
                1800
            );


            await wait(350);


            /*
             * ==========================
             * 2번 슬롯
             * ==========================
             */

            await spinReel(
                reels[1],
                finalResults[1],
                1800
            );


            await wait(350);


            /*
             * ==========================
             * 3번 슬롯
             * ==========================
             */

            await spinReel(
                reels[2],
                finalResults[2],
                1800
            );


            await wait(350);


            /*
             * ==========================
             * 4번 슬롯
             * ==========================
             */

            await spinReel(
                reels[3],
                finalResults[3],
                1800
            );


            /*
             * 결과 판정
             */
            checkResult(
                finalResults
            );


            isSpinning = false;

            goButton.disabled = false;

        }


        /*
         * 결과 확인
         */
        function checkResult(
            results
        ) {

            /*
             * 네 개 모두 같은지
             */
            const jackpot =
                results.every(
                    symbol =>
                        symbol === results[0]
                );


            if (jackpot) {

                /*
                 * JACKPOT
                 */
                result.textContent =
                    `🎉 JACKPOT! ${results.join(" ")} 🎉`;


                result.classList.add(
                    "jackpot"
                );


                playJackpotEffect();

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
        function playJackpotEffect() {

            /*
             * 화면 빛 효과
             */
            jackpotOverlay.classList.remove(
                "active"
            );


            void jackpotOverlay.offsetWidth;


            jackpotOverlay.classList.add(
                "active"
            );


            /*
             * 슬롯머신 본체 흔들림
             */
            const machine =
                document.querySelector(
                    ".machine"
                );


            machine.animate(

                [
                    {
                        transform:
                            "scale(1) rotate(0)"
                    },

                    {
                        transform:
                            "scale(1.02) rotate(-0.6deg)"
                    },

                    {
                        transform:
                            "scale(1.03) rotate(0.6deg)"
                    },

                    {
                        transform:
                            "scale(1.02) rotate(-0.3deg)"
                    },

                    {
                        transform:
                            "scale(1) rotate(0)"
                    }
                ],

                {
                    duration: 800,
                    easing: "ease-out"
                }

            );

        }


        /*
         * 버튼
         */
        goButton.addEventListener(
            "click",
            spin
        );


        /*
         * 페이지 처음 열었을 때
         */
        initializeReels();

    </script>

</body>
</html>
