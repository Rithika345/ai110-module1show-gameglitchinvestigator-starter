# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the hints were backwards").
Bug 1: The hints lie

Expected: If my guess is lower than the secret number, the hint should tell me to guess higher.

Actual: When the secret was 81 and I guessed 7, the game told me "Too Low, go LOWER!" which makes no sense and sends you in the wrong direction.

Bug 2: The New Game button is broken

Expected: Clicking "New Game 🔁" after winning or losing a round should reset the board and let me play again.

Actual: The game just gets stuck on the "Game over" or "You won" screen and locks you out from entering any new guesses.

Bug 3: The score goes up when you guess wrong

Expected: I should lose points for an incorrect guess.

Actual: Sometimes when I guess incorrectly and get a "Too High" message, my score actually goes up by 5 points instead of going down.
---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)? Gemini and Copilot
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
What the AI suggested: I asked Copilot why the New Game button was broken. It correctly identified that st.session_state.status wasn't resetting to "playing" and that the secret number was hardcoded to 1-100 instead of using the difficulty variables. It provided a refactored if new_game: block to reset all state variables properly.

Correct or Incorrect: Correct.

How I verified: I applied the code, clicked "New Game" in the live Streamlit app, and verified that the game allowed me to play a new round instead of freezing on the Game Over screen.

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
**What the AI suggested:** Before using Agent Mode, I asked Copilot how to fix the "Lying Hint" bug. Copilot suggested keeping the weird string conversion but adding a massive, complex `if/else` block to check string lengths and parse them back to integers.
**Correct or Incorrect:** Incorrect/Misleading.
**How I verified:** I read the proposed code and realized it was just a band-aid that made the code much messier. I rejected it and used Agent Mode to completely strip out the root cause (the unnecessary string conversion) instead.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

I decided a bug was fixed only when I could reproduce the exact scenario that broke it earlier and see the correct result in both the live app and my automated tests. For example, I ran a custom `pytest` case specifically asserting that `check_guess(7, 81)` returns "Too Low" instead of the old string-glitch behavior, which proved my core logic handled integer comparisons correctly. The AI was highly involved in this process; Copilot Agent Mode automatically updated my test file imports during the refactor to prevent my suite from breaking, and Gemini helped me draft the exact targeted `pytest` case to prove my fix worked. 

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

If I were explaining Streamlit to a friend, I'd say it redraws the entire app from top to bottom every single time you click a button or type something. Because it restarts constantly, the app basically has "amnesia" and forgets all your variables unless you explicitly tell it to save them. `st.session_state` is like a memory backpack the app wears so it can remember important things—like your current score, the secret number, and whether the game is over—across all those continuous screen refreshes.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

One habit I want to reuse is using inline `# FIX:` comments to immediately document why I accepted an AI's code change, which made tracking my refactoring steps much easier. Next time I work with AI, I will definitely double-check plain text and string outputs immediately; I assumed the AI would get basic English hints like "Higher/Lower" right, but it actually swapped them in plain sight! Ultimately, this project taught me that AI is a fast typist but a careless thinker, meaning I have to act as the lead engineer who rigorously reviews its logic rather than blindly trusting its output.