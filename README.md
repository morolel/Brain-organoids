<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Brain Organoids: Interactive Learning Platform</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        .container {
            width: 100%;
            max-width: 100%;
            padding: 20px;
        }

        .header {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            text-align: center;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
        }

        .header h1 {
            color: #4a5568;
            font-size: 2.5em;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .header p {
            font-size: 1.2em;
            color: #666;
        }

        .navigation {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 30px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
        }

        .nav-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
        }

        .nav-item {
            padding: 15px;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            font-weight: bold;
        }

        .nav-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }

        .content-section {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            display: none;
        }

        .content-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .section-title {
            color: #4a5568;
            font-size: 2em;
            margin-bottom: 20px;
            border-bottom: 3px solid #667eea;
            padding-bottom: 10px;
        }

        .interactive-element {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            color: white;
        }

        .quiz-container {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            border-left: 5px solid #667eea;
        }

        .quiz-question {
            font-weight: bold;
            margin-bottom: 15px;
            color: #4a5568;
        }

        .quiz-options {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .quiz-option {
            padding: 10px 15px;
            background: white;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .quiz-option:hover {
            border-color: #667eea;
            background: #f7fafc;
        }

        .quiz-option.correct {
            background: #48bb78;
            color: white;
            border-color: #48bb78;
        }

        .quiz-option.incorrect {
            background: #f56565;
            color: white;
            border-color: #f56565;
        }

        .expandable {
            background: #e6fffa;
            border: 2px solid #4fd1c7;
            border-radius: 10px;
            margin: 15px 0;
            overflow: hidden;
        }

        .expandable-header {
            background: #4fd1c7;
            color: white;
            padding: 15px;
            cursor: pointer;
            font-weight: bold;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .expandable-content {
            padding: 20px;
            display: none;
        }

        .expandable-content.active {
            display: block;
        }

        .key-concept {
            background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            border-left: 5px solid #ed8936;
        }

        .progress-bar {
            background: #e2e8f0;
            border-radius: 10px;
            height: 10px;
            margin: 20px 0;
            overflow: hidden;
        }

        .progress-fill {
            background: linear-gradient(90deg, #667eea, #764ba2);
            height: 100%;
            width: 0%;
            transition: width 0.3s ease;
        }

        .btn {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s ease;
            margin: 10px 5px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .image-placeholder {
            background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);
            border-radius: 10px;
            padding: 40px;
            text-align: center;
            margin: 20px 0;
            color: #4a5568;
            font-weight: bold;
        }

        .timeline {
            position: relative;
            margin: 30px 0;
        }

        .timeline-item {
            background: white;
            border-radius: 10px;
            padding: 20px;
            margin: 20px 0;
            margin-left: 30px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            position: relative;
        }

        .timeline-item::before {
            content: '';
            position: absolute;
            left: -15px;
            top: 25px;
            width: 12px;
            height: 12px;
            background: #667eea;
            border-radius: 50%;
        }

        .timeline-item::after {
            content: '';
            position: absolute;
            left: -9px;
            top: 37px;
            width: 2px;
            height: 100%;
            background: #667eea;
        }

        .timeline-item:last-child::after {
            display: none;
        }

        @media (max-width: 768px) {
            .nav-grid {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2em;
            }
            
            .container {
                padding: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🧠 Brain Organoids Interactive Learning Platform</h1>
            <p>Explore the fascinating world of lab-grown brain tissue and its revolutionary applications in neuroscience research</p>
        </div>

        <div class="navigation">
            <div class="nav-grid">
                <div class="nav-item" onclick="showSection('intro')">1. Introduction</div>
                <div class="nav-item" onclick="showSection('concepts')">2. What are Brain Organoids?</div>
                <div class="nav-item" onclick="showSection('making')">3. How Are They Made?</div>
                <div class="nav-item" onclick="showSection('applications')">4. Applications & Uses</div>
                <div class="nav-item" onclick="showSection('challenges')">5. Challenges & Future</div>
                <div class="nav-item" onclick="showSection('ethics')">6. Ethics & Conclusion</div>
            </div>
        </div>

        <div class="progress-bar">
            <div class="progress-fill" id="progressFill"></div>
        </div>

        <!-- Introduction Section -->
        <div id="intro" class="content-section active">
            <h2 class="section-title">🚀 Introduction to Brain Organoids</h2>
            
            <div class="key-concept">
                <h3>🎯 Key Concept</h3>
                <p>Brain organoids are small, 3D clusters of human brain cells grown in laboratory dishes. Think of them as "mini-brains" that can help us understand how the human brain develops and what goes wrong in neurological diseases.</p>
            </div>

            <div class="timeline">
                <div class="timeline-item">
                    <h3>2013 - The Beginning</h3>
                    <p>Scientists Madelaine Lancaster and Juergen Knoblich create the first brain organoids to study microcephaly (small brain condition).</p>
                </div>
                <div class="timeline-item">
                    <h3>2013 - Self-Organization Discovery</h3>
                    <p>Yoshiki Sasai's team discovers that human stem cells can self-organize into brain-like structures.</p>
                </div>
                <div class="timeline-item">
                    <h3>Today</h3>
                    <p>Brain organoids are used worldwide to study brain development, disease, and test new treatments.</p>
                </div>
            </div>

            <div class="quiz-container">
                <div class="quiz-question">🤔 Quick Check: What year were brain organoids first developed?</div>
                <div class="quiz-options">
                    <div class="quiz-option" onclick="checkAnswer(this, false)">2010</div>
                    <div class="quiz-option" onclick="checkAnswer(this, true)">2013</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">2015</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">2020</div>
                </div>
            </div>

            <div class="interactive-element">
                <h3>🔍 Did You Know?</h3>
                <p>Brain organoids are currently only about 5mm in diameter (half a centimeter) - smaller than a pea! But they can already mimic many aspects of how a real human brain develops.</p>
            </div>
        </div>

        <!-- Concepts Section -->
        <div id="concepts" class="content-section">
            <h2 class="section-title">🧩 What Are Brain Organoids?</h2>

            <div class="key-concept">
                <h3>🎯 Definition</h3>
                <p>Brain organoids are 3D cell cultures that resemble the structure and function of human brain tissue. They're made from stem cells and can develop into different types of brain cells.</p>
            </div>

            <div class="expandable">
                <div class="expandable-header" onclick="toggleExpand(this)">
                    <span>🏗️ Three Key Requirements for Brain Organoids</span>
                    <span>+</span>
                </div>
                <div class="expandable-content">
                    <ol>
                        <li><strong>Architecture:</strong> Must look like real brain tissue</li>
                        <li><strong>Cell Types:</strong> Must contain the same types of cells as the brain</li>
                        <li><strong>Self-Organization:</strong> Must be able to organize themselves naturally</li>
                    </ol>
                </div>
            </div>

            <div class="image-placeholder">
                [Interactive Diagram: Brain Organoid Structure]
                <br>Imagine layers of cells organizing themselves just like in a developing brain!
            </div>

            <div class="expandable">
                <div class="expandable-header" onclick="toggleExpand(this)">
                    <span>🎯 Types of Brain Organoids</span>
                    <span>+</span>
                </div>
                <div class="expandable-content">
                    <h4>Unguided (Whole-Brain) Organoids:</h4>
                    <p>✅ Contain multiple brain regions<br>
                    ❌ Results can be unpredictable</p>
                    
                    <h4>Guided (Region-Specific) Organoids:</h4>
                    <p>✅ Focus on specific brain areas (cortex, cerebellum, etc.)<br>
                    ✅ More predictable results</p>
                </div>
            </div>

            <div class="quiz-container">
                <div class="quiz-question">🤔 Which type of organoid is more predictable in its development?</div>
                <div class="quiz-options">
                    <div class="quiz-option" onclick="checkAnswer(this, false)">Unguided organoids</div>
                    <div class="quiz-option" onclick="checkAnswer(this, true)">Guided organoids</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">Both are equally predictable</div>
                </div>
            </div>
        </div>

        <!-- Making Section -->
        <div id="making" class="content-section">
            <h2 class="section-title">🔬 How Are Brain Organoids Made?</h2>

            <div class="key-concept">
                <h3>🎯 The Basic Process</h3>
                <p>Think of making brain organoids like following a recipe - you need the right ingredients, the right environment, and the right steps!</p>
            </div>

            <div class="timeline">
                <div class="timeline-item">
                    <h3>Step 1: Get Stem Cells</h3>
                    <p>Scientists take regular cells (like skin cells) and reprogram them to become stem cells using "Yamanaka factors" - special proteins that reset the cells.</p>
                </div>
                <div class="timeline-item">
                    <h3>Step 2: Form Embryoid Bodies</h3>
                    <p>Stem cells are grouped together in small clusters called embryoid bodies - like tiny cell communities.</p>
                </div>
                <div class="timeline-item">
                    <h3>Step 3: Add Growth Factors</h3>
                    <p>Special chemicals (growth factors) guide the cells to become brain cells instead of other types of cells.</p>
                </div>
                <div class="timeline-item">
                    <h3>Step 4: Embed in Matrix</h3>
                    <p>Cells are placed in a gel-like substance (often Matrigel) that acts like scaffolding to support 3D growth.</p>
                </div>
                <div class="timeline-item">
                    <h3>Step 5: Bioreactor</h3>
                    <p>Organoids are placed in a spinning bioreactor that provides nutrients and oxygen, helping them grow larger.</p>
                </div>
            </div>

            <div class="interactive-element">
                <h3>🧪 Key Ingredients</h3>
                <p><strong>Stem Cells:</strong> The starting material<br>
                <strong>Growth Factors:</strong> Chemical signals that guide development<br>
                <strong>Matrix:</strong> Physical support structure<br>
                <strong>Bioreactor:</strong> Controlled environment for growth</p>
            </div>

            <div class="quiz-container">
                <div class="quiz-question">🤔 What is the main purpose of the bioreactor?</div>
                <div class="quiz-options">
                    <div class="quiz-option" onclick="checkAnswer(this, false)">To make the organoids smaller</div>
                    <div class="quiz-option" onclick="checkAnswer(this, true)">To provide nutrients and oxygen</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">To freeze the organoids</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">To change the cell type</div>
                </div>
            </div>
        </div>

        <!-- Applications Section -->
        <div id="applications" class="content-section">
            <h2 class="section-title">🎯 Applications & Uses</h2>

            <div class="key-concept">
                <h3>🎯 Why Are Brain Organoids Important?</h3>
                <p>Brain organoids are revolutionizing neuroscience research by providing a more human-like model than traditional methods!</p>
            </div>

            <div class="expandable">
                <div class="expandable-header" onclick="toggleExpand(this)">
                    <span>🔬 Disease Modeling</span>
                    <span>+</span>
                </div>
                <div class="expandable-content">
                    <h4>Neurodevelopmental Diseases:</h4>
                    <p>• Microcephaly (small brain)<br>• Autism spectrum disorders<br>• Lissencephaly (smooth brain)</p>
                    
                    <h4>Neurodegenerative Diseases:</h4>
                    <p>• Alzheimer's disease<br>• Parkinson's disease<br>• Huntington's disease</p>
                    
                    <h4>Psychiatric Disorders:</h4>
                    <p>• Schizophrenia<br>• Bipolar disorder<br>• Depression</p>
                </div>
            </div>

            <div class="expandable">
                <div class="expandable-header" onclick="toggleExpand(this)">
                    <span>🐭 Replacing Animal Models</span>
                    <span>+</span>
                </div>
                <div class="expandable-content">
                    <h4>Why are organoids better than mouse models?</h4>
                    <p>• <strong>Human-specific:</strong> Made from human cells<br>
                    • <strong>More ethical:</strong> No animal suffering<br>
                    • <strong>Better similarity:</strong> Human brain has folds (gyrification), mouse brains are smooth<br>
                    • <strong>Human diseases:</strong> Some diseases only affect humans</p>
                </div>
            </div>

            <div class="expandable">
                <div class="expandable-header" onclick="toggleExpand(this)">
                    <span>💊 Drug Testing & Personalized Medicine</span>
                    <span>+</span>
                </div>
                <div class="expandable-content">
                    <h4>Drug Discovery:</h4>
                    <p>• Test new treatments safely<br>• Screen for toxic effects<br>• Understand how drugs work</p>
                    
                    <h4>Personalized Treatment:</h4>
                    <p>• Make organoids from patient's own cells<br>• Test which treatments work best<br>• Predict treatment responses</p>
                </div>
            </div>

            <div class="quiz-container">
                <div class="quiz-question">🤔 What advantage do brain organoids have over mouse models?</div>
                <div class="quiz-options">
                    <div class="quiz-option" onclick="checkAnswer(this, false)">They're cheaper to maintain</div>
                    <div class="quiz-option" onclick="checkAnswer(this, true)">They're made from human cells</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">They grow faster</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">They're easier to study</div>
                </div>
            </div>

            <div class="interactive-element">
                <h3>🌟 Real-World Impact</h3>
                <p>Scientists have already used brain organoids to discover new mechanisms of Alzheimer's disease and test potential treatments. Some organoids have even been transplanted into stroke-damaged mouse brains and helped repair the damage!</p>
            </div>
        </div>

        <!-- Challenges Section -->
        <div id="challenges" class="content-section">
            <h2 class="section-title">⚠️ Challenges & Future Solutions</h2>

            <div class="key-concept">
                <h3>🎯 Current Limitations</h3>
                <p>While brain organoids are amazing, they still have some challenges that scientists are working to overcome.</p>
            </div>

            <div class="expandable">
                <div class="expandable-header" onclick="toggleExpand(this)">
                    <span>💀 Necrotic Core Problem</span>
                    <span>+</span>
                </div>
                <div class="expandable-content">
                    <h4>The Problem:</h4>
                    <p>When organoids grow too large (>1mm), the center doesn't get enough oxygen and nutrients, so cells die.</p>
                    
                    <h4>Solutions Being Developed:</h4>
                    <p>• Better stirring systems<br>• Higher oxygen levels<br>• Microfluidic chambers<br>• Adding blood vessels (vascularization)</p>
                </div>
            </div>

            <div class="expandable">
                <div class="expandable-header" onclick="toggleExpand(this)">
                    <span>🎲 Variability Issues</span>
                    <span>+</span>
                </div>
                <div class="expandable-content">
                    <h4>The Problem:</h4>
                    <p>Organoids from the same batch can develop differently, making results hard to reproduce.</p>
                    
                    <h4>Solutions:</h4>
                    <p>• Standardized protocols<br>• Synthetic matrices with defined composition<br>• Better quality control<br>• Guided development methods</p>
                </div>
            </div>

            <div class="expandable">
                <div class="expandable-header" onclick="toggleExpand(this)">
                    <span>🧩 Assembloids - The Future?</span>
                    <span>+</span>
                </div>
                <div class="expandable-content">
                    <h4>What are Assembloids?</h4>
                    <p>Multiple different brain organoids fused together to create more complex, brain-like structures.</p>
                    
                    <h4>Potential Benefits:</h4>
                    <p>• More complete brain models<br>• Better disease modeling<br>• Study brain connections<br>• More realistic drug testing</p>
                </div>
            </div>

            <div class="quiz-container">
                <div class="quiz-question">🤔 What is the main cause of the necrotic core problem?</div>
                <div class="quiz-options">
                    <div class="quiz-option" onclick="checkAnswer(this, false)">Too much oxygen</div>
                    <div class="quiz-option" onclick="checkAnswer(this, true)">Lack of nutrients and oxygen in the center</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">Wrong temperature</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">Contamination</div>
                </div>
            </div>

            <div class="interactive-element">
                <h3>🔮 Future Possibilities</h3>
                <p>Scientists are working on creating brain organoids with blood vessels, connecting them to artificial bodies, and even developing organoids that can interface with computers. The future of brain organoid research is incredibly exciting!</p>
            </div>
        </div>

        <!-- Ethics Section -->
        <div id="ethics" class="content-section">
            <h2 class="section-title">🤝 Ethics & Conclusion</h2>

            <div class="key-concept">
                <h3>🎯 Ethical Considerations</h3>
                <p>As brain organoids become more sophisticated, we need to consider important ethical questions about consciousness, consent, and the responsible use of this technology.</p>
            </div>

            <div class="expandable">
                <div class="expandable-header" onclick="toggleExpand(this)">
                    <span>🤔 Key Ethical Questions</span>
                    <span>+</span>
                </div>
                <div class="expandable-content">
                    <h4>Consciousness Concerns:</h4>
                    <p>• Could brain organoids ever become conscious?<br>• How would we know if they were?<br>• What responsibilities would we have?</p>
                    
                    <h4>Current Scientific Consensus:</h4>
                    <p>• Current organoids are too small and simple<br>• No evidence of higher brain functions<br>• Continuous monitoring is important</p>
                </div>
            </div>

            <div class="expandable">
                <div class="expandable-header" onclick="toggleExpand(this)">
                    <span>✅ Benefits vs. Risks</span>
                    <span>+</span>
                </div>
                <div class="expandable-content">
                    <h4>Major Benefits:</h4>
                    <p>• Reduce animal testing<br>• Better disease understanding<br>• Personalized treatments<br>• Drug safety testing</p>
                    
                    <h4>Potential Risks:</h4>
                    <p>• Misuse of technology<br>• Ethical concerns about consciousness<br>• Need for proper regulation</p>
                </div>
            </div>

            <div class="interactive-element">
                <h3>🎯 The Bottom Line</h3>
                <p>Brain organoids represent one of the most promising advances in neuroscience. While we must proceed thoughtfully and ethically, the potential to understand and treat devastating brain diseases makes this research incredibly valuable for humanity.</p>
            </div>

            <div class="quiz-container">
                <div class="quiz-question">🤔 What is the current scientific consensus about consciousness in brain organoids?</div>
                <div class="quiz-options">
                    <div class="quiz-option" onclick="checkAnswer(this, false)">They are definitely conscious</div>
                    <div class="quiz-option" onclick="checkAnswer(this, true)">They are too small and simple to be conscious</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">We should assume they are conscious</div>
                    <div class="quiz-option" onclick="checkAnswer(this, false)">Consciousness is not a concern</div>
                </div>
            </div>

            <div class="key-concept">
                <h3>🎓 Conclusion</h3>
                <p>Brain organoids are a revolutionary tool that's already changing how we study the brain and develop treatments. While challenges remain, the future of this field is bright, and with careful ethical consideration, brain organoids will help us understand and cure brain diseases that affect millions of people worldwide.</p>
            </div>
        </div>

        <div class="interactive-element" style="text-align: center; margin-top: 40px;">
            <h3>🏆 Congratulations!</h3>
            <p>You've completed the Brain Organoids Learning Journey!</p>
            <button class="btn" onclick="restartJourney()">🔄 Start Over</button>
            <button class="btn" onclick="showFinalQuiz()">📝 Take Final Quiz</button>
        </div>
    </div>

    <script>
        let currentSection = 'intro';
        let completedSections = new Set();
        let totalSections = 6;

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.content-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Update current section
            currentSection = sectionId;
            completedSections.add(sectionId);
            
            // Update progress bar
            updateProgress();
            
            // Scroll to top
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function updateProgress() {
            const progress = (completedSections.size / totalSections) * 100;
            document.getElementById('progressFill').style.width = progress + '%';
        }

        function toggleExpand(header) {
            const content = header.nextElementSibling;
            const isActive = content.classList.contains('active');
            
            if (isActive) {
                content.classList.remove('active');
                header.querySelector('span:last-child').textContent = '+';
            } else {
                content.classList.add('active');
                header.querySelector('span:last-child').textContent = '−';
            }
        }

        function checkAnswer(element, isCorrect) {
            // Remove any existing answer classes
            element.parentElement.querySelectorAll('.quiz-option').forEach(option => {
                option.classList.remove('correct', 'incorrect');
                option.style.pointerEvents = 'none';
            });
            
            // Add appropriate class
            if (isCorrect) {
                element.classList.add('correct');
                setTimeout(() => {
                    alert('🎉 Correct! Well done!');
                    resetQuiz(element.parentElement);
                }, 500);
            } else {
                element.classList.add('incorrect');
                setTimeout(() => {
                    alert('❌ Not quite right. Try again!');
                    resetQuiz(element.parentElement);
                }, 500);
            }
        }

        function resetQuiz(container) {
            container.querySelector
