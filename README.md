# gerador-de-questoes-mm
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StudyQuiz - Gerador de Questões e Simulados</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #4e54c8;
            --secondary: #8f94fb;
            --accent: #ff6b6b;
            --light: #f8f9fa;
            --dark: #343a40;
            --success: #28a745;
            --warning: #ffc107;
            --info: #17a2b8;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            padding: 20px;
            color: var(--dark);
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        
        header {
            background: linear-gradient(to right, var(--primary), var(--secondary));
            color: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo i {
            font-size: 2.5rem;
            color: white;
        }
        
        .logo h1 {
            font-size: 2.2rem;
            font-weight: 700;
        }
        
        .logo p {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        nav {
            display: flex;
            gap: 15px;
        }
        
        nav button {
            background: rgba(255, 255, 255, 0.2);
            border: none;
            color: white;
            padding: 10px 20px;
            border-radius: 50px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        nav button:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: translateY(-2px);
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
        }
        
        .card {
            background: white;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
            padding: 25px;
            transition: transform 0.3s ease;
        }
        
        .card:hover {
            transform: translateY(-5px);
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--secondary);
        }
        
        .card-header h2 {
            color: var(--primary);
            font-size: 1.8rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .card-header i {
            background: var(--secondary);
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
        }
        
        .upload-area {
            border: 3px dashed var(--secondary);
            border-radius: 12px;
            padding: 30px;
            text-align: center;
            margin-bottom: 20px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .upload-area:hover {
            background: rgba(143, 148, 251, 0.05);
            border-color: var(--primary);
        }
        
        .upload-area i {
            font-size: 3rem;
            color: var(--secondary);
            margin-bottom: 15px;
        }
        
        .upload-area h3 {
            color: var(--primary);
            margin-bottom: 10px;
        }
        
        .upload-area p {
            color: var(--dark);
            margin-bottom: 15px;
        }
        
        .file-types {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 15px;
        }
        
        .file-type {
            background: var(--light);
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark);
        }
        
        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e1e5eb;
            border-radius: 10px;
            font-size: 1rem;
            transition: border 0.3s ease;
        }
        
        .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
            outline: none;
            border-color: var(--secondary);
        }
        
        textarea {
            min-height: 150px;
            resize: vertical;
        }
        
        button.primary-btn {
            background: linear-gradient(to right, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 14px 25px;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }
        
        button.primary-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(78, 84, 200, 0.3);
        }
        
        .quiz-container {
            display: none;
        }
        
        .question-container {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 12px;
            background: white;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.05);
        }
        
        .question-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
        }
        
        .question-text {
            font-size: 1.2rem;
            margin-bottom: 20px;
            line-height: 1.6;
        }
        
        .options-container {
            display: grid;
            grid-template-columns: 1fr;
            gap: 12px;
        }
        
        .option {
            padding: 15px;
            border: 2px solid #e1e5eb;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .option:hover {
            border-color: var(--secondary);
            background: rgba(143, 148, 251, 0.05);
        }
        
        .option.selected {
            border-color: var(--primary);
            background: rgba(78, 84, 200, 0.1);
        }
        
        .option input {
            margin-right: 10px;
        }
        
        .timer {
            background: var(--warning);
            color: var(--dark);
            padding: 10px 20px;
            border-radius: 50px;
            font-weight: 700;
            font-size: 1.3rem;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }
        
        .controls {
            display: flex;
            justify-content: space-between;
            margin-top: 25px;
        }
        
        .btn {
            padding: 12px 25px;
            border-radius: 10px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            border: none;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .btn-outline {
            background: white;
            border: 2px solid var(--primary);
            color: var(--primary);
        }
        
        .btn-outline:hover {
            background: rgba(78, 84, 200, 0.1);
        }
        
        .btn-primary {
            background: linear-gradient(to right, var(--primary), var(--secondary));
            color: white;
        }
        
        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(78, 84, 200, 0.3);
        }
        
        .results-container {
            display: none;
            padding: 30px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }
        
        .score-display {
            text-align: center;
            margin-bottom: 30px;
        }
        
        .score-circle {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            background: conic-gradient(var(--success) 0% 70%, var(--light) 70% 100%);
            margin: 0 auto 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--dark);
        }
        
        .explanation {
            background: var(--light);
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 20px;
        }
        
        .explanation h4 {
            margin-bottom: 10px;
            color: var(--primary);
        }
        
        .saved-contents {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .content-card {
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.08);
            transition: all 0.3s ease;
            border-left: 4px solid var(--primary);
        }
        
        .content-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .content-header {
            padding: 15px;
            background: rgba(78, 84, 200, 0.05);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .content-body {
            padding: 15px;
        }
        
        .content-body h4 {
            margin-bottom: 10px;
            color: var(--dark);
        }
        
        .content-footer {
            padding: 15px;
            display: flex;
            justify-content: space-between;
            border-top: 1px solid #eee;
        }
        
        .tab-container {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .tab {
            padding: 10px 20px;
            background: var(--light);
            border-radius: 8px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
        }
        
        .tab.active {
            background: var(--primary);
            color: white;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .mock-test-btn {
            margin-top: 20px;
            background: linear-gradient(to right, var(--accent), #ff8e8e);
        }
        
        .mock-test-btn:hover {
            box-shadow: 0 5px 15px rgba(255, 107, 107, 0.3);
        }
        
        footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            color: var(--dark);
            font-size: 0.9rem;
        }
        
        @media (max-width: 900px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            header {
                flex-direction: column;
                text-align: center;
                gap: 20px;
            }
            
            nav {
                flex-wrap: wrap;
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-brain"></i>
                <div>
                    <h1>StudyQuiz</h1>
                    <p>Gerador de Questões e Simulados Inteligentes</p>
                </div>
            </div>
            <nav>
                <button id="navUpload"><i class="fas fa-upload"></i> Enviar Conteúdo</button>
                <button id="navContents"><i class="fas fa-book"></i> Meus Conteúdos</button>
                <button id="navQuiz"><i class="fas fa-question-circle"></i> Gerar Quiz</button>
                <button id="navMock"><i class="fas fa-clock"></i> Simulado</button>
            </nav>
        </header>
        
        <div class="main-content">
            <!-- Upload Section -->
            <div class="card upload-section">
                <div class="card-header">
                    <h2><i class="fas fa-cloud-upload-alt"></i> Enviar Conteúdo</h2>
                </div>
                
                <div class="upload-area" id="dropArea">
                    <i class="fas fa-file-upload"></i>
                    <h3>Arraste e solte seu arquivo aqui</h3>
                    <p>ou</p>
                    <button class="primary-btn" id="browseBtn">
                        <i class="fas fa-folder-open"></i> Procurar arquivo
                    </button>
                    <input type="file" id="fileInput" accept=".pdf,.doc,.docx,.txt,.pptx" style="display: none;">
                    
                    <div class="file-types">
                        <span class="file-type"><i class="fas fa-file-pdf"></i> PDF</span>
                        <span class="file-type"><i class="fas fa-file-word"></i> Word</span>
                        <span class="file-type"><i class="fas fa-file-alt"></i> Texto</span>
                        <span class="file-type"><i class="fas fa-file-powerpoint"></i> Slides</span>
                    </div>
                </div>
                
                <div class="form-group">
                    <label for="contentText">Ou cole seu texto aqui:</label>
                    <textarea id="contentText" placeholder="Digite ou cole o conteúdo que deseja utilizar para gerar questões..."></textarea>
                </div>
                
                <button class="primary-btn" id="saveContentBtn">
                    <i class="fas fa-save"></i> Salvar Conteúdo
                </button>
            </div>
            
            <!-- Quiz Generator -->
            <div class="card quiz-generator">
                <div class="card-header">
                    <h2><i class="fas fa-question-circle"></i> Gerar Questões</h2>
                </div>
                
                <div class="form-group">
                    <label for="contentSelect">Selecione o conteúdo:</label>
                    <select id="contentSelect">
                        <option value="">-- Selecione um conteúdo salvo --</option>
                        <option value="1">Introdução à Biologia</option>
                        <option value="2">História do Brasil</option>
                        <option value="3">Matemática Básica</option>
                        <option value="4">Física Quântica</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="questionCount">Número de questões:</label>
                    <input type="number" id="questionCount" min="1" max="50" value="10">
                </div>
                
                <div class="form-group">
                    <label for="difficulty">Dificuldade:</label>
                    <select id="difficulty">
                        <option value="easy">Fácil</option>
                        <option value="medium" selected>Médio</option>
                        <option value="hard">Difícil</option>
                    </select>
                </div>
                
                <button class="primary-btn" id="generateBtn">
                    <i class="fas fa-cogs"></i> Gerar Questões
                </button>
            </div>
            
            <!-- Saved Contents -->
            <div class="card saved-contents-section">
                <div class="card-header">
                    <h2><i class="fas fa-book"></i> Conteúdos Salvos</h2>
                </div>
                
                <div class="saved-contents">
                    <div class="content-card">
                        <div class="content-header">
                            <i class="fas fa-file-alt text-primary"></i>
                            <h3>Introdução à Biologia</h3>
                        </div>
                        <div class="content-body">
                            <h4>Conteúdo sobre células, DNA e evolução</h4>
                            <p>Biologia é a ciência que estuda a vida e os organismos vivos...</p>
                        </div>
                        <div class="content-footer">
                            <span><i class="fas fa-calendar"></i> 15/06/2025</span>
                            <button class="btn btn-outline"><i class="fas fa-trash"></i></button>
                        </div>
                    </div>
                    
                    <div class="content-card">
                        <div class="content-header">
                            <i class="fas fa-file-pdf text-danger"></i>
                            <h3>História do Brasil</h3>
                        </div>
                        <div class="content-body">
                            <h4>Da colonização à república</h4>
                            <p>O Brasil foi descoberto pelos portugueses em 1500...</p>
                        </div>
                        <div class="content-footer">
                            <span><i class="fas fa-calendar"></i> 10/06/2025</span>
                            <button class="btn btn-outline"><i class="fas fa-trash"></i></button>
                        </div>
                    </div>
                    
                    <div class="content-card">
                        <div class="content-header">
                            <i class="fas fa-file-word text-info"></i>
                            <h3>Matemática Básica</h3>
                        </div>
                        <div class="content-body">
                            <h4>Álgebra, geometria e trigonometria</h4>
                            <p>A matemática é a ciência do raciocínio lógico...</p>
                        </div>
                        <div class="content-footer">
                            <span><i class="fas fa-calendar"></i> 05/06/2025</span>
                            <button class="btn btn-outline"><i class="fas fa-trash"></i></button>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- Mock Test -->
            <div class="card mock-test-section">
                <div class="card-header">
                    <h2><i class="fas fa-clock"></i> Simulado</h2>
                </div>
                
                <div class="form-group">
                    <label for="mockContentSelect">Selecione o conteúdo para o simulado:</label>
                    <select id="mockContentSelect">
                        <option value="">-- Selecione um conteúdo --</option>
                        <option value="1">Introdução à Biologia</option>
                        <option value="2">História do Brasil</option>
                        <option value="3">Matemática Básica</option>
                        <option value="4">Física Quântica</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label>Configurações do Simulado:</label>
                    <div style="background: #f8f9fa; padding: 15px; border-radius: 10px;">
                        <p><i class="fas fa-check-circle text-success"></i> 30 questões</p>
                        <p><i class="fas fa-check-circle text-success"></i> Dificuldade média e difícil</p>
                        <p><i class="fas fa-check-circle text-success"></i> Tempo limite: 30 minutos</p>
                    </div>
                </div>
                
                <button class="primary-btn mock-test-btn" id="startMockBtn">
                    <i class="fas fa-play-circle"></i> Iniciar Simulado
                </button>
            </div>
        </div>
        
        <!-- Quiz Container -->
        <div class="quiz-container" id="quizContainer">
            <div class="card">
                <div class="question-header">
                    <h2>Questões Geradas</h2>
                    <div class="timer">
                        <i class="fas fa-clock"></i> <span id="quizTimer">30:00</span>
                    </div>
                </div>
                
                <div class="question-container">
                    <div class="question-text" id="questionText">
                        Qual é a organela responsável pela produção de energia nas células eucarióticas?
                    </div>
                    
                    <div class="options-container" id="optionsContainer">
                        <div class="option">
                            <input type="radio" name="answer" id="option1">
                            <label for="option1">Retículo endoplasmático</label>
                        </div>
                        <div class="option">
                            <input type="radio" name="answer" id="option2">
                            <label for="option2">Mitocôndria</label>
                        </div>
                        <div class="option">
                            <input type="radio" name="answer" id="option3">
                            <label for="option3">Complexo de Golgi</label>
                        </div>
                        <div class="option">
                            <input type="radio" name="answer" id="option4">
                            <label for="option4">Núcleo</label>
                        </div>
                    </div>
                </div>
                
                <div class="controls">
                    <button class="btn btn-outline" id="prevBtn">
                        <i class="fas fa-arrow-left"></i> Anterior
                    </button>
                    <div>Questão <span id="currentQuestion">1</span> de <span id="totalQuestions">10</span></div>
                    <button class="btn btn-primary" id="nextBtn">
                        Próxima <i class="fas fa-arrow-right"></i>
                    </button>
                </div>
            </div>
        </div>
        
        <!-- Results Container -->
        <div class="results-container" id="resultsContainer">
            <div class="score-display">
                <div class="score-circle">7/10</div>
                <h2>Resultado do Quiz</h2>
                <p>Você acertou 7 de 10 questões!</p>
            </div>
            
            <h3>Explicações:</h3>
            
            <div class="explanation">
                <h4>Questão 1: Qual é a organela responsável pela produção de energia?</h4>
                <p><strong>Sua resposta:</strong> Mitocôndria <i class="fas fa-check-circle text-success"></i></p>
                <p><strong>Explicação:</strong> A mitocôndria é conhecida como a "usina de energia" da célula, onde ocorre a respiração celular e a produção de ATP.</p>
            </div>
            
            <div class="explanation">
                <h4>Questão 2: Quem foi o primeiro presidente do Brasil?</h4>
                <p><strong>Sua resposta:</strong> Dom Pedro I <i class="fas fa-times-circle text-danger"></i></p>
                <p><strong>Resposta correta:</strong> Deodoro da Fonseca</p>
                <p><strong>Explicação:</strong> Marechal Deodoro da Fonseca foi o primeiro presidente do Brasil, proclamando a república em 1889 e governando até 1891.</p>
            </div>
            
            <div class="controls" style="justify-content: center; margin-top: 30px;">
                <button class="btn btn-primary" id="backToStart">
                    <i class="fas fa-home"></i> Voltar ao Início
                </button>
            </div>
        </div>
        
        <footer>
            <p>StudyQuiz &copy; 2025 - Gerador de Questões e Simulados Inteligentes</p>
            <p>Desenvolvido para otimizar seus estudos e preparação para provas</p>
        </footer>
    </div>
    
    <script>
        // Navigation
        document.getElementById('navUpload').addEventListener('click', () => {
            document.querySelector('.upload-section').scrollIntoView({ behavior: 'smooth' });
        });
        
        document.getElementById('navContents').addEventListener('click', () => {
            document.querySelector('.saved-contents-section').scrollIntoView({ behavior: 'smooth' });
        });
        
        document.getElementById('navQuiz').addEventListener('click', () => {
            document.querySelector('.quiz-generator').scrollIntoView({ behavior: 'smooth' });
        });
        
        document.getElementById('navMock').addEventListener('click', () => {
            document.querySelector('.mock-test-section').scrollIntoView({ behavior: 'smooth' });
        });
        
        // File Upload
        const dropArea = document.getElementById('dropArea');
        const fileInput = document.getElementById('fileInput');
        const browseBtn = document.getElementById('browseBtn');
        
        ['dragenter', 'dragover', 'dragleave', 'drop'].forEach(eventName => {
            dropArea.addEventListener(eventName, preventDefaults, false);
        });
        
        function preventDefaults(e) {
            e.preventDefault();
            e.stopPropagation();
        }
        
        ['dragenter', 'dragover'].forEach(eventName => {
            dropArea.addEventListener(eventName, highlight, false);
        });
        
        ['dragleave', 'drop'].forEach(eventName => {
            dropArea.addEventListener(eventName, unhighlight, false);
        });
        
        function highlight() {
            dropArea.style.borderColor = '#4e54c8';
            dropArea.style.backgroundColor = 'rgba(78, 84, 200, 0.05)';
        }
        
        function unhighlight() {
            dropArea.style.borderColor = '#8f94fb';
            dropArea.style.backgroundColor = '';
        }
        
        dropArea.addEventListener('drop', handleDrop, false);
        
        function handleDrop(e) {
            const dt = e.dataTransfer;
            const files = dt.files;
            handleFiles(files);
        }
        
        browseBtn.addEventListener('click', () => {
            fileInput.click();
        });
        
        fileInput.addEventListener('change', () => {
            handleFiles(fileInput.files);
        });
        
        function handleFiles(files) {
            if (files.length > 0) {
                const file = files[0];
                const fileName = file.name;
                const fileSize = (file.size / 1024 / 1024).toFixed(2); // in MB
                
                // Simulate file processing
                dropArea.innerHTML = `
                    <i class="fas fa-file-alt" style="color: #4e54c8;"></i>
                    <h3>${fileName}</h3>
                    <p>${fileSize} MB</p>
                    <div class="file-types">
                        <span class="file-type">Arquivo carregado com sucesso!</span>
                    </div>
                `;
                
                // Show file type icon based on extension
                const fileType = fileName.split('.').pop().toLowerCase();
                let iconClass = 'fas fa-file';
                
                if (fileType === 'pdf') iconClass = 'fas fa-file-pdf text-danger';
                if (fileType === 'doc' || fileType === 'docx') iconClass = 'fas fa-file-word text-info';
                if (fileType === 'txt') iconClass = 'fas fa-file-alt text-primary';
                if (fileType === 'pptx') iconClass = 'fas fa-file-powerpoint text-warning';
                
                dropArea.querySelector('i').className = iconClass;
            }
        }
        
        // Save Content
        document.getElementById('saveContentBtn').addEventListener('click', () => {
            const contentText = document.getElementById('contentText').value;
            if (contentText.trim() !== '' || document.querySelector('.upload-area h3').textContent !== 'Arraste e solte seu arquivo aqui') {
                // Show success message
                alert('Conteúdo salvo com sucesso!');
                
                // Reset form
                document.getElementById('contentText').value = '';
                dropArea.innerHTML = `
                    <i class="fas fa-file-upload"></i>
                    <h3>Arraste e solte seu arquivo aqui</h3>
                    <p>ou</p>
                    <button class="primary-btn" id="browseBtn">
                        <i class="fas fa-folder-open"></i> Procurar arquivo
                    </button>
                    <div class="file-types">
                        <span class="file-type"><i class="fas fa-file-pdf"></i> PDF</span>
                        <span class="file-type"><i class="fas fa-file-word"></i> Word</span>
                        <span class="file-type"><i class="fas fa-file-alt"></i> Texto</span>
                        <span class="file-type"><i class="fas fa-file-powerpoint"></i> Slides</span>
                    </div>
                `;
                
                // Reattach event listeners
                document.getElementById('browseBtn').addEventListener('click', () => {
                    fileInput.click();
                });
            } else {
                alert('Por favor, adicione um conteúdo antes de salvar.');
            }
        });
        
        // Quiz Generation
        document.getElementById('generateBtn').addEventListener('click', () => {
            const contentSelect = document.getElementById('contentSelect').value;
            if (contentSelect === '') {
                alert('Por favor, selecione um conteúdo para gerar as questões.');
                return;
            }
            
            document.querySelector('.main-content').style.display = 'none';
            document.getElementById('quizContainer').style.display = 'block';
            
            // Start timer only for mock test
            // startTimer(1800); // 30 minutes
        });
        
        // Mock Test
        document.getElementById('startMockBtn').addEventListener('click', () => {
            const mockContent = document.getElementById('mockContentSelect').value;
            if (mockContent === '') {
                alert('Por favor, selecione um conteúdo para o simulado.');
                return;
            }
            
            document.querySelector('.main-content').style.display = 'none';
            document.getElementById('quizContainer').style.display = 'block';
            
            // Update UI for mock test
            document.querySelector('.question-header h2').textContent = 'Simulado - 30 Questões';
            document.getElementById('totalQuestions').textContent = '30';
            document.querySelector('.timer').style.display = 'inline-flex';
            
            // Start timer for mock test
            startTimer(1800); // 30 minutes
        });
        
        // Timer function
        function startTimer(duration) {
            let timer = duration;
            const display = document.getElementById('quizTimer');
            const timerInterval = setInterval(() => {
                const minutes = Math.floor(timer / 60);
                const seconds = timer % 60;
                
                display.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                
                if (--timer < 0) {
                    clearInterval(timerInterval);
                    finishQuiz();
                }
            }, 1000);
        }
        
        // Quiz Navigation
        let currentQuestion = 1;
        const totalQuestions = 10; // Would be 30 for mock test
        
        document.getElementById('nextBtn').addEventListener('click', () => {
            if (currentQuestion < totalQuestions) {
                currentQuestion++;
                document.getElementById('currentQuestion').textContent = currentQuestion;
                
                // Update question text and options (simulated)
                document.getElementById('questionText').textContent = `Questão ${currentQuestion}: ${getRandomQuestion()}`;
                
                // Reset options
                document.querySelectorAll('input[name="answer"]').forEach(input => {
                    input.checked = false;
                });
                
                // Update button states
                document.getElementById('prevBtn').disabled = false;
                if (currentQuestion === totalQuestions) {
                    document.getElementById('nextBtn').innerHTML = 'Finalizar <i class="fas fa-check"></i>';
                }
            } else {
                finishQuiz();
            }
        });
        
        document.getElementById('prevBtn').addEventListener('click', () => {
            if (currentQuestion > 1) {
                currentQuestion--;
                document.getElementById('currentQuestion').textContent = currentQuestion;
                
                // Update question text and options (simulated)
                document.getElementById('questionText').textContent = `Questão ${currentQuestion}: ${getRandomQuestion()}`;
                
                // Reset options
                document.querySelectorAll('input[name="answer"]').forEach(input => {
                    input.checked = false;
                });
                
                // Update button states
                document.getElementById('nextBtn').innerHTML = 'Próxima <i class="fas fa-arrow-right"></i>';
                if (currentQuestion === 1) {
                    document.getElementById('prevBtn').disabled = true;
                }
            }
        });
        
        // Option selection
        document.querySelectorAll('.option').forEach(option => {
            option.addEventListener('click', () => {
                option.querySelector('input').checked = true;
                document.querySelectorAll('.option').forEach(opt => {
                    opt.classList.remove('selected');
                });
                option.classList.add('selected');
            });
        });
        
        function finishQuiz() {
            document.getElementById('quizContainer').style.display = 'none';
            document.getElementById('resultsContainer').style.display = 'block';
        }
        
        document.getElementById('backToStart').addEventListener('click', () => {
            document.getElementById('resultsContainer').style.display = 'none';
            document.querySelector('.main-content').style.display = 'grid';
            currentQuestion = 1;
            document.getElementById('currentQuestion').textContent = '1';
            document.getElementById('nextBtn').innerHTML = 'Próxima <i class="fas fa-arrow-right"></i>';
            document.getElementById('prevBtn').disabled = true;
        });
        
        // Helper function to generate random questions
        function getRandomQuestion() {
            const questions = [
                "Qual é o processo pelo as plantas convertem luz solar em energia?",
                "Quem escreveu 'Os Sertões'?",
                "Qual é a fórmula da área de um círculo?",
                "Qual elemento químico tem o símbolo 'Au'?",
                "Qual é o maior planeta do sistema solar?",
                "Quem foi o primeiro homem a pisar na lua?",
                "Qual é o rio mais longo do mundo?",
                "Em que ano o Brasil declarou sua independência?",
                "Qual é o processo de divisão celular que resulta em células filhas idênticas?",
                "Quem pintou 'Mona Lisa'?"
            ];
            
            return questions[Math.floor(Math.random() * questions.length)];
        }
    </script>
</body>
</html>
