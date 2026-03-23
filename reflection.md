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

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

---

## 4. What did you learn about Streamlit and state?

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
