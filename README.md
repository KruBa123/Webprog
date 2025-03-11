<!DOCTYPE html>
<html lang="hu">
<head>
    <meta charset="UTF-8">
    <title>Oldalbeállítások</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        body {
            transition: background-color 0.3s, color 0.3s;
            font-size: 16px;
            --bg-color: #ffffff;
            --text-color: #000000;
            background-color: var(--bg-color);
            color: var(--text-color);
        }
        
        .dark-theme {
            --bg-color: #2c2c2c;
            --text-color: #ffffff;
        }

        .container {
            padding: 20px;
            max-width: 800px;
            margin: 0 auto;
        }

        button {
            padding: 10px;
            margin: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Beállítások</h1>
        <button id="themeToggle">Téma váltás</button>
        <button id="fontIncrease">Betűméret növelés</button>
        <button id="resetSettings">Alaphelyzet</button>
        
        <h2>Bemutató tartalom</h2>
        <p>Ez egy példaszöveg, amely bemutatja az oldal kinézetét és a beállítások hatását.</p>
    </div>

    <script>
        $(document).ready(function() {
            const savedTheme = localStorage.getItem('theme');
            const savedFontSize = localStorage.getItem('fontSize');

            if(savedTheme) $('body').addClass(savedTheme);
            if(savedFontSize) $('body').css('font-size', savedFontSize);

            $('#themeToggle').click(function() {
                $('body').toggleClass('dark-theme');
                localStorage.setItem('theme', $('body').hasClass('dark-theme') ? 'dark-theme' : '');
            });

            $('#fontIncrease').click(function() {
                const currentSize = parseFloat($('body').css('font-size'));
                const newSize = currentSize * 1.2;
                if(newSize <= 32) {
                    $('body').css('font-size', newSize + 'px');
                    localStorage.setItem('fontSize', newSize + 'px');
                }
            });

            $('#resetSettings').click(function() {
                localStorage.removeItem('theme');
                localStorage.removeItem('fontSize');
                $('body').removeClass('dark-theme').css('font-size', '16px');
            });
        });
    </script>
</body>
</html>