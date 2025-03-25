# WEB-T-CLA
**F1 Quiz Game - Implementation Documentation**

**Introduction**

The F1 Quiz Game is a web-based quiz application designed using HTML, CSS, and JavaScript. The game presents a set of multiple-choice questions related to Formula 1, allowing users to test their knowledge. The quiz includes a start button, real-time feedback, and a final score display upon completion.

**1. Technologies Used**

HTML5: Structure and layout of the quiz.
CSS3: Basic styling and responsiveness.
Bootstrap 5: Pre-styled components for buttons and layout.
JavaScript (Vanilla JS): Logic for handling the quiz flow, user interactions, and score tracking.

**2. File Structure**

index.html: Main file containing the quiz structure.
casestudy.css: Stylesheet for the quiz.
JavaScript (Inline in HTML): Handles quiz logic and user interactions.

**3. Implementation Details**
**3.1 HTML Structure**

The game consists of three main sections:
Start Screen: Displays a Start Quiz button.
Quiz Container: Shows questions and answer options.
End Screen: Displays the final score and a restart button.
The quiz-container and end-screen are hidden initially and become visible based on user interaction.

**3.2 JavaScript Implementation**
**The JavaScript code is responsible for:**

Managing quiz data.
Displaying questions dynamically.
Handling user input and checking answers.
Displaying feedback messages.
Keeping track of the score.
Handling the start and restart functionality.

Quiz Data (Array of Objects)

const quizData = [
    { question: "Who has won the most F1 championships?", options: ["Lewis Hamilton", "Michael Schumacher", "Max Verstappen", "Ayrton Senna"], answer: "Michael Schumacher" },
    { question: "Which team has the most Constructors' Championships?", options: ["Mercedes", "Ferrari", "Red Bull", "McLaren"], answer: "Ferrari" },
    { question: "Which country hosts the Monaco Grand Prix?", options: ["France", "Italy", "Monaco", "Spain"], answer: "Monaco" },
    { question: "Who was the first ever F1 World Champion?", options: ["Juan Manuel Fangio", "Giuseppe Farina", "Alberto Ascari", "Stirling Moss"], answer: "Giuseppe Farina" }
];

Stores the quiz questions, possible answer choices, and the correct answer.
Start Quiz Function

function startQuiz() {
    document.getElementById("start-screen").style.display = "none";
    document.getElementById("quiz-container").style.display = "block";
    loadQuestion();
}

Hides the start screen and displays the quiz section.
Calls loadQuestion() to begin the quiz.
Loading Questions Dynamically

function loadQuestion() {
    if (currentQuestionIndex >= quizData.length) {
        endQuiz();
        return;
    }
    const questionData = quizData[currentQuestionIndex];
    document.getElementById('question').textContent = questionData.question;
    const optionsContainer = document.getElementById('options');
    optionsContainer.innerHTML = '';
    
    questionData.options.forEach(option => {
        const button = document.createElement('button');
        button.textContent = option;
        button.classList.add('btn', 'btn-primary', 'd-block', 'mx-auto', 'my-2');
        button.onclick = () => checkAnswer(option);
        optionsContainer.appendChild(button);
    });
}

Retrieves the current question and displays it dynamically.
Generates buttons for answer options.
Adds an onclick event to each button to check the answer when clicked.
Checking Answers & Providing Feedback

function checkAnswer(selected) {
    const correct = quizData[currentQuestionIndex].answer;
    const feedback = document.getElementById('feedback');

    if (selected === correct) {
        feedback.textContent = "Correct! 🎉";
        feedback.style.color = "green";
        score++;
    } else {
        feedback.textContent = `Wrong! The correct answer is ${correct}.`;
        feedback.style.color = "red";
    }

    setTimeout(() => {
        currentQuestionIndex++;
        feedback.textContent = '';
        loadQuestion();
    }, 2000);
}

Compares the selected answer with the correct answer.
Displays appropriate feedback.
Moves to the next question after 2 seconds.
Ending the Quiz & Showing Results

function endQuiz() {
    document.getElementById("quiz-container").style.display = "none";
    document.getElementById("end-screen").style.display = "block";
    document.getElementById("score").textContent = `Your Score: ${score}/${quizData.length}`;
}

Hides the quiz section and displays the final score.
Restarting the Quiz

function restartQuiz() {
    currentQuestionIndex = 0;
    score = 0;
    document.getElementById("end-screen").style.display = "none";
    startQuiz();
}

Resets the quiz variables.
Restarts the game from the beginning.

**4. User Flow**

User clicks Start Quiz.
Questions are displayed one by one with multiple-choice answers.
User selects an answer, and feedback is provided.
Quiz continues until all questions are answered.
Final score is displayed at the end with an option to restart.

**5. Features & Enhancements**

✅ Start and End screens for a structured flow.
✅ Dynamic question loading using JavaScript.
✅ Automatic feedback system for correct and incorrect answers.
✅ Score tracking to evaluate performance.
✅ Restart option to play again.

**6. Conclusion**

This F1 Quiz Game is an interactive web-based application that tests users' knowledge of Formula 1. Using JavaScript, it dynamically manages quiz flow, user interaction, and score tracking, making it an engaging and educational game.
