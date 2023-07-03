# WORDLE-GUESS4 Project

# Project Goal
To find the "best" four ordered guesses to solve a NY Times **wordle** puzzle.

To find those four guesses efficiently, we use some heuristics including:
* each guess must add 5 more letters to the attempted letter set
* the six possible vowels must be split 2-2-1-1 or 3-1-1-1, and we give the algorithm intuitively good sets of vowels (rather than trying them all).
* we use two lists of 5-letter words:
    * all the legal answers to **wordle**.
    * all the legal guesses to **wordle**.
* when the vowels are common, we restrict the attempted words to the legal answers; otherwise the legal guesses
    * e.g., if looking for with only "y" as a vowel, we use the legal guesses list, but for "a", we use the legal answers.
    * this not only speeds up the algorithm, it prefers common words when practical.

## Scoring
Guesses are scored by how many letters from all the legal answers are exposed by the word. For example, the guesses ['abide', 'torch', 'gymps', 'flunk'] expose:
* 26.0% of the letters in the legal answers in one guess,
* 50.2% of the letters in the legal answers in two guesses,
* 66.7% of the letters in the legal answers in three guesses, and
* 84.0% of the letters in the legal answers in four guesses.

Overall score is the sum of the last three scores which weights overall goodness of the guesses by favor those that reveal the answer earliest (disregarding the one guess score because guessing on the second try happens rarely).

## How to Use the Four "Best" Guesses
**Least Number of Guesses.** In practice, I use the words in order but only until I think I can narrow down the word to just one or two possible answers. So, my goal is minimize tries w/o the risk of failing to solve the puzzle. Sometimes, I'll swap the order of the 3rd and 4th guesses if I can sense the 4th guess is more productive based on the imagined set of answers after the 2nd guess.

**Least Chance of Failing.** If just trying to solve the puzzle with the highest probability, then tring all four guesses and then solving is probably the strategy (i.e., it prevents you from wasting attempts on low probability answers when wrong about the number of remaining possible answers).

## So, What are the Best Four Guesses?
The top choices are in the file, 'final-2023-07-02.txt'. To recreate the file, you can run `./bestwords`.

To help decode the output, here is the last line (and the top overall score) and its interpretation:
```
2052 [308, 516, 697, 839] ['carle', 'lacer', 'recal', 'clear'] ['bigot'] ['kynds'] ['whump']
```
NOTE:
* `2052` is overall score (sum of the last three intermediate scores).
* `[308, 516, 697, 839]` are the intermediate scores; 308 is 10*percent; meaning 30.8% of the letters in the legal answers after one guess.
* `['carle', 'lacer', 'recal', 'clear']` are 1st guess anagrams with the same score; so just pick your favorite.

In summary, a set of words with top overall score (that I actually use and think is effective) is:
* **clear** -- reveals 30.8% of the letters after one guess.
* **bigot** -- reveals 51.6% of the letters after two guesses.
* **kynds** -- reveals 69.7% of the letters after three guesses.
* **whump** -- reveals 83.9% of the letters after three guesses.

## A Few Resources
* [Wordle - The New York Times](https://www.nytimes.com/games/wordle/index.html) - the "official" game.
* [Wordle Unlimited Practice Game | WordPlay](https://wordplay.com/) - play wordle 24/7 ;-)
