# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
  1. Game showed me the 7 guesses and asked me for a number. I found that the reccomendation to go lower or higher was randomized. When I was meant to go lower, the app would tell me to go higher instead, and if I typed in the exact same number again, it would decide I should go lower.
  2. Clicking the show hint button hid the hint, and re-clicking it did not make the hint reappear.
  3. Going into easy difficulty reduced my number of guesses down to 6 (or 5?), which was less than normal mode attempts of 8 (or 7?).
  4. The hint section told me I was out of guesses 1 guess before I was actually out of guesses. If I looked at attempts section and saw, "Attempts left: 1", the hint section told me I was out of attempts. It would still let me make another attempt, so it is evident that the hint is off, and not the actual attempts.
  5. The new game buttom did not restart the game only when I ran out of attempts. If I chose to restart the game while I had any number of attempts left, I could click restart game and it would reset my attempts. When I ran out of attempts and chose to restart, the system would visually reset my attempts, but I could no longer submit my guess.
---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
 - I used claude, and I saw that the AI was able to correctly identiy the problem with the broken hint stated in problem 1. It was correct in explaining where the problem was, why it was broken, and how to fix it. I verified the result by testing the program again to see if entering the same guess would always give me the same correct hint suggestion.
 - I think Claude did pretty good overall for most of the bugs, and that may just be to me knowing the problem and identifying what I believe is causing it. I will say the worst offender I found was identifying problem 1. It explained to me that the logic was flipped for higher or lower, but it did not explain an additional issue related to problem 1 where the hint would flip even when entering the same number. That had to do with the comparisons of string and int using streamlit, so its kind of a fail on Claude, but also it wasn't what I was asking about.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
As mentioned previously, I tested the application with test cases where I knew what the correct expected output was. In problem 1, I knew that entering 5 when the target was 10 would result in the hint telling me to go higher. Even if I re-entered 5 again, the expected hint output should always be higher. 
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
Again, I tested the application by entering in 5 when the target was greater than five, and I verified that the hint suggested was to go higher rather than lower. I also verified that this was consistent for every input by re-entering 5 to see if it was random luck that I got the correct expected output. 
- Did AI help you design or understand any tests? How?
Absolutely AI helped me understand tests. By explaining WHY the code was broken, it gave me insight into how I should design my test cases. If I was randomly clicking and not understanding the entire codebase, I may have thought that problem #1 was that the hint told me to go the opposite direction of where I was meant to go. If I had 5 and the target was 10, I may have entered in 5, seen it say go lower, and assumed it was simply a flipped suggestion. With AI and its explanation, I was able to see that the hint was truly just randomized, and that let me know one way to test the code after fixing the bug.
---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
From my understanding, it seems that streamlit was refreshing the state after every action I took, and that meant the secret number being held would essentially get refreshed and reset in a way to a different random number.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
Reruns seem to be like refreshing the page on an app with no persistent state. If you typed something into a regular textbox and refreshed, you would go back and see what you have typed in dissapeared. Now imagine that refresh action with the textbox happening every time you clicked something, and also it affected every bit of information held.
- What change did you make that finally gave the game a stable secret number?
Using a dictionary session_state was the solution for this problem, as it is specifically meant to be a dictionary that persists between reruns. This way, you do not have to worry about the secret number getting reset everytime you made a guess or something like that.
---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
  Testing habits. I have not built my testings habits at all, as I always used my intuition to test things, but I defiinitely see the benefit of using AI to help with testcases now.
- What is one thing you would do differently next time you work with AI on a coding task?
  Maybe trying to read the code a bit on my own. I test the app like suggested, but I did not spend time looking through the functions and how they were connected together. For a small scoped project like this one, it was fine. For larger projects, though, I can definitely see myself getting lost as the AI explains some concept I didn't even know existed in the app.
- In one or two sentences, describe how this project changed the way you think about AI generated code.
  This project did make me realize how nice using AI to generate code was. I saw it using a similar structure for how to work through problems as me, and I recognize the benefits of specific tasks like test case creation. The one thing I am starting to realize is that requirements and documentation seem to be very important, as Claude will spend lest time trying to understand what I want, and instead spend more time solving my problems with me.