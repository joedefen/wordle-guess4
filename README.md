# WORDLE-GUESS4 Project

# Project Goal
To find the "best" four ordered, predetermined guesses to solve a NY Times **wordle** puzzle.

To find those four "canned" guesses efficiently, we use some heuristics including:
* each guess must add 5 more letters to the attempted letter set
* the six possible vowels must be split 2-2-1-1 or 3-1-1-1, and we give the algorithm intuitively good sets of vowels (rather than trying them all).
* using two lists of 5-letter words:
    * all the legal answers to **wordle**.
    * all the legal guesses to **wordle**.
* when the vowels are common, we restrict the considered words to the legal answers; otherwise the legal guesses
    * e.g., if looking for with only "y" as a vowel, we use the legal guesses list, but for "a", we use the legal answers.
    * this not only speeds up the algorithm, it prefers common words when it would not compromise the result.

## Scoring
Guesses are scored by how many letters from all the legal answers are exposed by the word. For the highest scoring set of four:
* **clear** -- reveals 30.8% of the letters after one guess.
* **bigot** -- reveals 51.6% of the letters after two guesses.
* **kynds** -- reveals 69.7% of the letters after three guesses.
* **whump** -- reveals 83.9% of the letters after three guesses.

Overall score is the sum of the last three scores which tilts the overall score by sequences that reveal letters soonest (disregarding the one guess score because guessing on the second try happens rarely).

## How to Use the Four "Best" Guesses
**Least Number of Guesses.** To minimize guesses, typically use the canned words in order until it seems there are no more than two answers (most often, requiring four exposed letters). Sometimes, swap the 3rd and 4th canned guesses if the latter seems more likely to reveal letters.

**Least Chance of Failing and Least Effor.** If just trying to solve the puzzle with the highest probability and least effort, then use the canned guesses until five letters are exposed or the canned guesses are exhausted. This prevents you from wasting attempts on low probability, premature wild stabs, and you must "guess cautiously" only twice and with the most information available.

## So, What are Other Good Scoring Sets of Four?
The top scoring sets of four canned guesses are in the file, 'final-2023-07-02.txt'. To recreate the file, you can run `./bestwords`.

To help decode the output, here is the last line (and the top overall score) and its interpretation:
```
2052 [308, 516, 697, 839] ['carle', 'lacer', 'recal', 'clear'] ['bigot'] ['kynds'] ['whump']
```
NOTE:
* `2052` is overall score (sum of the last three intermediate scores).
* `[308, 516, 697, 839]` are the intermediate scores; 308 is 10*percent; meaning 30.8% of the letters in the legal answers after one guess (like expressing a batting average).
* `['carle', 'lacer', 'recal', 'clear']` are 1st guess anagrams with the same score; so just pick your favorite.

## A Few Resources
* [Wordle - The New York Times](https://www.nytimes.com/games/wordle/index.html) - the "official" game.
* [Wordle Unlimited Practice Game | WordPlay](https://wordplay.com/) - play wordle 24/7 ;-)
