# Quiz App Demo

This is a simple web app that is a quiz. The purpose of the quiz is to teach basic terminology of web based programming for HTML, CSS, PHP, SQL, and XML.

## Basic Features
* A number and visual bar timer that counts down.
* Automatically selects the correct answer when the timer runs out.
* 5 Premade questions about Web Development Terminology.
* Answers change into a dark blue when the mouse hovers over it and the cursor changes as well.
* The correct answer changes to green when selected and a checkmark appears.
* If a wrong answer is chosen then it turns red and a red X is shown, and the correct answer is displayed by turning green with a check mark.
* It shows the current questions and how many questions in total at the bottom left.
* At the end it says the quiz is complete and gives the user their score out of 5.
* Allows them to replay the quiz or just quit the quiz at the end.

## The Directory
In the DemoQuizApp there are 4 initial files. 2 folders, the index.html, and a .gitignore. The two folders are named css and js. In the css folder there’s a single style.css. In the js folder there are two javascript files named questions.js and quizApp.js. All of these files are referenced in the index.html file.

## The HTML
There is only 1 html file, index.html. In the head it implements the css file in “css/style.css” and an outside font at “https://kit.fontawesome.com/4a4f4b55b0.js”. It also implements the javascript files “js/questions.js” and “js/quizApp.js”, the first being the questions for the quiz and the later being the quiz logic.

The body of the html starts with a simple button to start the quiz.
`<div class="start_btn"><button>Start Quiz</button></div>`

Next there’s an info box that explains the rules of the quiz.
```html
<div class="info_box">
        <div class="info-title"><span>Some Rules of this Quiz</span></div>
        <div class="info-list">
            <div class="info">1. You will have only <span>15 seconds</span> per each question.</div>
            <div class="info">2. Once you select your answer, it can't be undone.</div>
            <div class="info">3. You can't select any option once time goes off.</div>
            <div class="info">4. You can't exit from the Quiz while you're playing.</div>
            <div class="info">5. You'll get points on the basis of your correct answers.</div>
        </div>
        <div class="buttons">
            <button class="quit">Exit Quiz</button>
            <button class="restart">Continue</button>
        </div>
</div>
```

Next, there’s the quiz box. In this box it has the timer, timer line (for the visuals), a place for the question, a place for the answer list, and there’s a footer for this box that holds the total number of questions and a button for going to the next question.

```html
<div class="quiz_box">
        <header>
            <div class="title">Demo Quiz App in JavaScript</div>
            <div class="timer">
                <div class="time_left_txt">Time Left</div>
                <div class="timer_sec">15</div>
            </div>
            <div class="time_line"></div>
        </header>
        <section>
            <div class="que_text">
                <!-- Insert questions from ./js/questions.js -->
            </div>
            <div class="option_list">
                <!-- Insert options to questions from ./js/questions.js -->
            </div>
        </section>

        <!-- footer of Quiz Box -->
        <footer>
            <div class="total_que">
                <!-- insert Question Count Number dynamically from JavaScript App logic -->
            </div>
            <button class="next_btn">Next Que</button>
        </footer>
</div>
```

Lastly, there’s a result box that shows a crown icon and announces that you’re finished, and tells you your score. There’s 2 more buttons that allow you to restart or quit the quiz.

```html
<div class="result_box">
        <div class="icon">
            <i class="fas fa-crown"></i>
        </div>
        <div class="complete_text">You've completed the Quiz!</div>
        <div class="score_text">
            <!-- insert dynamic user score as Result from JavaScript -->
        </div>
        <div class="buttons">
            <button class="restart">Replay Quiz</button>
            <button class="quit">Quit Quiz</button>
        </div>
</div>
```

## The CSS
They stylesheet first imports a google font and sets everything to default.

```css
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}
```

The css stylesheet declares default colors and positionings for the elements. An example of this is the result button:

```css
.result_box {
  background: #fff;
  border-radius: 5px;
  display: flex;
  padding: 25px 30px;
  width: 450px;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  transform: translate(-50%, -50%) scale(0.9);
  opacity: 0;
  pointer-events: none;
  transition: all 0.3s ease;
}
```

And for default positionings some of the defaults are listed as this:

```css
.start_btn,
.info_box,
.quiz_box,
.result_box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
```

## The JS
### questions.js
This script consists of a single array named “questions”. The array contains 5 objects, and they all contain a numb, question, answer, and options elements. The options element is another array of strings in each array. And example of the first object in the array is this:

```javascript
let questions = [
  {
    numb: 1,
    question: "What does HTML stand for?",
    answer: "Hyper Text Markup Language",
    options: [
      "Hyper Text Preprocessor",
      "Hyper Text Markup Language",
      "Hyper Text Multiple Language",
      "Hyper Tool Multi Language",
    ],
  },
```

### quizApp.js
The quizzApp.js contains all the main logic for the quiz. It starts off declaring all of the elements created in the html like buttons and the timer and the boxes themselves. Then it adds event listeners to the buttons and calls their respective functions and behaviors. An example of this is the continue and quit buttons:

```javascript
// if exitQuiz button clicked
exit_btn.addEventListener("click", (e) => {
  info_box.classList.remove("activeInfo"); //hide info box
});

// if continueQuiz button clicked
continue_btn.addEventListener("click", (e) => {
  info_box.classList.remove("activeInfo"); //hide info box
  quiz_box.classList.add("activeQuiz"); //show quiz box
  showQuetions(0); //calling showQestions function
  queCounter(1); //passing 1 parameter to queCounter
  startTimer(15); //calling startTimer function
  startTimerLine(0); //calling startTimerLine function
});
```

After this, it declares the main functions. showQuestions , which creates arrays for each option used in the options js script.

Next there’s the optionSelected function. When called it clears the current time counter and the timer line. It appends to the user score if they got it right and does nothing if they wrong besides indicate it with declaring it’s wrong.

```javascript
//if user selected option is equal to array's correct answer
  if (userAns == correcAns) {
    userScore += 1; //update total score value increment by 1
    answer.classList.add("correct"); //add green color to correct selected option
    answer.insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to correct selected option
    console.log("Correct Answer");
    console.log("Your correct answers = " + userScore);
  } else {
    answer.classList.add("incorrect"); //add red color to correct selected option
    answer.insertAdjacentHTML("beforeend", crossIconTag); //add cross icon to correct selected option
    console.log("Wrong Answer");

    for (i = 0; i < allOptions; i++) {
      if (option_list.children[i].textContent == correcAns) {
        //if there is an option which is matched to an array answer
        option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
        option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
        console.log("Auto selected correct answer.");
      }
    }
  }
```

The timer functions simply create a timer with an intercal of 1000. startTimer() has another function inside of it named timer(), and it decrements the time value over time. When the time is less than 0 then it will act out an “answer wrong” behavior.

```javascript
function startTimer(time) {
  counter = setInterval(timer, 1000);
  function timer() {
    timeCount.textContent = time; //change the value of timeCount with time value
    time--; //decrement the time value
    if (time < 9) {
      //if timer is less than 9
      let addZero = timeCount.textContent;
      timeCount.textContent = "0" + addZero; //add a 0 before time value
    }
    if (time < 0) {
      //if timer is less than 0
      clearInterval(counter); //clear counter
      timeText.textContent = "Time Off"; //change the time text to time off
      const allOptions = option_list.children.length; //get all option items
      let correcAns = questions[que_count].answer; //get correct answer from array
```
