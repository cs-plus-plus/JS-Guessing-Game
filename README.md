# CS++ JavaScript — Guessing Game Project

> **Capstone Project** | 100 Points | No Autograding — Teacher Graded

This is the final JavaScript project. You will combine everything you have learned — variables, functions, arrays, loops, conditionals, DOM manipulation, event listeners, and the Date object — to build a complete number guessing game.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Requirements](#requirements)
3. [Required HTML Elements](#required-html-elements)
4. [JavaScript Functions](#javascript-functions)
5. [Scoring Rubric](#scoring-rubric)
6. [Starter HTML](#starter-html)
7. [Concepts Review](#concepts-review)
8. [Tips for Success](#tips-for-success)
9. [FAQ](#faq)
10. [Submission](#submission)

---

## Project Overview

Build a browser-based number guessing game where the player:

1. Selects a difficulty level (Easy 1-3, Medium 1-10, Hard 1-100)
2. Guesses until they find the correct number or give up
3. Sees feedback on each guess (hot, warm, cold, correct)
4. Tracks statistics: wins, average score, leaderboard, round timer
5. Sees a live clock with the current date and time

---

## Requirements

### Core Game (70 points)

- A working guessing game with at least **three difficulty levels**
- Random number generation within the selected range
- Feedback on each guess (too high, too low, correct)
- **Total wins** counter
- **Average score** (average number of guesses per win)
- **Leaderboard** showing the top 3 best scores (lowest guesses = best)
- **Current date and time** displayed on the page

### Additional Features (3 points each, 24 points total)

- Ask for the player's name, case it correctly, and use it in messages
- **Give Up** button that ends the round and sets the score to the range value
- **Hot/warm/cold** feedback based on how close the guess is
- Score quality feedback (tell the player if their score was good, average, or bad)
- **Date with month names and suffixes** (e.g., March 1st, July 2nd, June 3rd)
- **Live updating time** that shows seconds
- **Round timer** using `Date.getTime()` and display the fastest game
- **Average time per game** across all rounds played

### Above and Beyond (6 points)

Add extra features not listed above. Document what you added in your code with comments.

---

## Required HTML Elements

These IDs and names must match exactly.

| Feature | HTML Tag | ID / Name | Purpose |
|---------|----------|-----------|---------|
| Date/time display | `<p>` | `id="date"` | Shows formatted date and live time |
| Difficulty radios | `<input type="radio">` | `name="level"` | Three levels: Easy (3), Medium (10), Hard (100) |
| Play button | `<button>` | `id="playBtn"` | Starts a new round |
| Guess input | `<input>` | `id="guess"` | Where the player types their guess |
| Guess button | `<button>` | `id="guessBtn"` | Submits the current guess |
| Give Up button | `<button>` | `id="giveUpBtn"` | Ends the round immediately |
| Message area | `<h3>` | `id="msg"` | Feedback messages |
| Wins display | `<p>` | `id="wins"` | Total number of wins |
| Average score | `<p>` | `id="avgScore"` | Average guesses per win |
| Fastest game | `<p>` | `id="fastest"` | Fastest round time |
| Average time | `<p>` | `id="avgTime"` | Average time across all games |
| Leaderboard items | `<li>` | `name="leaderboard"` | Top 3 scores in an `<ol>` |

---

## JavaScript Functions

Use these exact function names:

| Function | Purpose |
|----------|---------|
| `time()` | Returns a formatted date/time string with month name, day suffix, and live time with seconds |
| `play()` | Starts a new game: generates random answer, enables inputs, records start time |
| `makeGuess()` | Handles a guess: compares to answer, shows feedback, tracks guess count |
| `updateScore()` | Updates wins, average score, and leaderboard after a win |
| `updateTimers(endMs)` | Calculates round time, updates fastest game and average time |
| `reset()` | Re-enables level selection and Play button for the next round |
| `giveUp()` | Ends the round, sets score to range value, updates all stats |

### Event Listeners

Wire your buttons with `addEventListener`:

```javascript
document.getElementById("playBtn").addEventListener("click", play);
document.getElementById("guessBtn").addEventListener("click", makeGuess);
document.getElementById("giveUpBtn").addEventListener("click", giveUp);
```

---

## Scoring Rubric

| Category | Points |
|----------|--------|
| Working guessing game with 3+ levels | 20 |
| Wins counter and average score | 15 |
| Leaderboard (top 3, sorted ascending) | 15 |
| Date and time display | 10 |
| Game feedback (too high/low/correct) | 10 |
| Player name with correct casing | 3 |
| Give Up button with range score | 3 |
| Hot/warm/cold feedback | 3 |
| Score quality feedback | 3 |
| Month names and day suffixes | 3 |
| Live seconds in time display | 3 |
| Round timer and fastest game | 3 |
| Average time per game | 3 |
| Above and beyond features | 6 |
| **Total** | **100** |

---

## Starter HTML

You may copy this into your `index.html` as a starting point:

```html
<!DOCTYPE html>
<html>
<head>
    <title>JavaScript Number Guessing Game</title>
    <script src="script.js" defer></script>
</head>
<body>
    <p id="date"></p>

    <h3>Level</h3>
    <input type="radio" name="level" id="e" value="3" checked>
    <label for="e">Easy (1-3)</label>
    <input type="radio" name="level" id="m" value="10">
    <label for="m">Medium (1-10)</label>
    <input type="radio" name="level" id="h" value="100">
    <label for="h">Hard (1-100)</label>

    <button id="playBtn">Play</button>

    <h3 id="msg">Select a Level and Press Play</h3>
    <input type="text" id="guess">
    <button id="guessBtn" disabled>Guess</button>
    <button id="giveUpBtn" disabled>Give Up</button>

    <h3>Stats</h3>
    <p id="wins">Total wins: 0</p>
    <p id="avgScore">Average Score: </p>
    <p id="fastest">Fastest Game: </p>
    <p id="avgTime">Average Time: </p>

    <h3>Leaderboard</h3>
    <ol>
        <li name="leaderboard">--</li>
        <li name="leaderboard">--</li>
        <li name="leaderboard">--</li>
    </ol>
</body>
</html>
```

---

## Concepts Review

This project uses everything from the previous assignments:

| Concept | Where It Is Used |
|---------|-----------------|
| Variables (`let`, `const`) | Score tracking, game state, timer values |
| Functions | `play()`, `makeGuess()`, `updateScore()`, etc. |
| Arrays | Leaderboard scores, sorting |
| Loops | Updating leaderboard display |
| Conditionals | Hot/cold feedback, win detection, input validation |
| DOM manipulation | `getElementById`, `textContent`, enabling/disabling buttons |
| Event listeners | Button clicks |
| Date object | Live clock, round timer, elapsed time |
| `setInterval` / `clearInterval` | Live updating clock with seconds |
| `Math.random()` / `Math.floor()` | Generating the random answer |
| `.toFixed()` | Formatting timer and average values |

### Day Suffixes

For the date display, add the correct suffix to the day number:

```javascript
function getDaySuffix(day) {
    if (day >= 11 && day <= 13) return "th";  // special cases: 11th, 12th, 13th
    switch (day % 10) {
        case 1: return "st";
        case 2: return "nd";
        case 3: return "rd";
        default: return "th";
    }
}

// Usage: "March 1st", "April 2nd", "May 3rd", "June 4th", "November 11th"
```

### Hot/Warm/Cold Feedback

Use the absolute difference between the guess and the answer:

```javascript
let diff = Math.abs(guess - answer);

if (diff === 0) {
    feedback = "Correct!";
} else if (diff <= 2) {
    feedback = "Hot!";
} else if (diff <= 5) {
    feedback = "Warm";
} else {
    feedback = "Cold";
}
```

### Sorting the Leaderboard

Keep an array of scores and sort them ascending (lowest = best):

```javascript
let scores = [8, 3, 15, 2, 7];
scores.sort(function(a, b) { return a - b; });
// scores is now [2, 3, 7, 8, 15]
// Display only the first 3
```

---

## Tips for Success

1. Build incrementally — get the basic guessing game working first, then add features one at a time
2. Test after every change — play a round, check the stats, try give up
3. Use `console.log()` liberally while developing to check your variable values
4. Keep your function names and element IDs exact
5. The leaderboard should sort scores ascending (fewer guesses = better score)
6. For the timer, use `new Date().getTime()` to capture milliseconds at the start and end of each round
7. Disable the Guess and Give Up buttons between rounds, and disable Play and level radios during a round
8. Handle edge cases: what if the user types nothing? A letter? A number outside the range?

---

## FAQ

**Q: Is this project autograded?**
No. This is a teacher-graded project. There are no automated tests — your teacher will review your code and play your game.

**Q: Do I have to implement all the additional features?**
You need the core game (70 points) plus enough additional features to reach your target grade. Each additional feature is worth 3 points.

**Q: How should the leaderboard work?**
Keep an array of all scores. After each game, add the score, sort the array ascending, and display the top 3 in the `<li>` elements. If fewer than 3 games have been played, show "--" for unfilled spots.

**Q: What should the Give Up button do?**
End the round immediately, set the player's score to the range value (e.g., 10 for Medium difficulty), update all stats and timers, and reset for the next round.

**Q: How do I make the time update every second?**
Use `setInterval` with a 1000ms delay:
```javascript
setInterval(function() {
    document.getElementById("date").textContent = time();
}, 1000);
```

**Q: Can I add CSS styling?**
Yes. Create a `style.css` file and link it in your HTML. Styling is encouraged and can count toward the "above and beyond" points.

---

## Submission

1. Commit and push your `index.html` and `script.js` to your GitHub repository
2. Enable **GitHub Pages**: Repository Settings > Pages > Deploy from branch > main > / (root)
3. Wait for the site to publish (you will see a link at the top of the Pages section)
4. Test your live page in the browser
5. Submit the GitHub Pages URL to your teacher

---

View all assignments and scoring breakdowns at [csplusplus.com/js-tests](https://csplusplus.com/js-tests)

*CS++ — AP Computer Science Principles — [csplusplus.com](https://csplusplus.com)*
