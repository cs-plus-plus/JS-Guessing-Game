# 🎯 AP Computer Science Principles Project: JavaScript Number Guessing Game

## 📘 Overview
In this project, you’ll design and code a **JavaScript Number Guessing Game** that runs entirely in the browser.  
Your program must follow the specifications below to meet the rubric and pass the automated GitHub Actions tests.  

The game should allow the user to:
- Select a difficulty level  
- Enter guesses until they get the correct number or give up  
- Track and display statistics like total wins, average score, and leaderboard  
- Show the current date and time (continuously updating)  

Your HTML elements, variable names, and function names must match the specifications below exactly — otherwise, the automated tests will not run correctly.

---

## 🗂️ Required Files
Your repository **must include** these two files in the root directory:

```
index.html
script.js
```

No additional folders or renaming (e.g., `/src`, `/scripts`) should be used.

---

## 🧩 Required HTML Structure

The tests rely on specific **IDs** and **element names**. Make sure these match exactly, including capitalization.

### Required Elements
| Feature | HTML Tag | ID / name | Notes |
|----------|-----------|------------|-------|
| Display current date and time | `<p>` | `id="date"` | Must show formatted date and live time |
| Level selector | `<input type="radio" name="level" id="e" value="3">` | name must be `"level"` | You must include **three** levels: Easy, Medium, Hard |
| Play button | `<button>` | `id="playBtn"` | Starts the game and generates random answer |
| Guess input | `<input>` | `id="guess"` | User types their guess here |
| Guess button | `<button>` | `id="guessBtn"` | Submits the current guess |
| Message area | `<h3>` | `id="msg"` | Displays feedback (“Too high”, “Correct”, etc.) |
| Wins display | `<p>` | `id="wins"` | Shows total number of games won |
| Average score display | `<p>` | `id="avgScore"` | Shows average number of guesses per win |
| Leaderboard list | `<ol>` | child `<li name="leaderboard">` | Must contain at least three `<li>` items |
| Optional Give Up button | `<button>` | `id="giveUp"` | Ends the game early and counts as loss |

### Example Base HTML
```html
<!DOCTYPE html>
<html>
  <head>
    <title>JavaScript Number Guessing Game</title>
  </head>
  <body>
    <p id="date"></p>

    <h3>Level</h3>
    <input type="radio" name="level" id="e" value="3" checked><label for="e">Easy</label>
    <input type="radio" name="level" id="m" value="10"><label for="m">Medium</label>
    <input type="radio" name="level" id="h" value="100"><label for="h">Hard</label>

    <button id="playBtn">Play</button>

    <h3 id="msg">Select a Level</h3>
    <input type="text" id="guess">
    <button id="guessBtn" disabled>Guess</button>
    <button id="giveUp" disabled>Give Up</button>

    <h3>Stats</h3>
    <p id="wins">Total wins: 0</p>
    <p id="avgScore">Average Score: </p>

    <h3>Leaderboard</h3>
    <ol>
      <li name="leaderboard">100</li>
      <li name="leaderboard">100</li>
      <li name="leaderboard">100</li>
    </ol>

    <script src="script.js"></script>
  </body>
</html>
```

---

## ⚙️ Required JavaScript Functions and Variables

The test suite expects **specific function names** and global variables.  
Be sure to use these names exactly.

### Global Variables
```js
const levelArr = document.getElementsByName("level");
let level, answer, score;
const scoreArr = [];
```

### Required Functions

| Function | Description | Notes |
|-----------|--------------|-------|
| `time()` | Returns formatted date and time as a string | Must use `Date()` and include month name and suffix (e.g., `March 1st, 2025, 2:30:45 PM`) |
| `play()` | Starts a new game | 1️⃣ Sets `answer` to random number 1–level <br> 2️⃣ Enables guess input/button <br> 3️⃣ Disables play button <br> 4️⃣ Displays “Guess a #1–(level)” |
| `makeGuess()` | Handles user guess | Compares input to `answer` and updates `msg` |
| `updateScore()` | Updates total wins, average score, and leaderboard | Sort scores ascending; display top 3 |
| `reset()` | Resets game controls | Re-enables difficulty radios and Play button |
| *(Optional)* `giveUp()` | Ends the round immediately | Sets score to range value (equal to level) |
| *(Optional)* `titleCase(name)` | Converts entered name to “Firstname Lastname” format | Used to personalize messages |

### Event Listeners
```js
playBtn.addEventListener("click", play);
guessBtn.addEventListener("click", makeGuess);
giveUp.addEventListener("click", giveUp); // optional
```

### Example `play()` Implementation
```js
function play() {
  score = 0;
  for (let i = 0; i < levelArr.length; i++) {
    if (levelArr[i].checked) {
      level = levelArr[i].value;
    }
    levelArr[i].disabled = true;
  }
  playBtn.disabled = true;
  guess.disabled = false;
  guessBtn.disabled = false;
  giveUp.disabled = false;

  answer = Math.floor(Math.random() * level) + 1;
  msg.innerHTML = "Guess a #1-" + level;
}
```

---

## 🧮 Required Game Features

Your program must include these **Minimum Requirements** to earn a full base score (70 points):

| Requirement | Description |
|--------------|-------------|
| ✅ Working guessing game | Player can play and win |
| ✅ Track total wins | Display count in `<p id="wins">` |
| ✅ Calculate average score | Display in `<p id="avgScore">` |
| ✅ Leaderboard (top 3) | Update `<li name="leaderboard">` elements |
| ✅ At least three levels | Easy, Medium, Hard radio buttons |
| ✅ Display current date and time | Update every second |
| ✅ Ask for player name | Input, formatted with correct case |
| ✅ Let user give up | Score = range value |
| ✅ Show hot/warm/cold feedback | Based on absolute difference |
| ✅ Rate user performance | “Good”, “OK”, or “Bad” message |
| ✅ Month name & suffix on date | “May 1st”, “June 2nd”, etc. |
| ✅ Track round time | Use `getTime()` for each round |
| ✅ Track fastest game | Display fastest time so far |
| ✅ Track total time & average time | Show in additional stats area |

---

## 🧪 Automated Testing
When you push your code to GitHub, the **GitHub Actions** workflow will automatically:

1. Load your `index.html` and `script.js`  
2. Simulate playing the game using virtual clicks and inputs  
3. Check whether each required element and function behaves correctly  
4. Output a **rubric-style grade report** under the “Actions” tab  

You’ll see something like:

| Check | Points | Max | Passed |
|--------|--------|------|--------|
| Current date & time shown | 4 | 4 | ✅ |
| Leaderboard (top 3, ascending) | 8 | 8 | ✅ |
| Give up sets score to range | 6 | 6 | ❌ |
| ... | ... | ... | ... |

Your total and percentage will also appear at the top of the report.

---

## 📦 Optional Advanced Features (“Above and Beyond”)

Earn up to **+6 bonus points** for creative or unique features such as:

- Animated feedback (color transitions, sound effects, etc.)
- Streak counter or achievements
- Local storage leaderboard
- Hints or difficulty scaling
- Responsive design with CSS media queries

Mark these elements with an attribute like:
```html
<div data-extra>Streak: 3</div>
```

---

## 🧭 Next Steps (24 pts @ 3 pts each)
The rubric also includes eight “next steps” checks.  
To earn these, include the following improvements:

| Step | Description |
|------|--------------|
| Reset Form | Add `<button id="reset" type="reset">Reset</button>` |
| Accessibility labels | Every input has a `<label for="...">` |
| Input validation | Handle invalid or blank guesses gracefully |
| Responsive layout | Add `<meta name="viewport">` in `<head>` |
| Semantic HTML | Use `<main>`, `<section>`, or `<footer>` |
| No console errors | Code runs cleanly |
| Meaningful commits | Commit messages describe progress |
| Extra polish | Any thoughtful improvement |

---

## 🧠 Tips for Success

- Always **test your game manually** before pushing.  
- Check that all required IDs and function names are exactly correct.  
- Use `console.log()` for debugging, then remove before submission.  
- Commit and push often—each push will re-run the tests automatically.  
- Use your creativity for bonus points but keep base features intact.

---

## ✅ Example Directory Structure

```
📦 guessing-game/
 ┣ 📜 index.html
 ┣ 📜 script.js
 ┗ 📜 README.md
```

---

## 🏁 Submission
1. Complete your project locally or in GitHub Codespaces.  
2. Commit all files and push to your GitHub repository.  
3. Wait 1–2 minutes, then open the **Actions** tab.  
4. Click the latest workflow run to view your automated grade report.  

If any tests fail, read the log to see which feature or ID needs fixing, correct it, and push again.
