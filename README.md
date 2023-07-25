# WORDLE-GUESS4 Project

## Project Goal
To find the "best" four "canned" guesses to solve a NY Times **wordle** puzzle as an "easy" human assist. Using these words can:
* nearly minimize the time spent,
* nearly maximize the odds of solving, and
* help lower the average number of attempts as a secondary goal.

> To play wordle optimally, you must craft the next word given all the know information and the statistics of remaining possibilities.  This strategy mostly eliminates that time consuming, tedious chore w/o sacrificing losing the game.

**Spoiler Alert.** Most people have favorite first words pulled from computer simulations or trial-and-error. But, using four canned words makes wordle too easy to solve.  If new to Wordle, then you can use these words as "training wheels", particularly if you try to lower your average tries by looking for opportunities to deviate from the canned words to minimize the average number of guesses.

**Suggested Human Stategy**:
* by default, play all four canned words and then guess; if you do this, then you will often solve on the 5th try, and if not, on the 6th.
* to lower your average attempts significantly:
  * start guessing the answer when you think it has been narrowed down to one or two words; this typically requires 4 known letters; possibly just 3 if some positions are known and the exposed letters are very helpful.
  * sometimes, it makes sense to reverse the 3th and 4th word; e.g., if word 4 ends in "y" and "e" has been eliminated from slot 4 and 5 and slot 5 is uncertain, then play word 4 play the word ending in "y".
 * starting to guess too early (e.g. when there are actually more than two possibilites) is the "trap" that loses most games; when you deviate from the canned words, reconsider after the first deviation if it seems you misjudged (and resume the unused canned words).
 * see more tips in the section below, "Additional Some Rules of Thumb".

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

## Top 30 Results
Here are the top 30 results.  Using the first row as an example, the columns are:
* `855` - the adjusted score weighing the factors describe above,
* `[317, ...]` - in batting average style, the percentages of letters revealed after each word (so 317 means 31.7% after playing the first word, "slice"),
* `slice` ... bumph - the four canned words
* `/20` - the number of unique letters in the four words (20 is the most possible)
* `ei-a-oy-u` - the vowel sequence of the four words.
```
855  [317, 588, 778, 940] slice graft wonky bumph /djqvxz ei-a-oy-u
856  [314, 598, 775, 941] slant drive chowk bumpy /fgjqxz a-ei-o-uy
856  [314, 603, 769, 946] slant fried bumpy chowk /gjqvxz a-ei-uy-o
856  [317, 592, 758, 955] slice grand bumpy fowth /jkqvxz ei-a-uy-o
857  [303, 567, 794, 956] slime prank botch fudgy /jqvwxz ei-a-o-uy
857  [309, 580, 794, 956] slide graft conky bumph /jqvwxz ei-a-oy-u
857  [309, 594, 779, 955] slide craft bungy whomp /jkqvxz ei-a-uy-o
857  [314, 603, 780, 946] slant fried chowk bumpy /gjqvxz a-ei-o-uy
857  [314, 609, 785, 955] slant bride whomp gucky /fjqvxz a-ei-o-uy
857  [314, 610, 787, 933] slant prime chowk judgy /bfqvxz a-ei-o-uy
857  [317, 592, 784, 939] slice grand boxty whump /fjkqvz ei-a-oy-u
857  [328, 567, 794, 956] shire blank compt fudgy /jqvwxz ei-a-o-uy
858  [303, 587, 790, 956] grant shied flock bumpy /jqvwxz a-ei-o-uy
858  [317, 594, 784, 946] slice draft wonky bumph /gjqvxz ei-a-oy-u
858  [317, 592, 779, 955] slice grand bufty whomp /jkqvxz ei-a-uy-o
859  [301, 572, 781, 956] shine graft block dumpy /jqvwxz ei-a-o-uy
859  [314, 609, 779, 955] slant bride gucky whomp /fjqvxz a-ei-uy-o
859  [317, 588, 779, 955] slice graft bundy whomp /jkqvxz ei-a-uy-o
859  [317, 592, 789, 955] slice grand fowth bumpy /jkqvxz ei-a-o-uy
860  [296, 610, 772, 949] prime slant fudgy chowk /bjqvxz ei-a-uy-o
860  [317, 620, 786, 935] slice grant bumpy vozhd /fjkqwx ei-a-uy-o
861  [296, 610, 787, 949] prime slant chowk fudgy /bjqvxz ei-a-o-uy
861  [303, 612, 778, 955] grant slide bumpy chowk /fjqvxz a-ei-uy-o
861  [317, 594, 779, 955] slice draft bungy whomp /jkqvxz ei-a-uy-o
862  [303, 612, 789, 955] grant slide chowk bumpy /fjqvxz a-ei-o-uy
864  [309, 612, 778, 955] slide grant bumpy chowk /fjqvxz ei-a-uy-o
864  [317, 588, 793, 955] slice graft downy bumph /jkqvxz ei-a-oy-u
865  [309, 612, 789, 955] slide grant chowk bumpy /fjqvxz ei-a-o-uy
866  [314, 610, 772, 949] slant prime fudgy chowk /bjqvxz a-ei-uy-o
867  [314, 610, 787, 949] slant prime chowk fudgy /bjqvxz a-ei-o-uy
```
All are good choices; I typically use:
```
858  [303, 587, 790, 956] grant shied flock bumpy /jqvwxz a-ei-o-uy
```
It scores decently, uses four quite normal words, and only "jqvwxz" (the six least frequent letters) are uncovered.

## Letter Frequencies
```
2315 answer words; 10767 unique letters
Showing for each letter:
 - % of all words w letter
 - % of words w letter having it in position (>100% reflects double-letters)

let  pct   1  2  3  4  5  sum [position-pcts]
=== ====  == == == == ==  ===
 e: 9.0%   7 23 17 30 40 = 117    # e prefers 5, then 4
 a: 8.0%  16 33 34 18  7 = 108    # a prefers 2 & 3
 r: 7.0%  13 32 19 18 25 = 107
 o: 6.0%   6 41 36 20  9 = 112    # o prefers 2 & 3
 t: 6.0%  22 12 17 21 38 = 110
 l: 6.0%  14 31 17 25 24 = 111
 i: 6.0%   5 31 41 24  2 = 103    # i prefers 2 & 3
 s: 5.0%  59  3 13 28  6 = 109    # s prefers 1, then 4
 n: 5.0%   7 16 25 33 24 = 105
 u: 4.0%   7 41 36 18  0 = 102    # u prefers 2 & 3
 c: 4.0%  44  9 12 34  7 = 106    # c prefers 1, then 4
 y: 3.0%   1  6  7  1 87 = 102    # y strongly prefers 5
 h: 3.0%  18 38  2  7 37 = 102    # h prefers 2 & 5
 d: 3.0%  30  5 20 19 32 = 106
 p: 3.0%  41 18 17 14 16 = 106
 g: 2.0%  38  4 22 25 14 = 103
 m: 2.0%  36 13 20 23 14 = 106
 b: 2.0%  65  6 21  9  4 = 105    # b prefers 1
 f: 1.0%  66  4 12 17 13 = 112    # f prefers 1
 k: 1.0%  10  5  6 27 56 = 104    # k prefers 5, then 4
 w: 1.0%  43 23 13 13  9 = 101
 v: 1.0%  29 10 33 31  0 = 103
 x: 0.0%   0 38 32  8 22 = 100    # x prefers 2 & 3
 z: 0.0%   9  6 31 57 11 = 114    # z prefers 4, then 3
 q: 0.0%  79 17  3  0  0 =  99    # q prefers 1, then 2
 j: 0.0%  74  7 11  7  0 =  99    # j prefers 1
```

## Additional Some Rules of Thumb
From [Any tips on scoring more 3's and 4's rather than 5's? : wordle](https://www.reddit.com/r/wordle/comments/12hkn3i/comment/jfpo4jj/?utm_source=share&utm_medium=android_app&utm_name=androidcss&utm_term=1&utm_content=share_button),
here are a few selected tips to add to the general guidance above.

* Observe where letters like to live (see comments above) ... this speeds up choosing non-canned guess.
* If E & R are both alive after your starting word, there's a good chance they are together in Slots 4 & 5 (---ER).
* If E is ruled out altogether or at least Slot 4 & 5, there is a good chance the word ends with Y (364 Solutions end in the letter Y).
* When you get 3 or 4 letters in position quickly, it may indicate there are many possibilities remaining; be very sure, and it may be best think of alternative using the letters you need to rule in or out.

## A Few Resources
* [Wordle - The New York Times](https://www.nytimes.com/games/wordle/index.html) - the "official" game.
* [Wordle Unlimited Practice Game | WordPlay](https://wordplay.com/) - play wordle 24/7 ;-)
* [Wordle Solver](https://jonathanolson.net/wordle-solver/) - the site does not provide any fun/challenge for you as its data entry clerk, but it suggests the lowest possible average guesses is 3.42 (when using a computer for every guess).
* [SCOREDLE](https://scoredle.com/) - grades your solution and makes it available for sharing.
* [r/wordle](https://www.reddit.com/r/wordle/) - subreddit for discussing wordle.
* [The best strategies for Wordle, part 2](https://sonorouschocolate.com/notes/index.php/The_best_strategies_for_Wordle,_part_2) - interesting article on the theory of computer strategies (and much more technical than this project).
