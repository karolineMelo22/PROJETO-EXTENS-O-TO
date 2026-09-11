<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pequenos Exploradores no Mundo da TO</title>
  <style>
    :root {
      --primary: #6B46C1;
      --secondary: #319795;
      --accent: #ED8936;
      --bg: #F7FAFC;
      --card-bg: #FFFFFF;
      --text: #2D3748;
    }

    body {
      font-family: 'Comic Sans MS', 'Segoe UI', Tahoma, sans-serif;
      margin: 0;
      padding: 0;
      background-color: var(--bg);
      color: var(--text);
    }

    header {
      background: linear-gradient(135deg, var(--primary), var(--secondary));
      color: white;
      text-align: center;
      padding: 2rem 1rem;
      border-bottom-left-radius: 20px;
      border-bottom-right-radius: 20px;
    }

    header h1 { margin: 0; font-size: 2rem; }
    header p { margin-top: 8px; font-size: 1.1rem; opacity: 0.95; }

    .nav-tabs {
      display: flex;
      justify-content: center;
      gap: 10px;
      margin: 20px 10px;
      flex-wrap: wrap;
    }

    .tab-btn {
      background: #E2E8F0;
      border: none;
      padding: 12px 20px;
      border-radius: 25px;
      font-weight: bold;
      color: var(--text);
      cursor: pointer;
      transition: all 0.3s;
    }

    .tab-btn.active {
      background: var(--primary);
      color: white;
      transform: scale(1.05);
    }

    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: 0 15px 40px 15px;
    }

    .tab-content {
      display: none;
      background: var(--card-bg);
      padding: 25px;
      border-radius: 15px;
      box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
    }

    .tab-content.active {
      display: block;
      animation: fadeIn 0.4s ease-in-out;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* ESTILOS DO GERADOR DE MISSÕES */
    .roulette-box {
      text-align: center;
      background: #EBF8FF;
      border: 2px dashed #3182CE;
      padding: 20px;
      border-radius: 12px;
      margin-top: 15px;
    }

    .btn-action {
      background: var(--accent);
      color: white;
      border: none;
      padding: 15px 30px;
      font-size: 1.1rem;
      font-weight: bold;
      border-radius: 30px;
      cursor: pointer;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
      transition: transform 0.2s;
    }

    .btn-action:hover { transform: scale(1.05); }

    /* ESTILOS DO JOGO */
    .game-canvas {
      width: 100%;
      height: 300px;
      background: #FEFCBF;
      border-radius: 12px;
      position: relative;
      overflow: hidden;
      cursor: pointer;
      border: 3px solid #D69E2E;
    }

    .bubble {
      width: 50px;
      height: 50px;
      background: var(--secondary);
      border-radius: 50%;
      position: absolute;
      animation: floatUp 4s infinite linear;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      font-weight: bold;
      user-select: none;
    }

    @keyframes floatUp {
      0% { bottom: -60px; }
      100% { bottom: 320px; }
    }

    /* CARDS FLIP */
    .card-flip {
      background: #EDF2F7;
      padding: 20px;
      border-radius: 10px;
      margin-bottom: 15px;
      cursor: pointer;
      border-left: 5px solid var(--primary);
    }

    .card-flip .answer {
      display: none;
      margin-top: 10px;
      color: #2B6CB0;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <header>
    <h1>🧠 Mundo TO: Pequenos Exploradores</h1>
    <p>Descubra a Terapia Ocupacional no dia a dia do seu filho!</p>
  </header>

  <div class="nav-tabs">
    <button class="tab-btn active" onclick="openTab('olhar')">👁️ Olhar da TO</button>
    <button class="tab-btn" onclick="openTab('missoes')">🎲 Missões Práticas</button>
    <button class="tab-btn" onclick="openTab('jogo')">🎮 Jogo Sensorial</button>
    <button class="tab-btn" onclick="openTab('mitos')">💡 Mitos e Verdades</button>
  </div>

  <div class="container">

    <!-- ABA 1: OLHAR DA TERAPIA OCUPACIONAL -->
    <div id="olhar" class="tab-content active">
      <h2>O que a Terapia Ocupacional enxerga?</h2>
      <p>Para um adulto, vestir uma roupa é automático. Para uma criança de 3 anos, envolve dezenas de habilidades motoras e sensoriais!</p>
      
      <p><strong>Escolha uma rotina para analisar com a visão do Terapeuta Ocupacional:</strong></p>
      
      <button class="tab-btn" onclick="mostrarCena('vestir')">👕 Hora de Vestir</button>
      <button class="tab-btn" onclick="mostrarCena('comida')">🥣 Hora da Refeição</button>
      <button class="tab-btn" onclick="mostrarCena('parque')">🛝 Brincar no Parquinho</button>

      <div id="cena-resultado" class="roulette-box" style="margin-top:20px; text-align:left;">
        <h3 id="cena-titulo">Clique em uma das rotinas acima!</h3>
        <p id="cena-desc">Descubra os "ingredientes motores e sensoriais" de cada momento.</p>
      </div>
    </div>

    <!-- ABA 2: GERADOR DE MISSÕES PRÁTICAS -->
    <div id="missoes" class="tab-content">
      <h2>Sua Missão do Dia em Casa</h2>
      <p>A Terapia Ocupacional usa a brincadeira como ferramenta. Clique no botão para sortear uma atividade simples usando o que você tem na sala ou na cozinha!</p>
      
      <div class="roulette-box">
        <button class="btn-action" onclick="sortearMissao()">🎰 Sortear Nova Missão</button>
        <h3 id="missao-titulo" style="margin-top:20px; color:var(--primary);">Pronto para brincar?</h3>
        <p id="missao-corpo">Clique no botão para receber o desafio motor do dia!</p>
      </div>
    </div>

    <!-- ABA 3: JOGO SENSORIAL EM TELA -->
    <div id="jogo" class="tab-content">
      <h2>Jogo do Rastreio Visual e Toque</h2>
      <p><strong>Para jogar junto com seu filho:</strong> Peça para ele estourar as bolhas sensoriais que sobem na tela!</p>
      <p>Pontuação: <span id="pop-count" style="font-weight:bold; color:var(--accent);">0</span> bolhas estouradas.</p>
      
      <div class="game-canvas" id="canvas" onclick="popBubble(event)">
        <div class="bubble" id="b1" style="left: 20%;">TO</div>
        <div class="bubble" id="b2" style="left: 60%; animation-delay: 2s;">TO</div>
      </div>
      
      <p style="font-size:0.9rem; color:#718096; margin-top:10px;">
        💡 <strong>Dica de TO:</strong> Atividades de acompanhar objetos com os olhos e tocar com precisão fortalecem os músculos oculares e preparam a criança para a leitura e escrita no futuro.
      </p>
    </div>

    <!-- ABA 4: MITOS E VERDADES -->
    <div id="mitos" class="tab-content">
      <h2>Desmistificando a Terapia Ocupacional</h2>
      <p>Clique nas perguntas abaixo para revelar o conceito científico:</p>

      <div class="card-flip" onclick="toggleAnswer(this)">
        <strong>1. "Terapia Ocupacional é a mesma coisa que Fisioterapia?"</strong>
        <div class="answer">NÃO! Enquanto a Fisioterapia foca na função física e movimento muscular, a Terapia Ocupacional foca no desempenho das atividades do dia a dia (comer, vestir, brincar, escovar dentes) e na integração dos sentidos.</div>
      </div>

      <div class="card-flip" onclick="toggleAnswer(this)">
        <strong>2. "O Terapeuta Ocupacional só atende crianças com deficiência?"</strong>
        <div class="answer">MITO! A TO atende qualquer criança que apresente dificuldades de coordenação, recusa alimentar por sensibilidade à textura dos alimentos, agitação extrema ou atrasos no desenvolvimento típico.</div>
      </div>

      <div class="card-flip" onclick="toggleAnswer(this)">
        <strong>3. "Brincar na terra ou com tinta faz parte da terapia?"</strong>
        <div class="answer">VERDADE! Isso se chama Integração Sensorial. Ajuda o cérebro da criança a processar estímulos táteis, diminuindo a hipersensibilidade e o medo de se sujar ou de tocar em texturas novas.</div>
      </div>
    </div>

  </div>

  <script>
    // LÓGICA DAS ABAS
    function openTab(tabId) {
      document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
      document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
      
      document.getElementById(tabId).classList.add('active');
      event.currentTarget.classList.add('active');
    }

    // LÓGICA DO OLHAR DA TO
    function mostrarCena(tipo) {
      const tit = document.getElementById('cena-titulo');
      const desc = document.getElementById('cena-desc');

      if (tipo === 'vestir') {
        tit.innerText = '👕 Na Hora de Vestir a Camiseta';
        desc.innerHTML = '<strong>Habilidades exigidas:</strong><br>• <i>Esquema Corporal:</i> Saber onde estão os braços e a cabeça sem olhar.<br>• <i>Planejamento Motor:</i> A sequência exata de puxar e encaixar.<br>• <i>Força Muscular de Tronco:</i> Manter o equilíbrio sentado enquanto passa a roupa.';
      } else if (tipo === 'comida') {
        tit.innerText = '🥣 Na Hora da Refeição';
        desc.innerHTML = '<strong>Habilidades exigidas:</strong><br>• <i>Processamento Tátil e Gustativo:</i> Aceitar diferentes texturas (crocante, pastoso).<br>• <i>Pega em Pinça:</i> Segurar a colher de forma funcional.<br>• <i>Coordenação Bimanual:</i> Segurar o prato com uma mão e a colher com a outra.';
      } else if (tipo === 'parque') {
        tit.innerText = '🛝 No Balanço e Trepa-Trepa';
        desc.innerHTML = '<strong>Habilidades exigidas:</strong><br>• <i>Sistema Vestibular:</i> Sentir o movimento do corpo no espaço sem ter tontura ou medo excessivo.<br>• <i>Sistema Proprioceptivo:</i> Ajustar a força nas mãos para segurar as correntes do balanço.';
      }
    }

    // LÓGICA DAS MISSÕES
    const missoes = [
      { t: "🧺 A Caça às Meias Perdidas", d: "Junte vários pares de meias coloridas desfeitas. Peça para a criança achar os pares iguais e enrolá-los fazendo uma 'bolinha'. Trabalha a percepção visual e a força nas mãos!" },
      { t: "🏎️ Pista de Fita Crepe", d: "Cole fitas no chão formando curvas. A criança deve empurrar um carrinho exatamente por cima da linha. Excelente para coordenação visual e controle de movimento!" },
      { t: "🏔️ A Montanha de Almofadas", d: "Empilhe almofadas no chão para a criança passar por cima engatinhando ou andando. Fortalece as articulações e trabalha o equilíbrio postural (propriocepção)." },
      { t: "🍝 Resgate do Macarrão", d: "Espalhe macarrão cru na mesa. Dê um pregador de roupa para a criança resgatar as peças e colocar no copo. Fortalece a pega em pinça!" },
      { t: "🕷️ A Teia de Aranha", d: "Passe barbante entre os pés de uma cadeira. Peça para a criança pegar um brinquedo no fundo sem encostar nos fios. Treina a noção espacial!" },
      { t: "🧱 Torre de Tampinhas", d: "Junte tampinhas de garrafa e desafie a criança a empilhar o máximo que conseguir sem derrubar. Trabalha o controle de força nas mãos!" },
      { t: "💧 Bacia da Esponja", d: "Coloque uma bacia com água e outra vazia. A criança deve molhar a esponja e espremer na outra bacia. Excelente para força de preensão!" },
      { t: "👣 Passos de Gigante", d: "Coloque folhas de papel no chão como pontes. A criança só pode pisar nelas para atravessar o cômodo. Desenvolve o equilíbrio e a coordenação!" },
      { t: "🎨 Pinta-Chão com Água", d: "Dê um pincel grande e um pote de água para a criança 'pintar' o muro ou chão do quintal. Prepara os ombros e braços para a futura escrita!" },
      { t: "📦 Túnel de Papelão", d: "Use caixas ou lençóis em cadeiras para fazer um túnel. A criança deve atravessar rastejando. Fortalece o tronco e a consciência corporal!" },
      { t: "🧊 Tesouro no Gelo", d: "Congele pequenos brinquedos em potes com água. A criança usa colheres e água morna para derreter e resgatar. Ótimo estímulo sensorial!" },
      { t: "🧦 Varal de Meias", d: "Amarre um barbante baixo e peça para a criança pendurar meias usando pregadores de roupa. Treina o uso integrado das duas mãos!" },
      { t: "🎳 Boliche de Garrafas", d: "Monte garrafas PET com um pouco de água no fundo e use uma bola de meia para derrubar. Trabalha a mira e a coordenação olho-mão!" }

    ];

    function sortearMissao() {
      const idx = Math.floor(Math.random() * missoes.length);
      document.getElementById('missao-titulo').innerText = missoes[idx].t;
      document.getElementById('missao-corpo').innerText = missoes[idx].d;
    }

    // LÓGICA DO JOGO SENSORIAL
    let score = 0;
    function popBubble(e) {
      if (e.target.classList.contains('bubble')) {
        score++;
        document.getElementById('pop-count').innerText = score;
        e.target.style.display = 'none';
        setTimeout(() => {
          e.target.style.display = 'flex';
        }, 1500);
      }
    }

    // LÓGICA DOS CARDS MITOS
    function toggleAnswer(card) {
      const ans = card.querySelector('.answer');
      ans.style.display = ans.style.display === 'block' ? 'none' : 'block';
    }
  </script>
</body>
</html>
