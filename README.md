<!DOCTYPE html>
<html lang="en">

<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>

<title>Virtual Aerospace Mathematics Lab</title>

<!-- Plotly -->
<script src="https://cdn.plot.ly/plotly-2.35.2.min.js"></script>

<!-- MathJax -->
<script>
window.MathJax = {
    tex: {
        inlineMath: [['$', '$'], ['\\(', '\\)']]
    },
    svg: {
        fontCache: 'global'
    }
};
</script>

<script async
src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

<!-- Google Font -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">

<style>

:root{
    --primary:#2563eb;
    --primary-dark:#1d4ed8;
    --accent:#06b6d4;

    --bg:#f4f7fb;
    --card:#ffffff;
    --sidebar:#0f172a;

    --text:#0f172a;
    --muted:#64748b;

    --border:#e2e8f0;

    --shadow:
        0 10px 30px rgba(15,23,42,0.08);

    --radius:18px;

    --sidebar-width:300px;
}

.dark-mode{
    --bg:#020617;
    --card:#0f172a;
    --text:#f8fafc;
    --muted:#94a3b8;
    --border:#1e293b;
}

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:'Inter',sans-serif;
}

body{
    display:flex;
    height:100vh;
    overflow:hidden;
    background:var(--bg);
    color:var(--text);
}

/* Sidebar */

aside{
    width:var(--sidebar-width);

    background:linear-gradient(
        180deg,
        #0f172a 0%,
        #111827 100%
    );

    color:white;

    display:flex;
    flex-direction:column;

    border-right:1px solid rgba(255,255,255,0.08);
}

.lab-header{
    padding:32px 24px;
    border-bottom:1px solid rgba(255,255,255,0.08);
}

.lab-header h2{
    font-size:1.2rem;
    font-weight:800;
    line-height:1.4;
}

.lab-header p{
    margin-top:10px;
    color:#94a3b8;
    font-size:0.9rem;
}

nav{
    padding:20px 12px;
    overflow-y:auto;
    flex:1;
}

nav button{
    width:100%;
    border:none;
    background:transparent;

    color:#cbd5e1;

    padding:14px 18px;
    margin-bottom:8px;

    border-radius:12px;

    text-align:left;

    font-size:0.96rem;
    font-weight:500;

    cursor:pointer;

    transition:all 0.25s ease;
}

nav button:hover{
    background:rgba(255,255,255,0.08);
    color:white;
    transform:translateX(4px);
}

nav button.active{
    background:linear-gradient(
        90deg,
        rgba(37,99,235,0.25),
        rgba(6,182,212,0.15)
    );

    color:white;

    border:1px solid rgba(255,255,255,0.08);
}

#theme-toggle{
    margin:18px;
    border:none;
    padding:14px;
    border-radius:12px;
    background:#1e293b;
    color:white;
    cursor:pointer;
    font-weight:600;
}

/* Main */

main{
    flex:1;
    overflow:hidden;
    position:relative;
}

.content-section{
    display:none;
    height:100vh;
    overflow-y:auto;

    padding:42px;

    animation:fadeIn 0.35s ease;
}

.content-section.active{
    display:block;
}

@keyframes fadeIn{
    from{
        opacity:0;
        transform:translateY(12px);
    }
    to{
        opacity:1;
        transform:translateY(0);
    }
}

/* Cards */

.card{
    background:var(--card);

    border-radius:var(--radius);

    padding:34px;

    margin-bottom:28px;

    box-shadow:var(--shadow);

    border:1px solid var(--border);
}

/* Hero */

.hero-card{
    min-height:78vh;

    display:flex;
    flex-direction:column;
    justify-content:center;

    background:
    radial-gradient(
        circle at top right,
        rgba(37,99,235,0.12),
        transparent 40%
    ),
    white;
}

/* Ensure Hero Card updates in Dark Mode */
.dark-mode .hero-card {
    background: 
        radial-gradient(
            circle at top right,
            rgba(37, 99, 235, 0.2),
            transparent 40%
        ),
        var(--card); /* Uses the dark-mode card color instead of white */
}

/* Ensure the title and badge remain high-contrast */
.dark-mode .hero-card h1 {
    color: var(--text);
}

.dark-mode .hero-badge {
    background: rgba(37, 99, 235, 0.3); /* Slightly darker blue for dark mode */
    color: #60a5fa; /* Lighter blue for readability */
}
    
.hero-badge{
    width:max-content;

    padding:10px 18px;

    border-radius:999px;

    background:#dbeafe;

    color:#1d4ed8;

    font-size:0.88rem;
    font-weight:700;

    margin-bottom:24px;
}

.hero-actions{
    display:flex;
    gap:16px;
    margin-top:30px;
}

.secondary-btn{
    background:#0f172a !important;
}

/* Typography */

h1{
    font-size:2.4rem;
    font-weight:800;
    margin-bottom:18px;
    line-height:1.2;
}

h2{
    margin-top:28px;
    margin-bottom:14px;

    font-size:1.35rem;
    font-weight:700;
}

p{
    color:var(--muted);
    line-height:1.8;
    font-size:1rem;
}

ul{
    margin-left:20px;
    margin-top:12px;
}

li{
    margin-bottom:10px;
    color:var(--muted);
    line-height:1.7;
}

/* Buttons */

.btn{
    border:none;

    background:linear-gradient(
        135deg,
        var(--primary),
        var(--accent)
    );

    color:white;

    padding:14px 28px;

    border-radius:14px;

    font-weight:700;
    font-size:0.96rem;

    cursor:pointer;

    transition:all 0.25s ease;
}

.btn:hover{
    transform:translateY(-2px);
    box-shadow:
        0 10px 24px rgba(37,99,235,0.22);
}

/* Form */

.form-group{
    margin-bottom:24px;
}

label{
    display:block;
    margin-bottom:10px;
    font-weight:600;
}

select,
input[type="range"]{
    width:100%;
    padding:12px;
    border-radius:12px;
    border:1px solid var(--border);
    background:white;
}

/* Math Blocks */

.math-block{
    background:#f8fafc;

    border:1px solid #e2e8f0;

    border-left:5px solid var(--primary);

    border-radius:12px;

    padding:18px;

    margin:18px 0;

    overflow-x:auto;
}

/* Grid */

.grid-2{
    display:grid;
    grid-template-columns:1.1fr 0.9fr;
    gap:28px;
}

/* Plot */

#plot-area{
    width:100%;
    height:580px;

    border-radius:20px;

    overflow:hidden;

    background:white;

    border:1px solid var(--border);

    box-shadow:var(--shadow);
}

/* Quiz */

.quiz-option{
    display:flex;
    align-items:center;

    padding:14px;
    border-radius:12px;

    border:1px solid var(--border);

    margin-bottom:12px;

    cursor:pointer;

    transition:0.2s;
}

.quiz-option:hover{
    background:#f8fafc;
}

.quiz-option input{
    margin-right:12px;
}

/* Responsive */

@media(max-width:950px){

    body{
        flex-direction:column;
        overflow:auto;
    }

    aside{
        width:100%;
        height:auto;
    }

    main{
        height:auto;
    }

    .content-section{
        height:auto;
        padding:22px;
    }

    .grid-2{
        grid-template-columns:1fr;
    }

    .hero-actions{
        flex-direction:column;
    }
}
/* Force MathJax to inherit the text color from the theme */
.dark-mode .math-block,
.dark-mode mjx-container {
    color: var(--text) !important;
}

/* Optional: Adjust the background of math blocks for better contrast in dark mode */
.dark-mode .math-block {
    background: #1e293b; /* Darker slate background */
    border-color: #334155;
    border-left-color: var(--accent); /* Uses your cyan accent for the left border */
}

</style>
</head>

<body>

<!-- Sidebar -->

<aside>

    <div class="lab-header">
        <h2>IIIT Hyderabad Style<br>Virtual Aerospace Math Lab</h2>
        <p>Interactive Polar Integration Environment</p>
    </div>

    <nav>

        <button onclick="showSection('home')" id="nav-home" class="active">
            🏠 Home
        </button>

        <button onclick="showSection('aim')" id="nav-aim">
            🎯 Aim
        </button>

        <button onclick="showSection('theory')" id="nav-theory">
            📖 Theory
        </button>

        <button onclick="showSection('procedure')" id="nav-procedure">
            📋 Procedure
        </button>

        <button onclick="showSection('simulation')" id="nav-simulation">
            🧪 Simulation
        </button>

        <button onclick="showSection('examples')" id="nav-examples">
            📝 Examples
        </button>

        <button onclick="showSection('quiz')" id="nav-quiz">
            ✏️ Quiz
        </button>

        <button onclick="showSection('references')" id="nav-references">
            📚 References
        </button>

    </nav>

    <button id="theme-toggle">
        🌙 Toggle Theme
    </button>

</aside>

<!-- Main -->

<main>

<!-- HOME -->

<section id="home" class="content-section active">

    <div class="card hero-card">

        <div class="hero-badge">
            Aerospace Mathematics Laboratory
        </div>

        <h1>
            Conversion into Polar Form for Double Integration
        </h1>

        <p>
            Explore coordinate transformations, Jacobian mappings,
            and interactive polar integration systems using advanced
            mathematical visualization tools.
        </p>

        <div class="hero-actions">

            <button class="btn"
            onclick="showSection('simulation')">
                Launch Simulation
            </button>

            <button class="btn secondary-btn"
            onclick="showSection('theory')">
                Explore Theory
            </button>

        </div>

    </div>

</section>

<!-- AIM -->

<section id="aim" class="content-section">

<div class="card">

<h1>Experimental Aim</h1>

<p>
To mathematically analyze and computationally evaluate
the transformation from Cartesian coordinates
$(x,y)$ into Polar coordinates $(r,\theta)$
for applications in double integration.
</p>

<h2>Objectives</h2>

<ul>
<li>Understand coordinate transformation systems.</li>
<li>Visualize Jacobian area scaling.</li>
<li>Evaluate integrals using polar limits.</li>
<li>Study circular and symmetric regions efficiently.</li>
</ul>

</div>

</section>

<!-- THEORY -->

<section id="theory" class="content-section">

<div class="card">

<h1>Mathematical Theory</h1>

<p>
Polar coordinates simplify integrations involving
radial symmetry and circular boundaries.
</p>

<h2>Coordinate Transformations</h2>

<div class="math-block">
$$x = r\cos\theta$$
</div>

<div class="math-block">
$$y = r\sin\theta$$
</div>

<div class="math-block">
$$x^2+y^2=r^2$$
</div>

<h2>Jacobian Transformation</h2>

<div class="math-block">
$$
\frac{\partial(x,y)}{\partial(r,\theta)}
=
\begin{vmatrix}
\cos\theta & -r\sin\theta \\
\sin\theta & r\cos\theta
\end{vmatrix}
=
r
$$
</div>

<p>
Therefore:
</p>

<div class="math-block">
$$dx\,dy = r\,dr\,d\theta$$
</div>

<h2>Interactive Coordinate Model</h2>

<div class="form-group">

<label>
Angle θ:
<span id="theory-theta-val">45</span>°
</label>

<input
type="range"
id="theory-theta"
min="0"
max="360"
step="15"
value="45"
oninput="runTheoryMathEngine()">

</div>

<div class="math-block" id="calc-x">
$$x = 0.71$$
</div>

<div class="math-block" id="calc-y">
$$y = 0.71$$
</div>

<div class="math-block" id="calc-sq">
$$x^2+y^2 = 1$$
</div>

</div>

</section>

<!-- PROCEDURE -->

<section id="procedure" class="content-section">

<div class="card">

<h1>Procedure</h1>

<h2>Stepwise Method</h2>

<ul>
<li>Sketch the given region.</li>
<li>Convert Cartesian equations into polar form.</li>
<li>Determine limits of r and θ.</li>
<li>Replace differential element with $rdrd\theta$.</li>
<li>Evaluate the integral.</li>
</ul>

</div>

</section>

<!-- SIMULATION -->

<section id="simulation" class="content-section">

<h1>Interactive Polar Simulation</h1>

<div class="grid-2">

<div class="card">

<h2>Boundary Configuration</h2>

<div class="form-group">

<label>Select Profile</label>

<select id="geom-profile"
onchange="runSimulationEngine()">

<option value="circle">
Circle
</option>

<option value="cardioid">
Cardioid
</option>

<option value="rose">
Rose Curve
</option>

</select>

</div>

<div class="form-group">

<label>
Scale Parameter:
<span id="radius-val">3</span>
</label>

<input
type="range"
id="radius-scalar"
min="1"
max="5"
step="0.5"
value="3"
oninput="runSimulationEngine()">

</div>

<h2>Polar Equation</h2>

<div id="sim-polar-equation"
class="math-block">
$$r=3$$
</div>

<h2>Integral</h2>

<div id="sim-integral"
class="math-block">
$$
\int_0^{2\pi}\int_0^3 r\,dr\,d\theta
$$
</div>

<h2>Calculated Area</h2>

<div id="sim-area"
class="math-block">
Area = 28.27 units²
</div>

</div>

<div>

<div id="plot-area"></div>

</div>

</div>

</section>

<!-- EXAMPLES -->

<section id="examples" class="content-section">

<div class="card">

<h1>Worked Examples</h1>

<h2>Example 1</h2>

<p>
Find the area inside:
</p>

<div class="math-block">
$$x^2+y^2=4$$
</div>

<div class="math-block">
$$
A=
\int_0^{2\pi}
\int_0^2
rdrd\theta
=
4\pi
$$
</div>

<h2>Example 2</h2>

<div class="math-block">
$$r=1+\cos\theta$$
</div>

<div class="math-block">
$$
A=
\frac{3\pi}{2}
$$
</div>

</div>

</section>

<!-- QUIZ -->

<section id="quiz" class="content-section">

<div class="card">

<h1>Quiz Assessment</h1>

<p>
What is the Jacobian scaling factor in polar coordinates?
</p>

<label class="quiz-option">
<input type="radio" name="q1" value="incorrect">
1
</label>

<label class="quiz-option">
<input type="radio" name="q1" value="correct">
r
</label>

<label class="quiz-option">
<input type="radio" name="q1" value="incorrect">
r²
</label>

<label class="quiz-option">
<input type="radio" name="q1" value="incorrect">
sinθ
</label>

<button class="btn"
onclick="gradeQuizEngine()">
Submit
</button>

<div id="quiz-feedback"
style="margin-top:20px;"></div>

</div>

</section>

<!-- REFERENCES -->

<section id="references" class="content-section">

<div class="card">

<h1>References</h1>

<ul>

<li>
MIT OpenCourseWare — Multivariable Calculus
</li>

<li>
Paul's Online Math Notes — Polar Coordinates
</li>

<li>
Desmos Graphing Calculator
</li>

</ul>

</div>

</section>

</main>

<!-- SCRIPT -->

<script>

/* Navigation */

function showSection(sectionId){

    document
    .querySelectorAll('.content-section')
    .forEach(section=>{
        section.classList.remove('active');
    });

    document
    .querySelectorAll('nav button')
    .forEach(btn=>{
        btn.classList.remove('active');
    });

    document
    .getElementById(sectionId)
    .classList.add('active');

    document
    .getElementById('nav-'+sectionId)
    .classList.add('active');

    if(sectionId==='simulation'){
        setTimeout(runSimulationEngine,60);
    }
}

/* Dark Mode */

document.getElementById('theme-toggle')
.addEventListener('click',()=>{

    document.body.classList.toggle('dark-mode');

});

/* Theory Calculator */

function runTheoryMathEngine(){

    const degrees =
    parseFloat(
        document.getElementById('theory-theta').value
    );

    document
    .getElementById('theory-theta-val')
    .innerText=degrees;

    const rads =
    degrees*(Math.PI/180);

    const x =
    Math.cos(rads).toFixed(2);

    const y =
    Math.sin(rads).toFixed(2);

    const sq =
    (
        Math.pow(x,2)+
        Math.pow(y,2)
    ).toFixed(2);

    document.getElementById('calc-x')
    .innerHTML=
    `$$x = ${x}$$`;

    document.getElementById('calc-y')
    .innerHTML=
    `$$y = ${y}$$`;

    document.getElementById('calc-sq')
    .innerHTML=
    `$$x^2+y^2 = ${sq}$$`;

    if(window.MathJax){
        MathJax.typesetPromise();
    }
}

/* Simulation */

function runSimulationEngine(){

    const profile =
    document.getElementById('geom-profile').value;

    const scalar =
    parseFloat(
        document.getElementById('radius-scalar').value
    );

    document
    .getElementById('radius-val')
    .innerText=scalar;

    let thetaValues=[];
    let rValues=[];

    for(let i=0;i<=400;i++){

        let th=
        (i/400)*2*Math.PI;

        thetaValues.push(th);

        if(profile==='circle'){
            rValues.push(scalar);
        }

        else if(profile==='cardioid'){
            rValues.push(
                scalar*(1+Math.cos(th))
            );
        }

        else{
            rValues.push(
                scalar*Math.cos(3*th)
            );
        }
    }

    let eqText="";
    let integralText="";
    let area=0;

    if(profile==='circle'){

        eqText=`$$r=${scalar}$$`;

        integralText=
        `$$
        \\int_0^{2\\pi}
        \\int_0^{${scalar}}
        rdrd\\theta
        $$`;

        area=
        Math.PI*Math.pow(scalar,2);
    }

    else if(profile==='cardioid'){

        eqText=
        `$$r=${scalar}(1+\\cos\\theta)$$`;

        integralText=
        `$$
        \\int_0^{2\\pi}
        \\int_0^{
        ${scalar}(1+\\cos\\theta)
        }
        rdrd\\theta
        $$`;

        area=
        1.5*Math.PI*Math.pow(scalar,2);
    }

    else{

        eqText=
        `$$r=${scalar}\\cos(3\\theta)$$`;

        integralText=
        `$$
        \\int_0^{2\\pi}
        \\int_0^{
        ${scalar}\\cos(3\\theta)
        }
        rdrd\\theta
        $$`;

        area=
        (Math.PI*Math.pow(scalar,2))/2;
    }

    document
    .getElementById('sim-polar-equation')
    .innerHTML=eqText;

    document
    .getElementById('sim-integral')
    .innerHTML=integralText;

    document
    .getElementById('sim-area')
    .innerHTML=
    `Area = ${area.toFixed(2)} units²`;

    if(window.MathJax){
        MathJax.typesetPromise();
    }

    const tracer=[{

        r:rValues,

        t:thetaValues.map(
            v=>v*(180/Math.PI)
        ),

        type:'scatterpolar',

        mode:'lines',

        line:{
            color:'#2563eb',
            width:3
        },

        fill:'toself',

        fillcolor:'rgba(37,99,235,0.15)'
    }];

    const layout={

        title:{
            text:'Polar Coordinate Workspace',
            font:{size:22}
        },

        paper_bgcolor:'#ffffff',

        font:{
            family:'Inter,sans-serif'
        },

        polar:{

            bgcolor:'#ffffff',

            radialaxis:{
                visible:true,
                gridcolor:'#e2e8f0'
            },

            angularaxis:{
                gridcolor:'#e2e8f0'
            }
        },

        margin:{
            t:70,
            b:40,
            l:40,
            r:40
        }
    };

    Plotly.react(
        'plot-area',
        tracer,
        layout,
        {
            responsive:true,
            displaylogo:false
        }
    );
}

/* Quiz */

function gradeQuizEngine(){

    const selected=
    document.querySelector(
        'input[name="q1"]:checked'
    );

    const feedback=
    document.getElementById(
        'quiz-feedback'
    );

    if(!selected){

        feedback.innerHTML=
        "Please select an option.";

        feedback.style.color='red';

        return;
    }

    if(selected.value==='correct'){

        feedback.innerHTML=
        "Correct! The Jacobian scaling factor is r.";

        feedback.style.color='green';
    }

    else{

        feedback.innerHTML=
        "Incorrect. The correct answer is r.";

        feedback.style.color='red';
    }
}

/* Initialize */

runTheoryMathEngine();

</script>

</body>
</html>
