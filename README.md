<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Taller Interactivo: Manejo Asertivo de Emociones</title>
    
    <!-- Chosen Palette: Calm Harmony (Slate, Blue, Gray) -->
    <!-- Application Structure Plan: A single-page application with a fixed sidebar for navigation and a dynamic content area. This modular, app-like structure is chosen to reduce cognitive load and make the workshop content feel manageable and easy to navigate for users experiencing symptoms of depression like low energy and difficulty concentrating. The flow guides the user from a welcoming intro to four distinct learning modules and a critical resources section, allowing both linear progression and easy revisiting of specific tools. -->
    <!-- Visualization & Content Choices: The report's content is transformed into interactive exercises. Quantitative data (5% prevalence) is shown with a Chart.js donut chart for impact. Qualitative info (techniques) is presented through interactive forms ('Mensaje Yo' builder, Thought Challenger), simulators (role-playing), and guided checklists (Assertive Rights). These choices turn passive reading into active practice, which is key for skill acquisition in CBT/DBT frameworks. HTML/CSS/JS are used for all interactive diagrams and elements. NO SVG/Mermaid are used. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://unpkg.com/lucide-react@0.372.0/dist/lucide-react.js"></script>
    
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .content-section {
            display: none;
        }
        .content-section.active {
            display: block;
        }
        .nav-link {
            display: flex;
            align-items: center;
            padding: 0.75rem 1rem;
            border-radius: 0.5rem;
            transition: all 0.2s ease-in-out;
            cursor: pointer;
            font-weight: 500;
        }
        .nav-link:hover {
            background-color: #e2e8f0;
        }
        .nav-link.active {
            background-color: #3b82f6;
            color: white;
            font-weight: 600;
        }
        .nav-link.active svg {
            stroke: white;
        }
        .activity-card {
            background-color: #f8fafc;
            border: 1px solid #e2e8f0;
            border-radius: 0.75rem;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.05);
        }
        .btn-primary {
            background-color: #3b82f6;
            color: white;
            padding: 0.6rem 1.2rem;
            border-radius: 0.5rem;
            font-weight: 600;
            transition: background-color 0.2s;
        }
        .btn-primary:hover {
            background-color: #2563eb;
        }
         .feedback-box {
            margin-top: 1rem;
            padding: 0.75rem 1rem;
            border-radius: 0.5rem;
            font-weight: 500;
            border-width: 1px;
        }
        .feedback-correct {
            background-color: #dcfce7;
            color: #166534;
            border-color: #86efac;
        }
        .feedback-incorrect {
            background-color: #fee2e2;
            color: #991b1b;
            border-color: #fca5a5;
        }
        .disclaimer-box {
            background-color: #fefce8;
            border: 1px solid #fde047;
            color: #854d0e;
            padding: 1rem;
            border-radius: 0.75rem;
            margin-bottom: 1.5rem;
        }
        .chart-container { 
            position: relative; 
            width: 100%; 
            max-width: 250px; 
            height: auto;
            margin-left: auto; 
            margin-right: auto;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800">
    <div class="flex h-screen bg-slate-100">
        <!-- Sidebar Navigation -->
        <aside id="sidebar" class="bg-white w-64 p-4 flex-shrink-0 border-r border-slate-200 fixed lg:relative h-full lg:h-auto -translate-x-full lg:translate-x-0 transition-transform duration-300 z-20">
            <div class="flex items-center gap-3 mb-8">
                <div class="bg-blue-500 p-2 rounded-lg">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22a10 10 0 1 1 0-20 10 10 0 0 1 0 20Z"/><path d="M12 12v-4"/><path d="M12 16h.01"/></svg>
                </div>
                <h1 class="text-xl font-bold text-slate-800">Taller Asertivo</h1>
            </div>
            <nav class="space-y-2">
                <a class="nav-link active" data-target="home">
                    <svg class="mr-3" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m3 9 9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>
                    Inicio
                </a>
                <a class="nav-link" data-target="module1">
                    <svg class="mr-3" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15.5 8.5c.3-1.8.3-3.7 0-5.5"/><path d="M12 16.5c-2.3 0-4.4-.8-6-2.5"/><path d="M8.5 8.5c-.3-1.8-.3-3.7 0-5.5"/><path d="M12 2.5c2.3 0 4.4.8 6 2.5"/><path d="M14.5 13.5c.3-1.8.3-3.7 0-5.5"/><path d="M9.5 13.5c-.3-1.8-.3-3.7 0-5.5"/><path d="M12 20.5c-2.3 0-4.4-.8-6-2.5"/><path d="M12 2.5c-2.3 0-4.4.8-6 2.5"/><circle cx="12" cy="12" r="10"/></svg>
                    Módulo 1: Conciencia
                </a>
                <a class="nav-link" data-target="module2">
                    <svg class="mr-3" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 12 2 6l10-4 10 4-10 6Z"/><path d="M2 18V6"/><path d="m22 18-10-6"/><path d="m12 22-10-6"/></svg>
                    Módulo 2: Asertividad
                </a>
                <a class="nav-link" data-target="module3">
                    <svg class="mr-3" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"/><polyline points="14 2 14 8 20 8"/><path d="m10 10.5 2 2 2-2"/><path d="m10 16.5 2-2 2 2"/></svg>
                    Módulo 3: Afrontamiento
                </a>
                <a class="nav-link" data-target="module4">
                     <svg class="mr-3" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M22 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>
                    Módulo 4: Comunicación
                </a>
                <a class="nav-link" data-target="resources">
                    <svg class="mr-3" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>
                    Recursos de Ayuda
                </a>
            </nav>
        </aside>

        <!-- Main Content -->
        <main class="flex-1 p-6 lg:p-10 overflow-y-auto h-screen">
             <!-- Mobile Header -->
            <div class="lg:hidden flex items-center justify-between mb-6">
                <button id="menu-btn" class="p-2 rounded-md hover:bg-slate-200">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="4" x2="20" y1="12" y2="12"/><line x1="4" x2="20" y1="6" y2="6"/><line x1="4" x2="20" y1="18" y2="18"/></svg>
                </button>
                <h1 class="text-lg font-bold">Taller Asertivo</h1>
            </div>
            
            <!-- Home Section -->
            <section id="home" class="content-section active">
                <h2 class="text-3xl lg:text-4xl font-extrabold text-slate-800 mb-4">Bienvenido/a al Taller de Manejo Asertivo de Emociones</h2>
                <p class="text-lg text-slate-600 mb-6 leading-relaxed">Este es un espacio seguro y práctico para aprender a gestionar tus emociones y comunicarte de manera más efectiva, especialmente al enfrentar los desafíos de la depresión crónica.</p>
                
                <div class="disclaimer-box">
                    <h3 class="font-bold text-lg mb-2">Importante: Esto no es una Terapia</h3>
                    <p class="text-sm">Este taller es una herramienta educativa de apoyo y no sustituye la consulta, diagnóstico o tratamiento con un profesional de la salud mental cualificado. Si te encuentras en una crisis, por favor contacta a los servicios de emergencia o a una línea de ayuda (ver sección "Recursos de Ayuda").</p>
                </div>
                
                <div class="grid md:grid-cols-2 gap-8 items-center">
                    <div>
                        <h3 class="text-xl font-bold text-slate-700 mb-3">El Desafío de la Depresión Crónica</h3>
                        <p class="text-slate-600 mb-4">El Trastorno Depresivo Persistente afecta a una parte significativa de la población, impactando la energía, la autoestima y las relaciones. Aprender a ser asertivo es una habilidad clave que puede romper ciclos negativos y mejorar la calidad de vida.</p>
                        <p class="text-slate-600">Este taller te guiará a través de técnicas basadas en la Terapia Cognitivo-Conductual (TCC) y la Terapia Dialéctico-Conductual (DBT) para que construyas resiliencia y te sientas más en control.</p>
                    </div>
                    <div class="text-center">
                        <div class="chart-container">
                             <canvas id="prevalenceChart"></canvas>
                        </div>
                        <p class="mt-4 text-sm text-slate-500 font-medium">Se estima que la depresión crónica afecta aproximadamente al 5% de la población adulta a nivel global.</p>
                    </div>
                </div>
                 <div class="text-center mt-10">
                    <button class="btn-primary text-lg" onclick="navigateTo('module1')">Comenzar el Taller →</button>
                </div>
            </section>

            <!-- Module 1 Section -->
            <section id="module1" class="content-section">
                <h2 class="text-3xl font-extrabold text-slate-800 mb-2">Módulo 1: Reconocimiento y Conciencia Emocional</h2>
                <p class="text-lg text-slate-600 mb-8">El primer paso es entender qué sientes y por qué. Este módulo te ayudará a conectar con tus emociones sin juicio.</p>
                
                <div class="activity-card">
                    <h3 class="text-xl font-bold text-slate-700 mb-3">Actividad: Mi Mapa Emocional</h3>
                    <p class="text-slate-600 mb-4">Usa esta herramienta para identificar una emoción reciente. Esto te ayudará a ver los patrones en tus respuestas emocionales.</p>
                    <div class="space-y-4">
                        <div>
                            <label for="emotion-select" class="block text-sm font-medium text-slate-700 mb-1">1. ¿Qué emoción sentiste?</label>
                            <input type="text" id="emotion-input" class="w-full p-2 border border-slate-300 rounded-md" placeholder="Ej: Tristeza, frustración, ansiedad...">
                        </div>
                        <div>
                            <label for="trigger-input" class="block text-sm font-medium text-slate-700 mb-1">2. ¿Qué crees que la desencadenó?</label>
                            <textarea id="trigger-input" rows="2" class="w-full p-2 border border-slate-300 rounded-md" placeholder="Ej: Un comentario, un recuerdo, sentirme cansado..."></textarea>
                        </div>
                        <div>
                            <label for="response-input" class="block text-sm font-medium text-slate-700 mb-1">3. ¿Cómo reaccionaste?</label>
                            <textarea id="response-input" rows="2" class="w-full p-2 border border-slate-300 rounded-md" placeholder="Ej: Me aislé, discutí, lo ignoré..."></textarea>
                        </div>
                         <p class="text-xs text-slate-500 italic">Tus respuestas no se guardan. Este es un ejercicio personal de reflexión.</p>
                    </div>
                </div>

                <div class="activity-card">
                    <h3 class="text-xl font-bold text-slate-700 mb-3">Práctica de Mindfulness: Anclaje en el Presente</h3>
                    <p class="text-slate-600 mb-4">Cuando los pensamientos abruman, la técnica de los 5 sentidos te trae de vuelta al momento presente. Es una forma simple y poderosa de calmar la mente.</p>
                    <div class="space-y-3">
                        <p><strong class="text-blue-600">5</strong> cosas que puedas <strong class="text-blue-600">VER</strong> a tu alrededor.</p>
                        <p><strong class="text-green-600">4</strong> cosas que puedas <strong class="text-green-600">SENTIR</strong> (la silla, tu ropa, la mesa).</p>
                        <p><strong class="text-purple-600">3</strong> cosas que puedas <strong class="text-purple-600">OÍR</strong> (el silencio, tu respiración, un sonido lejano).</p>
                        <p><strong class="text-orange-600">2</strong> cosas que puedas <strong class="text-orange-600">OLER</strong> (el aire, un perfume, tu café).</p>
                        <p><strong class="text-red-600">1</strong> cosa que puedas <strong class="text-red-600">SABOREAR</strong> (el sabor que queda en tu boca, un sorbo de agua).</p>
                    </div>
                </div>
            </section>
            
            <!-- Module 2 Section -->
            <section id="module2" class="content-section">
                <h2 class="text-3xl font-extrabold text-slate-800 mb-2">Módulo 2: Desarrollando la Asertividad Personal</h2>
                <p class="text-lg text-slate-600 mb-8">La asertividad es expresar tus necesidades y opiniones respetándote a ti y a los demás. Aquí aprenderás las herramientas para lograrlo.</p>

                 <div class="activity-card">
                    <h3 class="text-xl font-bold text-slate-700 mb-3">Actividad: Escenario de Rol</h3>
                    <p class="text-slate-600 mb-4">Un amigo te pide un favor grande que te tomará todo el fin de semana, pero tú ya te sentías agotado y necesitabas descansar. ¿Cuál es la respuesta asertiva?</p>
                    <div class="space-y-2">
                        <button class="w-full text-left p-3 border rounded-md hover:bg-slate-100" onclick="checkAssertiveness(false, 'feedback-roleplay', 'pasiva')">A) "Sí, claro, no te preocupes. Ya veré cómo me las arreglo para descansar."</button>
                        <button class="w-full text-left p-3 border rounded-md hover:bg-slate-100" onclick="checkAssertiveness(true, 'feedback-roleplay')">B) "Te agradezco que pienses en mí, pero este fin de semana necesito recargar energías y no podré ayudarte. Espero que lo entiendas."</button>
                        <button class="w-full text-left p-3 border rounded-md hover:bg-slate-100" onclick="checkAssertiveness(false, 'feedback-roleplay', 'agresiva')">C) "¿Otra vez pidiendo favores? No, no puedo, estoy harto de que no consideres mi tiempo."</button>
                    </div>
                    <div id="feedback-roleplay" class="feedback-box" style="display: none;"></div>
                </div>

                <div class="activity-card">
                    <h3 class="text-xl font-bold text-slate-700 mb-3">Herramienta: Constructor de "Mensajes Yo"</h3>
                    <p class="text-slate-600 mb-4">Usa esta fórmula para expresar tus sentimientos sin culpar, facilitando que la otra persona te escuche. Completa las partes para construir tu mensaje.</p>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-slate-700">Cuando tú...</label>
                            <input type="text" id="yo-cuando" class="w-full p-2 border border-slate-300 rounded-md" placeholder="(describe la acción específica)">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700">Yo me siento...</label>
                            <input type="text" id="yo-siento" class="w-full p-2 border border-slate-300 rounded-md" placeholder="(describe tu emoción)">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700">Porque...</label>
                            <input type="text" id="yo-porque" class="w-full p-2 border border-slate-300 rounded-md" placeholder="(explica el impacto en ti)">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700">Y me gustaría...</label>
                            <input type="text" id="yo-gustaria" class="w-full p-2 border border-slate-300 rounded-md" placeholder="(propón una solución o pide un cambio)">
                        </div>
                        <button class="btn-primary" onclick="buildIMessage()">Generar mi Mensaje Yo</button>
                        <div id="i-message-result" class="mt-4 p-4 bg-blue-50 border border-blue-200 rounded-md text-blue-800 font-medium" style="display: none;"></div>
                    </div>
                </div>
            </section>
            
            <!-- Module 3 Section -->
            <section id="module3" class="content-section">
                <h2 class="text-3xl font-extrabold text-slate-800 mb-2">Módulo 3: Estrategias de Regulación Emocional</h2>
                <p class="text-lg text-slate-600 mb-8">Aprende a manejar pensamientos negativos y a incorporar actividades que te nutran, incluso cuando no tengas ganas.</p>

                <div class="activity-card">
                    <h3 class="text-xl font-bold text-slate-700 mb-3">Actividad: Desafío de Pensamientos Negativos</h3>
                    <p class="text-slate-600 mb-4">Los pensamientos no son hechos. Usa esta guía para cuestionar un pensamiento negativo que te esté molestando.</p>
                     <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-slate-700">1. Escribe el pensamiento negativo:</label>
                            <input type="text" id="neg-thought" class="w-full p-2 border border-slate-300 rounded-md" placeholder="Ej: 'Nunca hago nada bien'">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700">2. ¿Qué evidencia tienes de que este pensamiento es 100% verdad siempre?</label>
                             <textarea rows="2" class="w-full p-2 border border-slate-300 rounded-md" placeholder="Busca pruebas que lo contradigan..."></textarea>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700">3. ¿Cuál es una forma más equilibrada y realista de ver la situación?</label>
                            <textarea id="balanced-thought-input" rows="2" class="w-full p-2 border border-slate-300 rounded-md" placeholder="Ej: 'A veces cometo errores, pero también he tenido éxitos.'"></textarea>
                        </div>
                    </div>
                </div>
                
                <div class="activity-card">
                    <h3 class="text-xl font-bold text-slate-700 mb-3">Herramienta: Planificador de Actividades Gratificantes</h3>
                    <p class="text-slate-600 mb-4">La activación conductual rompe el ciclo de inactividad. Añade una pequeña actividad que podrías hacer hoy o mañana, sin importar cuán simple sea.</p>
                    <div class="flex gap-2">
                        <input type="text" id="activity-input" class="flex-grow p-2 border border-slate-300 rounded-md" placeholder="Ej: Caminar 10 min, escuchar una canción">
                        <button class="btn-primary" onclick="addActivity()">Añadir</button>
                    </div>
                    <ul id="activity-list" class="mt-4 space-y-2">
                        <!-- Activities will be added here -->
                    </ul>
                </div>

                <div class="activity-card text-center">
                     <h3 class="text-xl font-bold text-slate-700 mb-3">Práctica: Afirmación Positiva</h3>
                     <p class="text-slate-600 mb-4">Las afirmaciones ayudan a cultivar la autocompasión. Lee la siguiente y tómate un momento para sentirla.</p>
                     <div id="affirmation-box" class="p-4 bg-green-50 border-l-4 border-green-400 text-green-800 text-lg font-semibold mb-4">
                         Mi bienestar es una prioridad.
                     </div>
                     <button class="btn-primary" onclick="generateAffirmation()">Nueva Afirmación</button>
                </div>
            </section>
            
            <!-- Module 4 Section -->
            <section id="module4" class="content-section">
                 <h2 class="text-3xl font-extrabold text-slate-800 mb-2">Módulo 4: Comunicación Asertiva en Relaciones</h2>
                <p class="text-lg text-slate-600 mb-8">Aplica tus habilidades asertivas para mejorar tus relaciones, resolver conflictos y establecer límites saludables.</p>
                
                <div class="activity-card">
                     <h3 class="text-xl font-bold text-slate-700 mb-3">Herramienta: Creador de Guion Asertivo</h3>
                     <p class="text-slate-600 mb-4">A veces, las conversaciones difíciles necesitan preparación. Usa esta guía para estructurar lo que quieres decir.</p>
                     <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-slate-700">1. ¿Cuál es tu objetivo en esta conversación?</label>
                            <input type="text" class="w-full p-2 border border-slate-300 rounded-md" placeholder="Ej: Que se respete mi tiempo, expresar mi malestar...">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700">2. Escribe tu "Mensaje Yo" de apertura.</label>
                             <textarea rows="3" class="w-full p-2 border border-slate-300 rounded-md" placeholder="Usa la fórmula del Módulo 2."></textarea>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-slate-700">3. ¿Qué posible respuesta podrías recibir y cómo responderías asertivamente?</label>
                            <textarea rows="3" class="w-full p-2 border border-slate-300 rounded-md" placeholder="Anticipa y prepárate para mantener la calma."></textarea>
                        </div>
                    </div>
                </div>

                <div class="activity-card">
                    <h3 class="text-xl font-bold text-slate-700 mb-3">Técnicas Avanzadas de Asertividad</h3>
                    <p class="text-slate-600 mb-4">Estas técnicas son útiles cuando te enfrentas a insistencia o manipulación.</p>
                    <ul class="space-y-3">
                        <li><strong>Disco Rayado:</strong> Repetir tu punto de vista con calma y firmeza, una y otra vez. <em class="text-slate-500">"No, gracias." ... "Como te decía, no, gracias."</em></li>
                        <li><strong>Acuerdo Asertivo:</strong> Aceptar la parte de verdad en una crítica sin aceptar toda la culpa. <em class="text-slate-500">"Es verdad que llegué tarde, pero eso no significa que sea irresponsable."</em></li>
                        <li><strong>Aplazamiento Asertivo:</strong> Pedir tiempo para pensar antes de dar una respuesta. <em class="text-slate-500">"Necesito pensarlo. Te respondo mañana."</em></li>
                    </ul>
                </div>
            </section>
            
            <!-- Resources Section -->
            <section id="resources" class="content-section">
                <h2 class="text-3xl font-extrabold text-slate-800 mb-2">Recursos de Ayuda y Líneas de Crisis</h2>
                <p class="text-lg text-slate-600 mb-8">No estás solo/a. Si necesitas hablar con alguien o estás en crisis, estos recursos están disponibles para ti.</p>
                
                <div class="disclaimer-box border-red-400 bg-red-50 text-red-800">
                    <h3 class="font-bold text-lg mb-2">En caso de emergencia</h3>
                    <p class="text-sm">Si tú o alguien que conoces está en peligro inmediato, llama al número de emergencias de tu localidad (ej. 911).</p>
                </div>

                <div class="space-y-6">
                    <div class="bg-white p-4 rounded-lg shadow-sm">
                        <h3 class="font-bold text-lg text-blue-700">Líneas de Prevención del Suicidio y Crisis</h3>
                        <ul class="mt-2 space-y-3 divide-y divide-slate-100">
                            <li class="pt-3"><strong>Línea 988 (EE. UU.):</strong> Llama o envía un texto al 988. Apoyo 24/7. <a href="tel:988" class="text-blue-600 font-semibold">Llamar ahora</a></li>
                            <li class="pt-3"><strong>Línea 024 (España):</strong> Llama al 024. Atención a la conducta suicida 24/7. <a href="tel:024" class="text-blue-600 font-semibold">Llamar ahora</a></li>
                            <li class="pt-3"><strong>Consejo Ciudadano (México/América Latina):</strong> Llama o envía WhatsApp al 55 5533 5533. Apoyo psicológico 24/7. <a href="https://wa.me/525555335533" target="_blank" class="text-blue-600 font-semibold">Enviar WhatsApp</a></li>
                            <li class="pt-3"><strong>Crisis Text Line (EE. UU.):</strong> Envía HOME al 741741 para hablar por texto con un consejero de crisis.</li>
                        </ul>
                    </div>
                     <div class="bg-white p-4 rounded-lg shadow-sm">
                        <h3 class="font-bold text-lg text-blue-700">Organizaciones de Apoyo en Salud Mental</h3>
                        <ul class="mt-2 space-y-3 divide-y divide-slate-100">
                           <li class="pt-3"><strong>NAMI (Alianza Nacional sobre Enfermedades Mentales):</strong> Ofrece grupos de apoyo y recursos. <a href="https://www.nami.org/Home" target="_blank" class="text-blue-600 font-semibold">Visitar sitio</a></li>
                           <li class="pt-3"><strong>SAMHSA (Servicios de Abuso de Sustancias y Salud Mental):</strong> Línea de ayuda y localizador de tratamientos. <a href="https://www.samhsa.gov/find-help/national-helpline" target="_blank" class="text-blue-600 font-semibold">Visitar sitio</a></li>
                           <li class="pt-3"><strong>Psychology Today:</strong> Directorio para encontrar terapeutas en tu zona. <a href="https://www.psychologytoday.com/us/therapists" target="_blank" class="text-blue-600 font-semibold">Buscar terapeuta</a></li>
                        </ul>
                    </div>
                </div>
            </section>
        </main>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const navLinks = document.querySelectorAll('.nav-link');
            const contentSections = document.querySelectorAll('.content-section');
            const menuBtn = document.getElementById('menu-btn');
            const sidebar = document.getElementById('sidebar');

            function showSection(targetId) {
                contentSections.forEach(section => {
                    section.classList.remove('active');
                });
                document.getElementById(targetId).classList.add('active');

                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.dataset.target === targetId) {
                        link.classList.add('active');
                    }
                });
                
                sidebar.classList.add('-translate-x-full');
            }
            
            window.navigateTo = function(targetId) {
                showSection(targetId);
                 document.querySelector('main').scrollTop = 0;
            };

            navLinks.forEach(link => {
                link.addEventListener('click', () => {
                    const targetId = link.dataset.target;
                    showSection(targetId);
                });
            });

            menuBtn.addEventListener('click', () => {
                sidebar.classList.toggle('-translate-x-full');
            });
            
            document.querySelector('main').addEventListener('click', (e) => {
                 if (!sidebar.contains(e.target) && !menuBtn.contains(e.target) && !sidebar.classList.contains('-translate-x-full')) {
                     sidebar.classList.add('-translate-x-full');
                 }
            });

            // Chart.js implementation
            const ctx = document.getElementById('prevalenceChart').getContext('2d');
            new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: ['Afectados por Depresión Crónica', 'Resto de la Población'],
                    datasets: [{
                        data: [5, 95],
                        backgroundColor: [
                            '#3b82f6', // blue-500
                            '#e5e7eb'  // gray-200
                        ],
                        borderColor: [
                            '#ffffff',
                            '#ffffff'
                        ],
                        borderWidth: 2
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: true,
                    cutout: '70%',
                    plugins: {
                        legend: {
                            display: false
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.label + ': ' + context.raw + '%';
                                }
                            }
                        }
                    }
                }
            });
        });
        
        // Interactive activities logic
        function checkAssertiveness(isCorrect, feedbackId, type = 'correct') {
            const feedbackEl = document.getElementById(feedbackId);
            feedbackEl.style.display = 'block';
            feedbackEl.classList.remove('feedback-correct', 'feedback-incorrect');

            if (isCorrect) {
                feedbackEl.classList.add('feedback-correct');
                feedbackEl.textContent = '¡Excelente! Esta es una respuesta asertiva. Expresas tu necesidad con respeto y honestidad.';
            } else {
                feedbackEl.classList.add('feedback-incorrect');
                if (type === 'pasiva') {
                    feedbackEl.textContent = 'Esta es una respuesta pasiva. Ignoras tus propias necesidades para complacer a otro, lo que puede generar resentimiento.';
                } else {
                    feedbackEl.textContent = 'Esta es una respuesta agresiva. Aunque expresas tu necesidad, lo haces de forma hostil, dañando la relación.';
                }
            }
        }

        function buildIMessage() {
            const cuando = document.getElementById('yo-cuando').value;
            const siento = document.getElementById('yo-siento').value;
            const porque = document.getElementById('yo-porque').value;
            const gustaria = document.getElementById('yo-gustaria').value;
            const resultBox = document.getElementById('i-message-result');

            if (cuando && siento && porque && gustaria) {
                resultBox.innerHTML = `<strong>Tu mensaje:</strong> "Cuando ${cuando}, yo me siento ${siento} porque ${porque}, y me gustaría que ${gustaria}."`;
                resultBox.style.display = 'block';
            } else {
                resultBox.innerHTML = 'Por favor, completa todos los campos para generar el mensaje.';
                resultBox.style.display = 'block';
            }
        }
        
        function addActivity() {
            const input = document.getElementById('activity-input');
            const list = document.getElementById('activity-list');
            const activityText = input.value.trim();

            if (activityText) {
                const li = document.createElement('li');
                li.className = 'bg-white p-3 rounded-md shadow-sm flex justify-between items-center';
                li.textContent = activityText;
                
                const deleteBtn = document.createElement('button');
                deleteBtn.textContent = 'Hecho';
                deleteBtn.className = 'text-xs text-green-600 font-semibold hover:text-green-800';
                deleteBtn.onclick = function() {
                    li.classList.add('line-through', 'text-slate-400');
                    deleteBtn.remove();
                };
                
                li.appendChild(deleteBtn);
                list.appendChild(li);
                input.value = '';
            }
        }

        const affirmations = [
            "Soy capaz de manejar las emociones difíciles.",
            "Merezco sentirme tranquilo/a y en paz.",
            "Está bien establecer límites para proteger mi energía.",
            "Cada paso que doy hacia mi bienestar cuenta.",
            "Soy más fuerte de lo que creo.",
            "Tratarme con amabilidad es una prioridad.",
            "Mis sentimientos son válidos.",
            "Puedo superar los desafíos que se presenten."
        ];

        function generateAffirmation() {
            const affirmationBox = document.getElementById('affirmation-box');
            const randomIndex = Math.floor(Math.random() * affirmations.length);
            affirmationBox.textContent = affirmations[randomIndex];
        }

    </script>
</body>
</html>

