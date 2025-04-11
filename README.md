<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบสอบออนไลน์ | Online Exam System</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500&family=Sarabun:wght@400;500;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-color: #4361ee;
            --secondary-color: #3f37c9;
            --accent-color: #4895ef;
            --success-color: #4cc9f0;
            --danger-color: #f72585;
            --light-bg: #f8f9fa;
            --dark-text: #212529;
            --light-text: #f8f9fa;
        }
        
        body {
            font-family: 'Sarabun', sans-serif;
            background-color: #f5f7ff;
            color: var(--dark-text);
            line-height: 1.6;
        }
        
        h1, h2, h3, h4, h5, h6 {
            font-family: 'Kanit', sans-serif;
            font-weight: 500;
        }
        
        .navbar {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        }
        
        .navbar-brand {
            font-weight: 500;
            letter-spacing: 0.5px;
        }
        
        .exam-card {
            margin-bottom: 25px;
            border: none;
            border-radius: 12px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.08);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            overflow: hidden;
        }
        
        .exam-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 20px rgba(0, 0, 0, 0.12);
        }
        
        .exam-card .card-body {
            padding: 1.75rem;
        }
        
        .exam-card .card-footer {
            background-color: rgba(255, 255, 255, 0.9);
            border-top: 1px solid rgba(0, 0, 0, 0.03);
            padding: 1rem 1.75rem;
        }
        
        .question-card {
            margin-bottom: 25px;
            padding: 20px;
            border-radius: 10px;
            background-color: white;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            border-left: 4px solid var(--accent-color);
        }
        
        .timer {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--danger-color);
            background-color: rgba(247, 37, 133, 0.1);
            padding: 8px 16px;
            border-radius: 50px;
            display: inline-flex;
            align-items: center;
        }
        
        .timer i {
            margin-right: 8px;
        }
        
        .hidden {
            display: none;
        }
        
        .correct-answer {
            background-color: rgba(76, 201, 240, 0.1);
            border-left: 4px solid var(--success-color);
        }
        
        .wrong-answer {
            background-color: rgba(247, 37, 133, 0.08);
            border-left: 4px solid var(--danger-color);
        }
        
        .btn-primary {
            background-color: var(--primary-color);
            border-color: var(--primary-color);
            padding: 10px 24px;
            border-radius: 50px;
            font-weight: 500;
            letter-spacing: 0.5px;
            transition: all 0.3s ease;
        }
        
        .btn-primary:hover {
            background-color: var(--secondary-color);
            border-color: var(--secondary-color);
            transform: translateY(-2px);
        }
        
        .btn-success {
            padding: 12px 28px;
            border-radius: 50px;
            font-weight: 500;
            letter-spacing: 0.5px;
            transition: all 0.3s ease;
        }
        
        .btn-success:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(40, 167, 69, 0.3);
        }
        
        .result-card {
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.08);
            border: none;
        }
        
        .result-card .card-header {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            padding: 1.5rem;
        }
        
        .score-display {
            font-size: 3rem;
            font-weight: 700;
            color: var(--primary-color);
            margin: 20px 0;
            text-align: center;
        }
        
        .progress {
            height: 10px;
            border-radius: 5px;
            margin-bottom: 20px;
        }
        
        .progress-bar {
            background-color: var(--accent-color);
        }
        
        .form-control, .form-select {
            padding: 12px 16px;
            border-radius: 8px;
            border: 1px solid #e0e0e0;
        }
        
        .form-control:focus, .form-select:focus {
            border-color: var(--accent-color);
            box-shadow: 0 0 0 0.25rem rgba(67, 97, 238, 0.25);
        }
        
        .form-check-input:checked {
            background-color: var(--primary-color);
            border-color: var(--primary-color);
        }
        
        .badge {
            padding: 6px 10px;
            border-radius: 50px;
            font-weight: 500;
        }
        
        @media (max-width: 768px) {
            .exam-card {
                margin-bottom: 20px;
            }
            
            .question-card {
                padding: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container py-4">
        <!-- หน้าหลัก -->
        <div id="main-page">
            <nav class="navbar navbar-expand-lg navbar-dark mb-4 rounded-3">
                <div class="container-fluid">
                    <a class="navbar-brand" href="#">
                        <i class="fas fa-graduation-cap me-2"></i>ระบบสอบออนไลน์
                    </a>
                </div>
            </nav>

            <!-- แดชบอร์ด -->
            <div id="dashboard-section">
                <div class="d-flex justify-content-between align-items-center mb-4">
                    <h2 class="mb-0">แบบทดสอบทั้งหมด</h2>
                </div>
                <div class="row" id="exam-cards">
                    <!-- ข้อสอบจะแสดงที่นี่ -->
                </div>
                
            </div>

            <!-- หน้าสอบ -->
            <div id="exam-section" class="hidden">
                <div class="d-flex justify-content-between align-items-center mb-4">
                    <h2 class="mb-0" id="exam-title"></h2>
                    <div class="timer">
                        <i class="fas fa-clock"></i>
                        <span id="timer">เวลาเหลือ: 00:00</span>
                    </div>
                </div>
                <div class="alert alert-primary mb-4" id="exam-description"></div>
                <form id="exam-form">
                    <div id="questions-container">
                        <!-- คำถามจะแสดงที่นี่ -->
                    </div>
                    <div class="text-center mt-4">
                        <button type="submit" class="btn btn-success" id="submit-exam">
                            <i class="fas fa-paper-plane me-2"></i>ส่งคำตอบ
                        </button>
                    </div>
                </form>
            </div>

            <!-- ผลสอบ -->
            <div id="results-section" class="hidden">
                <div id="current-result">
                    <!-- ผลสอบล่าสุดจะแสดงที่นี่ -->
                </div>
                <div class="text-center mt-4">
                    <button class="btn btn-primary" id="back-to-exams">
                        <i class="fas fa-arrow-left me-2"></i>กลับสู่หน้าข้อสอบทั้งหมด
                    </button>
                    <button onclick="window.location.href='report.php'">ไปหน้ารายงานผล</button>
                    
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>
    <script>
        // ข้อมูลข้อสอบ (ไม่ใช้ฐานข้อมูล)
        const exams = [
            {
                id: 1,
                title: 'แบบทดสอบความรู้ทั่วไป',
                description: 'แบบทดสอบความรู้ทั่วไป 4 ข้อ ใช้เวลา 5 นาที',
                time_limit: 5, // นาที
                questions: [
                    {
                        id: 1,
                        question_text: 'ข้อใดคือเมืองหลวงของประเทศไทย?',
                        question_type: 'multiple_choice',
                        points: 1,
                        choices: [
                            { id: 1, choice_text: 'เชียงใหม่', is_correct: false },
                            { id: 2, choice_text: 'กรุงเทพมหานคร', is_correct: true },
                            { id: 3, choice_text: 'ภูเก็ต', is_correct: false },
                            { id: 4, choice_text: 'ขอนแก่น', is_correct: false }
                        ]
                    },
                    {
                        id: 2,
                        question_text: '1 + 1 เท่ากับเท่าไร?',
                        question_type: 'multiple_choice',
                        points: 1,
                        choices: [
                            { id: 5, choice_text: '1', is_correct: false },
                            { id: 6, choice_text: '2', is_correct: true },
                            { id: 7, choice_text: '3', is_correct: false },
                            { id: 8, choice_text: '4', is_correct: false }
                        ]
                    },
                    {
                        id: 3,
                        question_text: 'ดวงอาทิตย์เป็นดาวฤกษ์ที่ใกล้โลกที่สุด ใช่หรือไม่?',
                        question_type: 'true_false',
                        points: 1,
                        choices: [
                            { id: 9, choice_text: 'ใช่', is_correct: true },
                            { id: 10, choice_text: 'ไม่ใช่', is_correct: false }
                        ]
                    },
                    {
                        id: 4,
                        question_text: 'สีของดวงอาทิตย์คือสีอะไร? (ตอบเป็นภาษาไทย)',
                        question_type: 'short_answer',
                        points: 1,
                        correct_answer: 'สีเหลือง'
                    }
                ]
            },
            {
                id: 2,
                title: 'แบบทดสอบวิทยาศาสตร์',
                description: 'แบบทดสอบวิทยาศาสตร์พื้นฐาน 3 ข้อ ใช้เวลา 3 นาที',
                time_limit: 3, // นาที
                questions: [
                    {
                        id: 5,
                        question_text: 'น้ำเดือดที่อุณหภูมิกองศาเซลเซียส?',
                        question_type: 'multiple_choice',
                        points: 1,
                        choices: [
                            { id: 11, choice_text: '50 องศา', is_correct: false },
                            { id: 12, choice_text: '75 องศา', is_correct: false },
                            { id: 13, choice_text: '100 องศา', is_correct: true },
                            { id: 14, choice_text: '120 องศา', is_correct: false }
                        ]
                    },
                    {
                        id: 6,
                        question_text: 'พืชใช้กระบวนการอะไรเพื่อสร้างอาหาร? (ตอบเป็นภาษาไทย)',
                        question_type: 'short_answer',
                        points: 2,
                        correct_answer: 'การสังเคราะห์แสง'
                    },
                    {
                        id: 7,
                        question_text: 'มนุษย์มีโครโมโซมกี่คู่?',
                        question_type: 'multiple_choice',
                        points: 1,
                        choices: [
                            { id: 15, choice_text: '23 คู่', is_correct: true },
                            { id: 16, choice_text: '46 คู่', is_correct: false },
                            { id: 17, choice_text: '32 คู่', is_correct: false }
                        ]
                    }
                ]
            }
        ];

        let currentExam = null;
        let timerInterval = null;
        let timeLeft = 0;
        let currentResult = null;

        // โหลดข้อสอบทั้งหมดเมื่อหน้าเว็บโหลดเสร็จ
        document.addEventListener('DOMContentLoaded', function() {
            loadExams();
        });

        // แสดงหน้าต่างๆ
        function showPage(pageId) {
            document.querySelectorAll('#main-page > div').forEach(div => {
                div.classList.add('hidden');
            });
            document.getElementById(pageId).classList.remove('hidden');
        }

        // โหลดข้อสอบทั้งหมด
        function loadExams() {
            const examCards = document.getElementById('exam-cards');
            examCards.innerHTML = '';

            exams.forEach(exam => {
                const card = document.createElement('div');
                card.className = 'col-md-6 col-lg-4';
                card.innerHTML = `
                    <div class="exam-card card h-100">
                        <div class="card-body">
                            <h5 class="card-title">${exam.title}</h5>
                            <p class="card-text text-muted">${exam.description}</p>
                            <div class="d-flex align-items-center mt-3">
                                <span class="badge bg-primary me-2">
                                    <i class="fas fa-clock me-1"></i>${exam.time_limit} นาที
                                </span>
                                <span class="badge bg-success">
                                    <i class="fas fa-question-circle me-1"></i>${exam.questions.length} ข้อ
                                </span>
                            </div>
                        </div>
                        <div class="card-footer bg-transparent">
                            <button class="btn btn-primary w-100 start-exam-btn" data-exam-id="${exam.id}">
                                <i class="fas fa-play me-2"></i>เริ่มทำแบบทดสอบ
                            </button>
                        </div>
                    </div>
                `;
                examCards.appendChild(card);
            });

            // เพิ่ม Event Listener สำหรับปุ่มเริ่มทำแบบทดสอบ
            document.querySelectorAll('.start-exam-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const examId = parseInt(this.getAttribute('data-exam-id'));
                    startExam(examId);
                });
            });
        }

        // เริ่มทำข้อสอบ
        function startExam(examId) {
            currentExam = exams.find(exam => exam.id === examId);
            
            if (!currentExam) {
                alert('ไม่พบข้อสอบที่เลือก');
                return;
            }

            // แสดงหน้าสอบ
            document.getElementById('exam-title').textContent = currentExam.title;
            document.getElementById('exam-description').textContent = currentExam.description;
            
            // ตั้งเวลา
            timeLeft = currentExam.time_limit * 60; // แปลงเป็นวินาที
            updateTimerDisplay();
            
            if (timerInterval) {
                clearInterval(timerInterval);
            }
            
            timerInterval = setInterval(function() {
                timeLeft--;
                updateTimerDisplay();
                
                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    submitExam();
                }
            }, 1000);

            // แสดงคำถาม
            const questionsContainer = document.getElementById('questions-container');
            questionsContainer.innerHTML = '';
            
            currentExam.questions.forEach((question, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question-card';
                questionDiv.innerHTML = `
                    <h5 class="mb-3"><span class="badge bg-primary me-2">ข้อ ${index + 1}</span>${question.question_text}</h5>
                    <p class="text-muted mb-3"><i class="fas fa-star me-2"></i>คะแนน: ${question.points} คะแนน</p>
                    <div class="question-options" data-question-id="${question.id}">
                        ${renderQuestionOptions(question)}
                    </div>
                `;
                questionsContainer.appendChild(questionDiv);
            });

            showPage('exam-section');
        }

        // แสดงตัวเลือกคำถาม
        function renderQuestionOptions(question) {
            if (question.question_type === 'multiple_choice' || question.question_type === 'true_false') {
                let optionsHtml = '';
                question.choices.forEach(choice => {
                    optionsHtml += `
                        <div class="form-check mb-2">
                            <input class="form-check-input" type="radio" name="question_${question.id}" 
                                   id="choice_${choice.id}" value="${choice.id}">
                            <label class="form-check-label" for="choice_${choice.id}">
                                ${choice.choice_text}
                            </label>
                        </div>
                    `;
                });
                return optionsHtml;
            } else if (question.question_type === 'short_answer') {
                return `
                    <div class="form-group">
                        <textarea class="form-control" name="question_${question.id}" rows="3" placeholder="พิมพ์คำตอบของคุณที่นี่..."></textarea>
                    </div>
                `;
            }
            return '';
        }

        // อัพเดทตัวนับเวลา
        function updateTimerDisplay() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            document.getElementById('timer').textContent = 
                `เวลาเหลือ: ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
        }

        // ส่งคำตอบ
        document.getElementById('exam-form').addEventListener('submit', function(e) {
            e.preventDefault();
            submitExam();
        });

        function submitExam() {
            clearInterval(timerInterval);
            
            // เก็บคำตอบ
            const answers = [];
            let score = 0;
            let totalPoints = 0;
            
            currentExam.questions.forEach(question => {
                totalPoints += question.points;
                
                if (question.question_type === 'multiple_choice' || question.question_type === 'true_false') {
                    const selectedChoice = document.querySelector(`input[name="question_${question.id}"]:checked`);
                    if (selectedChoice) {
                        const choiceId = parseInt(selectedChoice.value);
                        const choice = question.choices.find(c => c.id === choiceId);
                        
                        answers.push({
                            question_id: question.id,
                            question_text: question.question_text,
                            answer_text: choice.choice_text,
                            is_correct: choice.is_correct,
                            points_earned: choice.is_correct ? question.points : 0
                        });
                        
                        if (choice.is_correct) {
                            score += question.points;
                        }
                    } else {
                        answers.push({
                            question_id: question.id,
                            question_text: question.question_text,
                            answer_text: 'ไม่ได้ตอบ',
                            is_correct: false,
                            points_earned: 0
                        });
                    }
                } else if (question.question_type === 'short_answer') {
                    const answerText = document.querySelector(`textarea[name="question_${question.id}"]`).value;
                    const isCorrect = answerText.toLowerCase().includes(question.correct_answer.toLowerCase());
                    
                    answers.push({
                        question_id: question.id,
                        question_text: question.question_text,
                        answer_text: answerText,
                        is_correct: isCorrect,
                        points_earned: isCorrect ? question.points : 0
                    });
                    
                    if (isCorrect) {
                        score += question.points;
                    }
                }
            });
            
            const percentage = Math.round((score / totalPoints) * 100);
            
            // บันทึกผลสอบ
            currentResult = {
                exam_id: currentExam.id,
                exam_title: currentExam.title,
                score: percentage,
                total_questions: currentExam.questions.length,
                correct_answers: answers.filter(a => a.is_correct).length,
                answers: answers
            };
            
            // แสดงผลสอบ
            showResult(currentResult);
        }

        // แสดงผลสอบ
        function showResult(result) {
            showPage('results-section');
            
            const resultDiv = document.getElementById('current-result');
            resultDiv.innerHTML = `
                <div class="result-card card mb-4">
                    <div class="card-header">
                        <h4 class="mb-0"><i class="fas fa-poll me-2"></i>${result.exam_title}</h4>
                    </div>
                    <div class="card-body">
                        <div class="score-display">
                            ${result.score}%
                        </div>
                        <div class="progress">
                            <div class="progress-bar" role="progressbar" style="width: ${result.score}%" 
                                 aria-valuenow="${result.score}" aria-valuemin="0" aria-valuemax="100"></div>
                        </div>
                        <div class="text-center mb-4">
                            <p class="h5">
                                ตอบถูก ${result.correct_answers} จาก ${result.total_questions} ข้อ
                            </p>
                            <p class="text-muted">
                                ${getResultMessage(result.score)}
                            </p>
                        </div>
                        <hr>
                        <h5 class="mb-4"><i class="fas fa-list-ol me-2"></i>รายละเอียดคำตอบ</h5>
                        ${renderResultDetails(result.answers)}
                    </div>
                </div>
            `;
        }

        // ข้อความแสดงผลตามคะแนน
        function getResultMessage(score) {
            if (score >= 80) return 'ยอดเยี่ยม! คุณทำได้ดีมาก';
            if (score >= 60) return 'ดีมาก! คุณผ่านเกณฑ์';
            if (score >= 40) return 'พอใช้ ลองทบทวนอีกครั้งจะดีกว่า';
            return 'ลองศึกษาทบทวนอีกครั้งนะครับ';
        }

        // แสดงรายละเอียดผลสอบ
        function renderResultDetails(answers) {
            let html = '';
            
            answers.forEach((answer, index) => {
                html += `
                    <div class="question-card ${answer.is_correct ? 'correct-answer' : 'wrong-answer'} mb-3">
                        <h6><span class="badge ${answer.is_correct ? 'bg-success' : 'bg-danger'} me-2">ข้อ ${index + 1}</span>
                            ${answer.question_text}
                        </h6>
                        <p class="mb-1"><strong>คำตอบของคุณ:</strong> ${answer.answer_text}</p>
                        <p class="mb-1"><strong>สถานะ:</strong> 
                            ${answer.is_correct ? 
                              '<span class="text-success"><i class="fas fa-check-circle me-1"></i>ถูกต้อง</span>' : 
                              '<span class="text-danger"><i class="fas fa-times-circle me-1"></i>ไม่ถูกต้อง</span>'}
                        </p>
                        <p class="mb-0"><strong>คะแนนที่ได้:</strong> ${answer.points_earned}</p>
                    </div>
                `;
            });
            
            return html;
        }

        // กลับสู่หน้าข้อสอบทั้งหมด
        document.getElementById('back-to-exams').addEventListener('click', function() {
            showPage('dashboard-section');
            loadExams();
        });
    </script>
</body>
</html>
