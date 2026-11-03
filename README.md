# KIDSWORDLE_FINAL_PRODUCT
Kids Wordle

A command-line version of the word game Wordle, made for primary school students and written in Python. Repository: github.com/LilyGil-sketch/WORDLE

Table of Contents
General Info
Technologies Used
Setup
Usage
How the Code Works
Room for Improvement
Acknowledgements

Kids Wordle is a word-guessing game that runs in the terminal. The computer secretly picks one of five simple words (APPLE, HAPPY, HOUSE, SMILE, TIGER), and the player has six tries to guess it.
After each guess, every letter turns green, yellow or grey to show how close the player is.
The original Wordle draws on thousands of words, which is too hard for young readers. This version keeps the same rules but uses a small set of simple words, shows them on the start screen, and replaces error messages with friendly tips.
The project is a code prototype built for a university creative coding subject. Its purpose is to demonstrate code literacy: every line of wordle.py is commented to explain what it does.
Technologies Used
Python 3.8 or newer (standard library only: random, json, os)
unittest (Python's built-in testing framework)
Visual Studio Code
Git and GitHub



Features
Two-pass scoring that colours repeated letters correctly, just like the real Wordle
Coloured board and keyboard drawn in the terminal with ANSI colour codes
Start screen that explains the colours and shows the five possible words
Friendly input checks – guesses that are the wrong length, contain numbers or repeat an earlier guess get a gentle "Oops!" tip instead of an error
Win messages that change with the number of guesses, from "WOW! First try - you're a word wizard!" to "Phew! Just in time - you did it!"
Saved scores – games played, win %, streaks and a guess bar chart, stored in stats.json
Backup word list built into the code, so the game still runs if words.txt is missing
Unit tests for the scoring, keyboard and word list
Screenshots

Example: guessing HAPPY when the secret word is APPLE

 H   A   P   P   Y
 ⬜  🟨  🟩  🟨  ⬜

The middle P is green (right spot). The second P is yellow, because APPLE has a spare P. The A is yellow (wrong spot), and H and Y are grey (not in the word).

<!-- To add a real screenshot: create an "img" folder in this repository, upload your screenshot into it, then replace this comment with: ![Kids Wordle in the terminal](img/screenshot.png) -->
Setup

Requirements

Python 3.8 or newer – download from python.org
A terminal (the VS Code terminal works well)

Get the project

Click the green Code button on this page, then Download ZIP (or clone the repository).
Unzip the folder and open it in VS Code (File > Open Folder).
Keep all the files together in the same folder.

Project files

File	Purpose
wordle.py	The game: scoring, classes and main loop
words.txt	The five words, one per line – edit to change them
test_wordle.py	Unit tests
stats.json	Created automatically after your first game to save scores
Usage

Open the terminal in VS Code (Terminal > New Terminal) and run:

bash (general label for terminal commands) mac uses "zsh"
python3 wordle.py



How to play

Press Enter on the start screen.
Type a 5-letter word and press Enter.
Use the colours to make your next guess:
🟩 Green = right letter, right spot
🟨 Yellow = the letter is in the word, but in a different spot
⬜ Grey = the letter is not in the word
Type quit at any time to end the round.

Run the tests

bash
python3 -m unittest test_wordle.py -v

Change the words

Edit words.txt and put one 5-letter word on each line:

apple
happy
house
smile
tiger
How the Code Works
What it does
load_words()	Reads words.txt and keeps only valid 5-letter words
score_guess()	The core algorithm – compares a guess with the answer and returns five colours
colour_tile()	Wraps one letter in an ANSI colour code
show_rules()	Shows the start screen and the five possible words
class Keyboard	Remembers each letter's colour; a green key never drops back to yellow
class Stats	Saves and loads scores in stats.json
class WordleGame	Runs one round: the board, valid guesses, win or lose
main()	Loads everything and asks "Play again?"

Scoring a guess – score_guess() works in two passes:

python
# PASS 1 - letters in exactly the right spot turn green
for i in range(WORD_LENGTH):
    if guess[i] == answer[i]:
        result[i] = CORRECT
    else:
        remaining[answer[i]] = remaining.get(answer[i], 0) + 1

# PASS 2 - a letter turns yellow only if a spare copy is left
for i in range(WORD_LENGTH):
    if result[i] == CORRECT:
        continue
    letter = guess[i]
    if remaining.get(letter, 0) > 0:
        result[i] = PRESENT
        remaining[letter] -= 1

The dictionary remaining counts the answer's letters that were not green. Each yellow uses up one copy, so a repeated letter is never coloured more times than it appears in the answer.



Room for Improvement
Make adult version or increase word bank 

Room for improvement:

Let teachers add their own word lists more easily

To do:

Easy and hard modes with different word lists
A version that runs in a web browser

Acknowledgements
This project was inspired by the word game Wordle, and by research on why puzzles like it are so popular (Pexman, 2022).
Game design ideas came from Crawford (2014); the word-list approach was informed by the Cookie Codes Wordle tutorial (James, 2022).
Python was learned with help from Madecraft (2024), Sweigart (2025) and Bunn (2021).
This README follows the layout of the README cheatsheet by Łyczywek (2018).



References

Bunn, T. (2021). Learn Python visually: Creative coding with Processing.py. No Starch Press.
Crawford, C. (2014). The art of computer game design. Internet Archive. https://archive.org/details/artofcomputergam00chri
James. (2022, December 26). Coding Wordle. Cookie Codes. https://cookiecodes.co.uk/coding-wordle/
Łyczywek, R. (2018, October 15). How to write a good README for your GitHub project? Bulldogjob. https://bulldogjob.com/readme/how-to-write-a-good-readme-for-your-github-project
Madecraft. (2024). Python for students [Video course]. LinkedIn Learning. https://www.linkedin.com/learning/
Microsoft. (n.d.). Visual Studio Code [Computer software]. https://code.visualstudio.com/
Pexman, P. (2022, January 26). Why do we love puzzles like Wordle, and are they good for our brains? PBS NewsHour. https://www.pbs.org/newshour/arts/why-do-we-love-puzzles-like-wordle-and-are-they-good-for-our-brains
Sweigart, A. (2025). Automate the boring stuff with Python: Practical programming for total beginners (3rd ed.). No Starch Press.
