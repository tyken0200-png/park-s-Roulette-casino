<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Four Beasts Slot</title>

    <style>
        * {
            box-sizing: border-box;
        }

        body {
            margin: 0;
            min-height: 100vh;

            display: flex;
            justify-content: center;
            align-items: center;

            background: #250000;

            font-family: Arial, sans-serif;
        }

        .machine {
            width: 90%;
            max-width: 900px;

            padding: 40px;

            text-align: center;

            background: #8b1111;

            border: 8px solid #e8bd3b;
            border-radius: 25px;

            box-shadow:
                0 0 30px #000,
                inset 0 0 30px rgba(0, 0, 0, .5);
        }

        h1 {
            margin: 0 0 30px;

            color: #ffe98a;

            font-size: 55px;

            text-shadow:
                0 0 10px #ffd700,
                0 0 25px #ff7300;
        }

        .slots {
            display: grid;

            grid-template-columns:
                repeat(4, 1fr);

            gap: 10px;

            padding: 15px;

            background: #160000;

            border: 5px solid #d6a92d;
            border-radius: 15px;
        }

        .slot {
            height: 200px;

            display: flex;
            justify-content: center;
            align-items: center;

            background: white;

            border: 5px solid #d7a72b;
            border-radius: 10px;

            font-size: 100px;
        }

        button {
            margin-top: 30px;

            width: 220px;
            height: 70px;

            border: 4px solid #ffe47a;
            border-radius: 15px;

            background: linear-gradient(
                #ffe86b,
                #e59e13
            );

            color: #650000;

            font-size: 30px;
            font-weight: bold;

            cursor: pointer;
        }

        button:hover {
            filter: brightness(1.15);
        }

        button:active {
            transform: translateY(4px);
        }

        #result {
            margin-top: 20px;

            min-height: 35px;

            color: #ffe98a;

            font-size: 24px;
            font-weight: bold;
        }

        @media (max-width: 600px) {

            .machine {
                padding: 20px;
            }

            h1 {
                font-size: 35px;
            }

            .slots {
                gap: 5px;
                padding: 7px;
            }

            .slot {
                height: 120px;
                font-size: 55px;
                border-width: 3px;
            }
        }
    </style>
</head>

<body>

    <div class="machine">

        <h1>FOUR BEASTS</h1>

        <div class="slots">

            <div class="slot" id="slot1">🐉</div>
            <div class="slot" id="slot2">🐯</div>
            <div class="slot" id="slot3">🐢</div>
            <div class="slot" id="slot4">🔥</div>

        </div>

        <div id="result">
            운명을 시험해보세요
        </div>

        <button id="go">
            GO
        </button>

    </div>

    <script>

        const symbols = [
            "🐉",
            "🐯",
            "🐢",
            "🔥"
        ];

        const slots = [
            document.getElementById("slot1"),
            document.getElementById("slot2"),
            document.getElementById("slot3"),
            document.getElementById("slot4")
        ];

        const button =
            document.getElementById("go");

        const result =
            document.getElementById("result");

        button.addEventListener(
            "click",
            function () {

                slots.forEach(function(slot) {

                    const random =
                        Math.floor(
                            Math.random() *
                            symbols.length
                        );

                    slot.textContent =
                        symbols[random];

                });

                const values =
                    slots.map(function(slot) {
                        return slot.textContent;
                    });

                const jackpot =
                    values.every(function(value) {
                        return value === values[0];
                    });

                if (jackpot) {

                    result.textContent =
                        "🎉 JACKPOT! 🎉";

                } else {

                    result.textContent =
                        "다시 도전!";

                }

            }
        );

    </script>

</body>
</html>
