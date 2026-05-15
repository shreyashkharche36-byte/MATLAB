<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Conversion into Polar Form for Double Integration | Virtual Lab</title>
    
    <!-- Dependencies: Plotly.js for charts & MathJax for equations -->
    <script src="https://plot.ly"></script>
    <script>
        window.MathJax = {
            tex: { inlineMath: [['$', '$'], ['\\(', '\\)']] },
            svg: { fontCache: 'global' }
        };
    </script>
    <script id="MathJax-script" async src="https://jsdelivr.net"></script>

    <style>
        :root {
            --primary: #0056b3;
            --primary-hover: #004085;
            --bg-light: #f8f9fa;
            --text-dark: #333333;
            --sidebar-width: 280px;
            --card-shadow: 0 4px 6px rgba(0,0,0,0.05);
            --border-color: #e2e8f0;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', system-ui, sans-serif;
        }

        body {
            display: flex;
            background-color: var(--bg-light);
            color: var(--text-dark);
            height: 100vh;
            overflow: hidden;
        }

        /* Sidebar Navigation Layout */
        aside {
            width: var(--sidebar-width);
            background: #ffffff;
            border-right: 1px solid var(--border-color);
            display: flex;
            flex-direction: column;
            z-index: 10;
        }

        .lab-header {
            padding: 24px;
            font-size: 1rem;
            font-weight: 700;
            color: var(--primary);
            border-bottom: 1px solid var(--border-color);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            line-height: 1.4;
        }

        nav {
            flex: 1;
            overflow-y: auto;
            padding: 15px 0;
        }

        nav button {
            width: 100%;
            text-align: left;
            padding: 14px 24px;
            border: none;
            background: transparent;
            font-size: 0.95rem;
            color: #4a5568;
            cursor: pointer;
            display: flex;
            align-items: center;
            transition: all 0.2s ease;
        }

        nav button:hover {
            background: #f1f5f9;
            color: var(--primary);
        }

        nav button.active {
            background: #e8f0fe;
            color: var(--primary);
            font-weight: 600;
            border-left: 4px solid var(--primary);
        }

        /* Workspace Main Content Frame */
        main {
            flex: 1;
            display: flex;
            flex-direction: column;
            height: 100vh;
            overflow: hidden;
            position: relative;
        }

        .content-section {
            display: none;
            width: 100%;
            height: 100%;
            overflow-y: auto;
            padding: 40px;
        }

        .content-section.active {
            display: block;
        }

        /* UI Building Blocks & Visual Cards */
        h1 {
            color: #1a202c;
            margin-bottom: 15px;
            font-size: 2rem;
            font-weight: 700;
        }

        h2 {
            color: #2d3748;
            margin: 30px 0 15px 0;
            font-size: 1.35rem;
            border-bottom: 2px solid #edf2f7;
            padding-bottom: 8px;
        }

        p {
            line-height: 1.6;
            margin-bottom: 15px;
            color: #4a5568;
            font-size: 1rem;
        }

        ul {
            margin-left: 20px;
            margin-bottom: 20px;
            color: #4a5568;
        }

        li {
            margin-bottom: 8px;
            line-height: 1.5;
        }

        .card {
            background: white;
            border-radius: 8px;
            padding: 30px;
            margin-bottom: 25px;
            box-shadow: var(--card-shadow);
            border: 1px solid var(--border-color);
        }

        .btn {
            background: var(--primary);
            color: white;
            border: none;
            padding: 12px 28px;
            border-radius: 6px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            display: inline-block;
            transition: background 0.2s ease;
            text-decoration: none;
        }

        .btn:hover {
            background: var(--primary-hover);
        }

        .grid-2 {
            display: grid;
            grid-template-columns: 1.1fr 0.9fr;
            gap: 30px;
            align-items: start;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            font-size: 0.9rem;
            color: #4a5568;
        }

        select, input[type="range"] {
            width: 100%;
            padding: 10px;
            border: 1px solid #cbd5e1;
            border-radius: 6px;
            font-size: 1rem;
            background-color: #fff;
        }

        .math-block {
            background: #f8fafc;
            padding: 16px;
            border-radius: 6px;
            margin: 15px 0;
            border-left: 4px solid #94a3b8;
            overflow-x: auto;
        }

        .interactive-math-box {
            background: #f0fdf4;
            border-left-color: #22c55e;
        }

        /* Simulation Canvas styling */
        #plot-area {
            width: 100%;
            height: 480px;
            background: #ffffff;
            border-radius: 8px;
            border: 1px solid var(--border-color);
            box-shadow: var(--card-shadow);
        }

        /* Assessment Quiz components */
        .quiz-option {
            display: flex;
            align-items: center;
            background: #f8fafc;
            border: 1px solid var(--border-color);
            padding: 14px 18px;
            margin-bottom: 12px;
            border-radius: 6px;
            cursor: pointer;
            transition: background 0.2s ease;
        }

        .quiz-option:hover {
            background: #f1f5f9;
        }

        .quiz-option input {
            margin-right: 12px;
            transform: scale(1.1);
        }

        #quiz-feedback {
            margin-top: 15px;
            font-weight: 600;
            padding: 12px;
            border-radius: 6px;
            display: none;
        }
    </style>
</head>
<body>

    <!-- Sidebar Menu Component -->
    <aside>
        <div class="lab-header">IIIT Hyderabad Style<br><span style="font-size:0.85rem; font-weight:400; color:#64748b;">Virtual Aerospace Math Lab</span></div>
        <nav>
            <button onclick="showSection('home')" id="nav-home" class="active">🏠 Home</button>
            <button onclick="showSection('aim')" id="nav-aim">🎯 Aim</button>
            <button onclick="showSection('theory')" id="nav-theory">📖 Theory</button>
            <button onclick="showSection('procedure')" id="nav-procedure">📋 Procedure</button>
            <button onclick="showSection('simulation')" id="nav-simulation">🧪 Interactive Simulation</button>
            <button onclick="showSection('examples')" id="nav-examples">📝 Worked Examples</button>
            <button onclick="showSection('quiz')" id="nav-quiz">✏️ Quiz Assessment</button>
            <button onclick="showSection('references')" id="nav-references">📚 References</button>
        </nav>
    </aside>

    <!-- Content Workspace -->
    <main>
        
        <!-- Home Landing View -->
        <section id="home" class="content-section active">
            <div class="card" style="text-align: center; padding: 80px 40px; margin-top: 40px;">
                <h1>Conversion into Polar Form for Application of Double Integration</h1>
                <p style="font-size: 1.15rem; max-width: 750px; margin: 20px auto 35px auto;">
                    Learn how complex Cartesian tracking frameworks are mapped smoothly into Polar coordinate domains to solve intricate planar area and volume integration topologies efficiently.
                </p>
                <div style="gap: 15px; display: inline-flex; justify-content: center;">
                    <button class="btn" onclick="showSection('simulation')">Launch Lab Simulation</button>
                    <button class="btn" style="background:#475569;" onclick="showSection('theory')">Explore Core Theory</button>
                </div>
            </div>
        </section>

        <!-- Aim Module -->
        <section id="aim" class="content-section">
            <div class="card">
                <h1>Experimental Aim</h1>
                <p>To mathematically analyze and computationally evaluate the change of variables in double integration from Cartesian coordinates $(x, y)$ to Polar coordinates $(r, \theta)$.</p>
                <h2>Lab Learning Objectives</h2>
                <ul>
                    <li>Understand the structural bounds where Cartesian evaluation fails or becomes analytically inefficient.</li>
                    <li>Master structural transformations using trigonometric vector identity substitutions.</li>
                    <li>Visualize dynamic integration constraints using active polar graphing instruments.</li>
                </ul>
            </div>
        </section>

        <!-- Academic Theory View -->
        <section id="theory" class="content-section">
            <div class="card">
                <h1>Mathematical Background</h1>
                <p>Evaluating integrals inside circular boundary areas or curves featuring radial symmetry becomes complicated under regular Cartesian configurations ($dx\,dy$) due to radical variables ($\sqrt{a^2-x^2}$). Changing coordinates bypasses these processing blocks completely.</p>
                
                <h2>Coordinate Conversions</h2>
                <p>Standard transformation equations derived using basic vector triangles:</p>
                <div class="math-block">$$x = r \cos(\theta)$$</div>
                <div class="math-block">$$y = r \sin(\theta)$$</div>
                <div class="math-block">$$x^2 + y^2 = r^2$$</div>

                <h2>Active Coordinate Parameter Modeler</h2>
                <p style="font-style: italic;">Adjust the sliders below to see standard conversion points change instantly:</p>
                <div class="form-group" style="max-width: 400px; padding: 10px 0;">
                    <label for="theory-theta">Angle Matrix Bound ($\theta$): <span id="theory-theta-val">45</span>°</label>
                    <input type="range" id="theory-theta" min="0" max="360" step="15" value="45" oninput="runTheoryMathEngine()">
                </div>
                
                <div class="math-block interactive-math-box">
                    <div id="calc-x">$$x = r \cos(\theta) \implies x = 1 \cdot \cos(45^\circ) = 0.71$$</div>
                    <div id="calc-y" style="margin-top:10px;">$$y = r \sin(\theta) \implies y = 1 \cdot \sin(45^\circ) = 0.71$$</div>
                    <div id="calc-sq" style="margin-top:10px;">$$x^2 + y^2 = r^2 \implies 0.71^2 + 0.71^2 = 1.00$$</div>
                </div>

                <h2>Double Integration Mapping Framework</h2>
                <p>To safely switch tracking metrics, we apply the scaling Jacobian factor modifier to track space expansion changes accurately ($dA = dx\,dy = r\,dr\,d\theta$):</p>
                <div class="math-block">$$A = \iint_R dx\,dy = \int_{\alpha}^{\beta} \int_{g_1(\theta)}^{g_2(\theta)} r \, dr \, d\theta$$</div>
            </div>
        </section>

        <!-- Procedure Guide -->
        <section id="procedure" class="content-section">
            <div class="card">
                <h1>Execution Procedure</h1>
                <h2>Algorithmic Evaluation Steps</h2>
                <p><b>Step 1:</b> Sketch and map the original coordinate boundary geometry tracking loops inside the graph grid space.</p>
                <p><b>Step 2:</b> Substitute $x = r\cos\theta$ and $y = r\sin\theta$ into boundary definitions to find explicit function constraints for the variable radius $r$.</p>
                <p><b>Step 3:</b> Track radial sweep boundaries across coordinate quadrants to determine the constant evaluation bounds for angular vector $\theta$.</p>
                <p><b>Step 4:</b> Assemble your double integral template workspace. Ensure you write the tracking differential strictly as $r \, dr \, d\theta$.</p>
            </div>
        </section>

        <!-- Interactive Lab Simulation View -->
        <section id="simulation" class="content-section">
            <h1>Interactive Integration Canvas</h1>
            <div class="grid-2">
                <!-- Simulation Control Panel Box -->
                <div class="card">
                    <h2>Geometric Boundaries</h2>
                    
                    <div class="form-group">
                        <label for="geom-profile">Select Coordinate Target Boundary</label>
                        <select id="geom-profile" onchange="runSimulationEngine()">
                            <option value="circle">Standard Circle Configuration (x² + y² = R²)</option>
                            <option value="cardioid">Cardioid Vector Wave (r = a(1 + cosθ))</option>
                            <option value="rose">Trigonometric Rose Curve (r = a · cos(3θ))</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label for="radius-scalar">Boundary Scalar Modifer ($a$ or $R$): <span id="radius-val">3</span></label>
                        <input type="range" id="radius-scalar" min="1" max="5" step="0.5" value="3" oninput="runSimulationEngine()">
                    </div>

                    <h2>Mathematical Translation Output</h2>
                    <p><b>Target Equation in Polar Form:</b></p>
                    <div id="sim-polar-equation" class="math-block">r = 3</div>
                    
                    <p><b>Resulting Integration Structural Workspace:</b></p>
                    <div id="sim-integral" class="math-block">$$\int_{0}^{2\pi} \int_{0}^{3} r \, dr \, d\theta$$</div>
                    
                    <p><b>Evaluated Area Calculation:</b></p>
                    <div id="sim-area" class="math-block" style="background: #eff6ff; color: #1d4ed8; font-weight: 700; border-left-color: #3b82f6;">Area = 28.27 units²</div>
                </div>

                <!-- Simulation Visualizing Plot Canvas Container -->
                <div>
                    <div id="plot-area"></div>
                </div>
            </div>
        </section>

        <!-- Worked Examples Module -->
        <section id="examples" class="content-section">
            <div class="card">
                <h1>Structured Worked Problems</h1>
                
                <h2>Example 1: Circle Enclosure Area Evaluation</h2>
                <p>Find the area wrapped inside the circular coordinate perimeter ring given by $x^2 + y^2 = 4$.</p>
                <div class="math-block"><b>Polar Mapping Transformation:</b> $r^2 = 4 \implies r = 2$</div>
                <div class="math-block"><b>Constructed Matrix Integral:</b> $$A = \int_{0}^{2\pi} \int_{0}^{2} r \, dr \, d\theta = \int_{0}^{2\pi} \left[ \frac{r^2}{2} \right]_{0}^{2} d\theta = \int_{0}^{2\pi} 2 \, d\theta = 4\pi \approx 12.57$$</div>

                <h2>Example 2: Cardioid Profile Space Calculation</h2>
                <p>Find the region area mapped by the curve profile equation: $r = 1 + \cos\theta$.</p>
                <div class="math-block"><b>Constructed Integrals Frame:</b> $$A = \int_{0}^{2\pi} \int_{0}^{1+\cos\theta} r \, dr \, d\theta = \int_{0}^{2\pi} \frac{(1+\cos\theta)^2}{2} \, d\theta = \frac{3\pi}{2}$$</div>
            </div>
        </section>

        <!-- Assessment Quiz View -->
        <section id="quiz" class="content-section">
            <div class="card">
                <h1>Assessment Quiz</h1>
                <p>Test your knowledge on coordinate conversions for double integration workflows.</p>
                
                <div id="quiz-workspace" style="margin-top: 25px;">
                    <div class="form-group">
                        <p><b>Question 1:</b> What is the correct differential scaling factor value (Jacobian matrix value) used when migrating Cartesian double integrals to Polar space targets ($dx\,dy \to \mathbf{?} \, dr\,d\theta$)?</p>
                        <label class="quiz-option"><input type="radio" name="q1" value="incorrect"> $1$</label>
                        <label class="quiz-option"><input type="radio" name="q1" value="correct"> $r$</label>
                        <label class="quiz-option"><input type="radio" name="q1" value="incorrect"> $r^2$</label>
                        <label class="quiz-option"><input type="radio" name="q1" value="incorrect"> $r \sin\theta$</label>
                    </div>
                    
                    <button class="btn" onclick="gradeQuizEngine()">Submit Answers</button>
                    <div id="quiz-feedback"></div>
                </div>
            </div>
        </section>

        <!-- References Module -->
        <section id="references" class="content-section">
            <div class="card">
                <h1>Academic References & Open Education Resources</h1>
                <ul style="list-style-type: none; margin-left: 0;">
                    <li style="margin-bottom: 15px;">🔗 <a href="https://mit.edu" target="_blank" style="color:var(--primary); font-weight: 600;">MIT OpenCourseWare: Multivariable Calculus Systems</a></li>
                    <li style="margin-bottom: 15px;">🔗 <a href="https://lamar.edu" target="_blank" style="color:var(--primary); font-weight: 600;">Paul's Online Math Notes: Polar Integrals Workspace</a></li>
                    <li style="margin-bottom: 15px;">🔗 <a href="https://desmos.com" target="_blank" style="color:var(--primary); font-weight: 600;">Desmos Graphing Calculator Engine</a></li>
                </ul>
            </div>
        </section>

    </main>

    <!-- Core Interactive Client Logic Script -->
    <script>
        // Tab Page Switcher Navigation Routing Engine
        function showSection(sectionId) {
            document.querySelectorAll('.content-section').forEach(section => section.classList.remove('active'));
            document.querySelectorAll('nav button').forEach(btn => btn.classList.remove('active'));
            
            document.getElementById(sectionId).classList.add('active');
            document.getElementById('nav-' + sectionId).classList.add('active');

            if (sectionId === 'simulation') {
                // Short buffer time ensures Plotly sizes correctly inside fully initialized containers
                setTimeout(runSimulationEngine, 60);
            }
        }

        // Live Coordinate Formula Transformation Modeler logic
        function runTheoryMathEngine() {
            const degrees = parseFloat(document.getElementById('theory-theta').value);
            document.getElementById('theory-theta-val').innerText = degrees;
            
            const rads = degrees * (Math.PI / 180);
            const computedX = (1 * Math.cos(rads)).toFixed(2);
            const computedY = (1 * Math.sin(rads)).toFixed(2);
            const computedSumSq = (Math.pow(computedX, 2) + Math.pow(computedY, 2)).toFixed(2);

            document.getElementById('calc-x').innerHTML = `$$x = r \\cos(\\theta) \\implies x = 1 \\cdot \\cos(${degrees}^\\circ) = ${computedX}$$`;
            document.getElementById('calc-y').innerHTML = `$$y = r \\sin(\\theta) \\implies y = 1 \\cdot \\sin(${degrees}^\\circ) = ${computedY}$$`;
            document.getElementById('calc-sq').innerHTML = `$$x^2 + y^2 = r^2 \\implies (${computedX})^2 + (${computedY})^2 = ${computedSumSq}$$`;

            if (window.MathJax && window.MathJax.typesetPromise) {
                MathJax.typesetPromise();
            }
        }

        // Live Simulation Rendering Graph Tool
        function runSimulationEngine() {
            const profile = document.getElementById('geom-profile').value;
            const scalar = parseFloat(document.getElementById('radius-scalar').value);
            document.getElementById('radius-val').innerText = scalar;

            let eqText = "";
            let integralText = "";
            let finalArea = 0;

            let thetaValues = [];
            let rValues = [];

            // Calculate loop plot matrix limits
            for (let idx = 0; idx <= 200; idx++) {
                let th = (idx / 200) * 2 * Math.PI;
                thetaValues.push(th);
                
                if (profile === 'circle') {
                    rValues.push(scalar);
                } else if (profile === 'cardioid') {
                    rValues.push(scalar * (1 + Math.cos(th)));
                } else if (profile === 'rose') {
                    rValues.push(scalar * Math.cos(3 * th));
                }
            }

            // Math formatting configs
            if (profile === 'circle') {
                eqText = `r = ${scalar}`;
                integralText = `$$\\int_{0}^{2\\pi} \\int_{0}^{${scalar}} r \\, dr \\, d\\theta$$`;
                finalArea = Math.PI * Math.pow(scalar, 2);
            } else if (profile === 'cardioid') {
                eqText = `r = ${scalar}(1 + \\cos\\theta)`;
                integralText = `$$\\int_{0}^{2\\pi} \\int_{0}^{${scalar}(1+\\cos\\theta)} r \\, dr \\, d\\theta$$`;
                finalArea = 1.5 * Math.PI * Math.pow(scalar, 2);
            } else if (profile === 'rose') {
                eqText = `r = ${scalar}\\cos(3\\theta)`;
                integralText = `$$\\int_{0}^{2\\pi} \\int_{0}^{${scalar}\\cos(3\\theta)} r \\, dr \\, d\\theta$$`;
                finalArea = (Math.PI * Math.pow(scalar, 2)) / 4; 
            }

            document.getElementById('sim-polar-equation').innerHTML = eqText;
            document.getElementById('sim-integral').innerHTML = integralText;
            document.getElementById('sim-area').innerText = `Calculated Target Area = ${finalArea.toFixed(2)} units²`;

            if (window.MathJax && window.MathJax.typesetPromise) {
                MathJax.typesetPromise();
            }

            // Map and plot trace parameters using Plotly vector models
            const tracer = [{
                r: rValues,
                t: thetaValues.map(v => v * (180 / Math.PI)), // Map angles back to standard layout values
                type: 'scatterpolar',
                mode: 'lines',
                name: 'Boundary Profile Map',
                line: { color: '#0056b3', width: 3 },
                fill: 'toself',
                fillcolor: 'rgba(0, 86, 179, 0.1)'
            }];

            const structuralLayout = {
                title: 'Polar System Transformation Graph Workspace',
                font: { family: 'Segoe UI, sans-serif' },
                polar: {
                    radialaxis: { visible: true, range: [0, profile === 'cardioid' ? scalar * 2 : scalar] }
                },
                margin: { t: 50, b: 30, l: 30, r: 30 }
            };

            Plotly.newPlot('plot-area', tracer, structuralLayout, {responsive: true});
        }

        // Quiz Evaluation Grading Logic Module
        function gradeQuizEngine() {
            const userPick = document.querySelector('input[name="q1"]:checked');
            const boxFeedback = document.getElementById('quiz-feedback');
            
            boxFeedback.style.display = "block";

            if (!userPick) {
                boxFeedback.style.background = "#fee2e2";
                boxFeedback.style.color = "#991b1b";
                boxFeedback.innerText = "Please pick an option before submitting.";
                return;
            }

            if (userPick.value === "correct") {
                boxFeedback.style.background = "#dcfce7";
                boxFeedback.style.color = "#166534";
                boxFeedback.innerText = "Correct! The structural Jacobian transformation multiplier parameter is strictly 'r'.";
            } else {
                boxFeedback.style.background = "#fee2e2";
                boxFeedback.style.color = "#991b1b";
                boxFeedback.innerText = "Incorrect answer. Remember that switching parameters requires area scaling adjustments using the Jacobian factor.";
            }
        }
    </script>
</body>
</html>
