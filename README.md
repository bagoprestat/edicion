<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Progreso de Edición</title>
    <style>
        :root {
            --primary-color: #a1007d;
            --text-main: #333333;
            --text-muted: #777777;
            --bg-color: #ffffff;
            --box-bg: #fdfdfd;
        }

        body {
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            text-align: center;
        }

        .container {
            width: 90%;
            max-width: 600px;
            padding: 40px 20px;
        }

        h1 {
            text-transform: uppercase;
            letter-spacing: 3px;
            font-weight: 300;
            font-size: 24px;
            margin-bottom: 50px;
            color: var(--text-main);
        }

        .status-label {
            font-size: 12px;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: var(--text-muted);
            margin-bottom: 10px;
        }

        .status-box {
            border: 1px solid var(--primary-color);
            background-color: var(--box-bg);
            padding: 25px 20px;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(161, 0, 125, 0.05);
            margin-bottom: 25px;
            transition: all 0.3s ease;
        }

        .current-stage {
            font-size: 20px;
            font-weight: 500;
            color: var(--primary-color);
            margin: 0;
        }

        .next-stage-container {
            margin-bottom: 50px;
        }

        .next-stage-label {
            font-size: 12px;
            color: var(--text-muted);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .next-stage {
            font-size: 15px;
            color: var(--text-main);
            margin-top: 5px;
        }

        .progress-wrapper {
            margin-top: 20px;
        }

        .progress-bar-container {
            width: 100%;
            height: 6px;
            background-color: #f0f0f0;
            border-radius: 10px;
            overflow: hidden;
            margin-bottom: 15px;
        }

        .progress-fill {
            height: 100%;
            background-color: var(--primary-color);
            width: 0%;
            transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .percentage {
            font-size: 18px;
            font-weight: 600;
            color: var(--primary-color);
        }

        /* Controles para el editor (puedes ocultarlos cuando envíes captura o pantalla al cliente) */
        .controls {
            margin-top: 60px;
            padding-top: 20px;
            border-top: 1px dashed #eee;
            width: 100%;
        }

        select {
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-family: inherit;
            width: 100%;
            max-width: 400px;
            color: var(--text-main);
            cursor: pointer;
            outline: none;
        }

        select:focus {
            border-color: var(--primary-color);
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>EDICIÓN REALITY</h1>

        <div class="status-label">Estado Actual del Proyecto</div>
        <div class="status-box">
            <p class="current-stage" id="currentStageText">Cargando...</p>
        </div>

        <div class="next-stage-container">
            <div class="next-stage-label">Siguiente en la lista:</div>
            <div class="next-stage" id="nextStageText">Cargando...</div>
        </div>

        <div class="progress-wrapper">
            <div class="progress-bar-container">
                <div class="progress-fill" id="progressFill"></div>
            </div>
            <div class="percentage" id="percentageText">0% completado</div>
        </div>

        <div class="controls">
            <p style="font-size: 12px; color: #999;">Control de editor (Selecciona para actualizar):</p>
            <select id="stageSelector" onchange="updateProgress(this.value)"></select>
        </div>
    </div>

    <script>
        const stages = [
            "Transferencia y respaldo de datos",
            "Organización de material",
            "Visionado de material",
            "Corte de clips y selección de momentos",
            "Sincronización de audio boom y filmadora",
            "Calado de los clips en pantalla verde (croma, color y rotoscopía)",
            "Descarga de recursos como títulos, transiciones y elementos gráficos",
            "Armado de primera base",
            "Elaboración de voz en off (guion y voz)",
            "Selección musical",
            "Reajuste de primera base (primer corte)",
            "Ajuste en base a feedback",
            "Reajuste de segunda base (segundo corte)",
            "Colorización",
            "Postproducción de sonido y limpieza de audio",
            "Ajuste de base final (corte final)",
            "Exporte final"
        ];

        const selector = document.getElementById('stageSelector');
        const currentStageText = document.getElementById('currentStageText');
        const nextStageText = document.getElementById('nextStageText');
        const progressFill = document.getElementById('progressFill');
        const percentageText = document.getElementById('percentageText');

        // Llenar el selector con las etapas
        stages.forEach((stage, index) => {
            let option = document.createElement('option');
            option.value = index;
            option.textContent = `${index + 1}. ${stage}`;
            selector.appendChild(option);
        });

        function updateProgress(index) {
            index = parseInt(index);
            const totalStages = stages.length;
            
            // Actualizar estado actual
            currentStageText.textContent = stages[index];

            // Actualizar siguiente estado
            if (index < totalStages - 1) {
                nextStageText.textContent = stages[index + 1];
            } else {
                nextStageText.textContent = "¡Proyecto finalizado y listo para entrega!";
            }

            // Calcular y actualizar porcentaje
            // Si está en el último paso (exporte final), es el 100%
            let percentage = Math.round((index / (totalStages - 1)) * 100);
            
            progressFill.style.width = percentage + '%';
            percentageText.textContent = percentage + '% completado';
        }

        // Inicializar en la etapa 0
        updateProgress(0);
    </script>
</body>
</html>
