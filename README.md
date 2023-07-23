# WORDLE-GUESS4 Project

## Project Goal
To find the "best" four "canned" guesses to solve a NY Times **wordle** puzzle as an "easy" human assist. Using these words can:
* nearly minimize the time spent,
* nearly maximize the odds of solving,
* help lower the average number of attempts, and
* find good solutions relatively quickly (i.e., no overnight runs, use only python, etc.).

**Suggested Human Stategy**:
* by default, play all four canned words and then guess; if you do this, then you will often solve on the 5th try, and if not, on the 6th.
* to lower your average attempts significantly:
  * start guessing the answer when you think it has been narrowed down to one or two words; this typically requires 4 known letters; possibly just 3 if some positions are known and the expose letters are helpful (e.g., consonants are usually more helpful).
  * sometimes, it makes sense to reverse the 3th and 4th word.
 * starting to guess too early (e.g. there are actually more than two possibilites) is the "trap" that loses most games; when you deviate from the canned words, reconsider after the first deviation if it seems you misjudged (and resume the unused canned words).


## Program Design
### Internal Heuristics
To find  four "canned" guesses efficiently, we use some heuristics including:
* each guess must add 5 more letters to the attempted letter set, except for the 4th which may expose as few as 3 more letters.
* exposing all the vowels by giving the algorithm intuitively good sets of vowels (rather than trying them all); the six possible vowels must be split 2-2-1-1 or 3-1-1-1, and, for example, "u" belongs in the 3rd or 4th word intuitively.
* using two lists of 5-letter words:
    * all the legal answers to **wordle**.
    * all the legal guesses to **wordle**.
* when the vowels are common, we restrict the considered words to the legal answers; otherwise the legal guesses
    * e.g., if looking for with only "y" as a vowel, we use the legal guesses list, but for "a", we use the legal answers.
    * this speeds up the algorithm, and it prefers more common words when the word set is bountiful.

### Scoring
Without all the gory details, the scoring favors
* words with letters in the most frequent position (i.e. a word with "s" is favored if "s" is in the first position where it is found most often)
* sets of words that expose the most letters sooner rather than later.

### Summary of Results
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
* [Wordle Solver](https://jonathanolson.net/wordle-solver/) - the site does not provide any fun/challenge for you as its data entry clerk, but it suggests the lowest possible average guesses is 3.42 (when using a computer for every guess).
