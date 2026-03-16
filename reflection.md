# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
When I first ran the game, I immediately noticed that there is a dropdown labeled Developer Debug Info, which most likely shouldn't be shown to the user. I also noticed that the show hint button is toggled on, so it will show the user a hint each time they guess. The game also lets the user know what to do and keeps track of how many attempts the user has left. On the left side of the website, I do notice that the attempts do not match.

- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
  The hints that it gave me after each guess I made lead me in the wrong direction. For the first playthrough, the secret number was 85 but I originally guessed 25 and it kept telling me to go lower. I also noticed that it tells me the secret number when I still had one more guess left. Once I use that last guess, it completely ends the game with a try again message even when I put the secret number it told me. When I press new game, I saw the number of guesses I have changes to 8, which is one more than I started with for the first game. Unfortunately, when I try to play the new game, it does not do anything. I also noticed that the message of "guess the number between 1 and 100." is not accurately reflected on which difficullty the user selected. Additionally, the number of attempts should go down by 1 after the first guess but instead it waits until the second guess.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
For this project, I uses Claude in VS Code. 

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
One example of an AI suggestion that was correct was when I had prompted Claude to explain the incorrect logic in app.py that caused the error of the attempts left number displaying being wrong. I prompted Claude to break it down in an easy to follow paragraph/bullet point format. Claude had suggested to move the attempts left statement in app.py to later on in the code. Claude explained the statement should be placed after a guess is validated and the game outcome logic finishes because it would update correctly on every rerun, acurrately showing the remaining attempts regardless of whether a guess was just submitted. Before accepting this edit, I looked through the code and made sure this is what the error was in logic. I had realized that when this statement is placed before the guess validation, it does not increment for the current guess which makes sense why it was off by 1. 

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
One example of an AI suggestion that was misleading was when I had prompted Claude to 
explain the incorrect logic in the code for why the secret number was still being shown as well as the Developer Debug Info window. Since these two bugs were intertwined in a way and Claude ignored the fact that I stated it should not be shown to the user, Claude had suggested to make a new variable called debug_mode which would track when the Develop Debug Info is shown to the user and when it shouldn't be through a toggle on the sidebar. Then with this new variable, I update the if-else conditional that stated if the user is playing then the secret is hidden, but if the user is not playing then the number is shown. This suggestion was very misleading as I looked through the code and realized if the information shouldn't be shown to the playyer at all, it can very well just be commented out. Claude did want me to do more work because it thought that I wanted the information to be shown sometimes, like in the cases of a Developer keeping track of their information. Insteead of accepting the edit, I commented out the if-else conditional so the player would not see it. 
---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
I first looked through the logic myself to see if Claude was hallucinating, but if I felt that like the bug could be fixed through Claude's suggestion, I edited it. When I fixed the bugs, I verified it was fixed by recreating the situation where it had first failed. When that error had been fixed, I attempted to find other errors through different test cases like as numbers out of bounds or empty inputs. For some of these fixes, I made sure the logic didn't break halfway through a game so I played until a new game to make sure the logic flow was correct.

- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
One test I ran checked that the "Too High" and "Too Low" logic in the check_guess function was working correctly. The secret number was 50 in this test and it was checked against the number 60. By using assert, I know that if the logic were to fail the issue is in the if-else conditional within the check_guess function. Since the code runs as it should, I know that the bug I fixed in the if-else statements correctly compares two values and points the player in the right direction with the hint.  

- Did AI help you design or understand any tests? How?
Claude did help me design my tests by including assert in my tests instead of me using print statements. Since I am more comfortable with print statements, I decided to use them for my tests but it was a bit difficult to know which error was for what test. Claude helped me understand why it would be better to use assert in this case, it also advised me to run tests at different times if I suspected something wrong for certain cases. Assert made the process a lot more faster because the computer handles checking for me so if something is wrong, I don't have to scroll and check, the tests flag the error for me. 

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
The secret number kept changing in the original app because when there is an interaction with the website, the Python code reruns from the start of the code. Within the code, the secret number was randomly generated, so when the page refreshes, the secret number would update and no longer be the same. From my understanding, this is just how Streamlit works. This bug really defeated the whole point of the game because it was unbeatable since the player would be guessing a secret number that is no longer the secret number.

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
I would explain reruns as when you accidentally switch tabs on a phone and when you go to the tab you were just on, you see it start up again so what you were doing is not right there so now you have to go and find it again. Essentially, a rerun starts from the top of the code when it detects any interaction with the code. A session state is like a saved draft or post on social media because when you hit save, the app knows that it must hold onto that information and shouldn't get rid of it. It holds onto it unti the user says it doesn't need it anymore. Essentially, a session state allows the code to remember some key aspects (in the game, the secret number or score) that shoud not be forgotten when a rerun happens.

- What change did you make that finally gave the game a stable secret number?
The secret number becomes stable because it is stored into the session state where it first checks if the secret number has not been saved. If it hasn't, then it randomly generates a secret number within the range that the difficulty the user chose states. If it has saved one already, then it skips this if statement and keeps the existing secret number. This prevents the code from updating the secret number when a new interaction occurs with the website, allowing the secret number to stay the same until the game is over. 

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
One habit I used in this project was prompting AI for specific output formats. This proved to be helpful because a lot of the time when AI has to go through a lot of information and context, it throws back a bunch of information back to the user. However, prompting Claude to format its explanations in small paragraphs and mainly bullet points made it easier for me to comprehend the logic and know where to look in my code exactly if it didn't immediately suggest an edit. 

- What is one thing you would do differently next time you work with AI on a coding task?
One thing I would do differently next time I work with AI on a coding task is breaking the code into smaller pieces for the AI to look at and understand. The AI looked at a lot of context because the file was a long piece of code and I noticed this with the amount of time it took for Claude to respond to me. Next time, I should suggest Claude to look at smaller pieces of code (like a function or an if-else conditional statement) so it can focus on that one part without bringing up new or old bugs that may not be relevant to fixing the one at hand.

- In one or two sentences, describe how this project changed the way you think about AI generated code.
This project really showed me that AI generated code can appear to be right, but it is always best for a human to inspect the logic concerns with the code and make sure the code actually makes sense as a whole (from smaller pieces of code to the whole block of code). It allowed me to test my code comprehension skills as I made sure Claude was offering actual support that helped push the game in the right direction.