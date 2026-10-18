<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Treinamento Interativo com IA (Corrigido)</title>
    
    <!-- Scripts do TensorFlow.js carregados de forma otimizada -->
    <script src="https://jsdelivr.net"></script>
    <script src="https://jsdelivr.net"></script>

    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #121212;
            color: #ffffff;
            margin: 0;
            padding: 220px 20px 20px 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        #header-fixo {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            background-color: #1e1e1e;
            padding: 15px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.5);
            text-align: center;
            z-index: 1000;
        }
        .progress-container {
            width: 80%;
            background-color: #333;
            border-radius: 10px;
            margin: 10px auto;
            overflow: hidden;
        }
        .progress-bar {
            width: 0%;
            height: 20px;
            background-color: #00ff88;
            transition: width 0.3s ease;
        }
        #container-principal {
            display: flex;
            flex-direction: row;
            gap: 20px;
            max-width: 1000px;
            width: 100%;
            justify-content: center;
            align-items: flex-start;
        }
        .card {
            background-color: #1e1e1e;
            border-radius: 12px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0,0,0,0.3);
            flex: 1;
        }
        #camera-container {
            position: relative;
            width: 400px;
            height: 300px;
            background-color: #000;
            border-radius: 12px;
            overflow: hidden;
        }
        video, canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 400px;
            height: 300px;
            transform: scaleX(-1);
        }
        .status-exercicio {
            font-size: 24px;
            font-weight: bold;
            color: #00ff88;
            margin: 15px 0;
        }
        .contador {
            font-size: 48px;
            font-weight: bold;
            color: #ffffff;
        }
        .alerta-abdominal {
            background-color: #ff3333;
            color: white;
            padding: 10px;
            border-radius: 6px;
            margin-top: 10px;
            display: none;
            font-weight: bold;
        }
        .btn-manual {
            background-color: #22c55e;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 6px;
            cursor: pointer;
            margin-top: 15px;
            font-weight: bold;
            font-size: 16px;
        }
        .btn-manual:hover {
            background-color: #16a34a;
        }
        #status-sistema {
            color: #ffaa00;
            font-weight: bold;
            font-size: 16px;
            margin-bottom: 5px;
        }
    </style>
</head>
<body>

    <div id="header-fixo">
        <h2>🏋️ Sistema de Treino Supervisionado por IA</h2>
        <div id="status-sistema">Solicitando acesso à câmera...</div>
        <div class="progress-container">
            <div class="progress-bar" id="barra-progresso"></div>
        </div>
        <div>Progresso Geral: <span id="texto-progresso">0%</span></div>
    </div>

    <div id="container-principal">
        <div class="card">
            <h3 id="nome-exercicio">Inicializando...</h3>
            <p id="instrucao-exercicio">Dê a permissão da câmera no seu navegador para começar.</p>
            <div class="status-exercicio" id="meta-exercicio">Meta: --</div>
            <div class="contador" id="contador-reps">0</div>
            
            <div class="alerta-abdominal" id="aviso-abdominal">
                ⚠️ REGRA DO ABDOMINAL ATIVA: Se ficar inativo por mais de 5s, o treino reseta do zero!
            </div>
            <div id="cronometro-inatividade" style="margin-top: 5px; color: #ff3333; font-weight: bold; font-size: 18px;"></div>

            <button class="btn-manual" id="btn-manual" onclick="contarManual()" style="display:none;">+1 Repetição Manual</button>
        </div>

        <div class="card" style="display: flex; flex-direction: column; align-items: center;">
            <h3>👁️ Visão da IA</h3>
            <div id="camera-container">
                <video id="video" autoplay playsinline muted></video>
                <canvas id="output"></canvas>
            </div>
            <p style="font-size: 12px; color: #aaa; margin-top: 10px;">Afaste-se para que seu corpo apareça por completo na tela.</p>
        </div>
    </div>

    <script>
        const rotinaTreino = [
            { id: 0, nome: "Flexão de Mão Fechada", meta: 15, tipo: "flexao" },
            { id: 1, nome: "Flexão de Mão Aberta", meta: 20, tipo: "flexao" },
            { id: 2, nome: "Abdominais", meta: 30, tipo: "abdominal" },
            { id: 3, nome: "Agachamento", meta: 50, tipo: "agachamento" },
            { id: 4, nome: "Levantamento de Peso (Braço Esquerdo)", meta: 200, tipo: "peso" },
            { id: 5, nome: "Levantamento de Peso (Braço Direito)", meta: 200, tipo: "peso" }
        ];

        let exercicioAtualIndex = 0;
        let repeticoesAtuais = 0;
        let totalExercicios = rotinaTreino.length;

        let naPosicaoMover = false; 
        let ultimoMovimentoTempo = Date.now();
        let detector;
        let videoElement = document.getElementById('video');
        let canvasElement = document.getElementById('output');
        let ctx = canvasElement.getContext('2d');

        // Fluxo de Inicialização Garantido: Câmera -> Depois IA
        window.addEventListener('DOMContentLoaded', async () => {
            try {
                document.getElementById('status-sistema').innerText = "Visualizando câmera... Aceite a permissão de vídeo.";
                await iniciarCamera();
                
                document.getElementById('status-sistema').innerText = "🔄 Carregando Inteligência Artificial... Aguarde alguns segundos.";
                await iniciarIA();
                
                document.getElementById('status-sistema').innerText = "🟢 Sistema Pronto! IA Monitorando.";
                document.getElementById('status-sistema').style.color = "#00ff88";
                
                atualizarInterface();
                rodarDeteccao();
            } catch (erro) {
                console.error(erro);
                document.getElementById('status-sistema').innerText = "❌ Erro ao acessar a câmera ou iniciar a IA. Verifique as permissões.";
                document.getElementById('status-sistema').style.color = "#ff3333";
            }
        });

        async function iniciarCamera() {
            const restricoes = {
                video: { width: 400, height: 300, facingMode: "user" },
                audio: false
            };
            const stream = await navigator.mediaDevices.getUserMedia(restricoes);
            videoElement.srcObject = stream;
            return new Promise((resolve) => {
                videoElement.onloadedmetadata = () => {
                    videoElement.play();
                    resolve();
                };
            });
        }

        async function iniciarIA() {
            // Garante que o TensorFlow definiu o motor de execução antes de carregar o modelo
            await tf.ready();
            detector = await poseDetection.createDetector(
                poseDetection.SupportedModels.MoveNet,
                { modelType: poseDetection.movenet.modelType.SINGLEPOSE_LIGHTING }
            );
        }

        function atualizarInterface() {
            let ex = rotinaTreino[exercicioAtualIndex];
            document.getElementById('nome-exercicio').innerText = ex.nome;
            document.getElementById('meta-exercicio').innerText = `Meta: ${ex.meta} repetições`;
            document.getElementById('contador-reps').innerText = repeticoesAtuais;

            if(ex.tipo === "abdominal") {
                document.getElementById('aviso-abdominal').style.display = "block";
                ultimoMovimentoTempo = Date.now();
            } else {
                document.getElementById('aviso-abdominal').style.display = "none";
                document.getElementById('cronometro-inatividade').innerText = "";
            }

            // Exibe botão de emergência/suporte para exercícios longos
            if(ex.tipo === "peso" || ex.tipo === "flexao") {
                document.getElementById('btn-manual').style.display = "inline-block";
                document.getElementById('instrucao-exercicio').innerText = "A IA está rastreando. Se ela perder o ângulo no chão ou com o peso, use o botão verde.";
            } else {
                document.getElementById('btn-manual').style.display = "none";
                document.getElementById('instrucao-exercicio').innerText = "Faça o exercício em frente à câmera. A contagem é automática.";
            }

            let progressoGeral = (exercicioAtualIndex / totalExercicios) * 100;
            document.getElementById('barra-progresso').style.width = `${progressoGeral}%`;
            document.getElementById('texto-progresso').innerText = `${Math.round(progressoGeral)}%`;
        }

        function contarManual() {
            contarRepeticao();
        }

        function contarRepeticao() {
            let ex = rotinaTreino[exercicioAtualIndex];
