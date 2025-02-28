# xxx-c
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sitio con Anuncios</title>
    <style>
        /* Tus estilos CSS aquí (sin cambios) */
    </style>
</head>
<body>
    <!-- Pop-up de anuncio -->
    <div class="popup-overlay" id="popupOverlay">
        <div class="popup">
            <button class="close-btn left" id="closeLeft">X</button>
            <button class="close-btn right" id="closeRight">X</button>
            <div class="ad-block">¡Anuncio! Cierra esta ventana para continuar.</div>
        </div>
    </div>

    <!-- Bloques de anuncio -->
    <div class="ad-block" id="adBlock1"></div>
    <div class="ad-block" id="adBlock2"></div>

    <!-- Temporizador -->
    <div class="timer" id="timer">10</div>

    <!-- Botón para saltar fase -->
    <button class="skip-btn" onclick="nextPhase()" id="skipBtn" disabled>Saltar Fase</button>

    <!-- Bloques de anuncio -->
    <div class="ad-block" id="adBlock3"></div>
    <div class="ad-block" id="adBlock4"></div>

    <script>
        let currentPhase = 1;
        const totalPhases = 4;
        let timeLeft = 10; // Contador visible (25 segundos reales)
        const timerInterval = 2500; // 2500 ms = 2.5 segundos
        let timerId = null;

        const adBlocks = document.querySelectorAll('.ad-block');
        const timerElement = document.getElementById('timer');
        const skipButton = document.getElementById('skipBtn');
        const popupOverlay = document.getElementById('popupOverlay');
        const closeLeft = document.getElementById('closeLeft');
        const closeRight = document.getElementById('closeRight');

        // Mostrar pop-up al inicio de cada fase
        function showPopup() {
            popupOverlay.style.display = 'flex';
            setRandomCloseButton();
        }

        // Configurar "X" correcta
        function setRandomCloseButton() {
            const correctX = Math.random() < 0.5 ? closeLeft : closeRight;
            correctX.onclick = () => {
                closePopup();
                startTimer();
            };
            const wrongX = correctX === closeLeft ? closeRight : closeLeft;
            wrongX.onclick = () => alert('¡Equivocado! Usa la otra "X".');
        }

        // Cerrar pop-up
        function closePopup() {
            popupOverlay.style.display = 'none';
        }

        // Iniciar temporizador
        function startTimer() {
            timeLeft = 10;
            timerElement.textContent = timeLeft;
            skipButton.disabled = true;
            skipButton.classList.remove('active');

            if (timerId) clearInterval(timerId);

            timerId = setInterval(() => {
                timeLeft--;
                timerElement.textContent = timeLeft;

                if (timeLeft <= 0) {
                    clearInterval(timerId);
                    skipButton.disabled = false;
                    skipButton.classList.add('active');
                }
            }, timerInterval);
        }

        // Cambiar de fase
        function nextPhase() {
            if (currentPhase < totalPhases) {
                currentPhase++;
                adBlocks.forEach((block, index) => {
                    block.textContent = `Anuncio ${currentPhase}-${index + 1}`;
                });
                showPopup();
            } else {
                window.location.href = 'https://mega.nz/TU_ENLACE_AQUI';
            }
        }

        // Iniciar primera fase
        showPopup();
    </script>
</body>
</html>
