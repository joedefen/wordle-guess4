# WORDLE-GUESS4 Project

## Project Goal
To find the "best" four "canned" guesses to solve a NY Times **wordle** puzzle as an "easy" human assist. Using these words can:
* nearly minimize the time spent,
* nearly maximize the odds of solving, and
* help lower the average number of attempts as a secondary goal.

> To play wordle optimally, you must craft the next word given all the know information and the statistics of remaining possibilities.  This strategy mostly eliminates that time consuming, tedious chore w/o sacrificing losing the game.

Optionally, the "best" three "canned" guesses can be generated.  The trade-offs of using three versus four are:
* With three, more letters are exposed first, and your chance using fewer guesses improves.
* But with three, your chance of failing to solve goes up since you are left to your vocabulary and wits after testing only 15 letters (not 20).

**Spoiler Alert.** Most people have favorite first words pulled from computer simulations or trial-and-error. But, using four canned words may make wordle "too easy to solve".  If new to Wordle, then you can use these words as "training wheels", particularly if you try to lower your average tries by looking for opportunities to deviate from the canned words to minimize the average number of guesses.

**Suggested Human Stategy**:
* by default, play all four [three] canned words and then guess; if you do this, then you will often solve on the 5th or 6th [4th, 5th, or 6th] try.
* to lower your average attempts significantly:
  * start guessing the answer when you think it has been narrowed down to one or two words; this typically requires roughly three known letters; knowing positions and consonants help solve with fewer clues.
 * starting to guess too early (e.g. when there are actually more than two possibilites) is the "trap" that loses most games; when you deviate from the canned words, reconsider after the first deviation if it seems you misjudged (and resume the unused canned words).
 * see more tips in the section below, "Additional Some Rules of Thumb".

## Program Design
### Internal Heuristics
To find  four "canned" guesses efficiently, we use some heuristics including:
* each guess must add 5 more letters to the attempted letter set, except for the 4th which may expose as few as 3 more letters.
* exposing all the vowels by giving the algorithm intuitively good sets of vowels (rather than trying them all); the six possible vowels must be split 2-2-1-1 or 3-1-1-1, and, for example, "u" may belong in the 3rd or 4th word intuitively.
* using two lists of 5-letter words:
    * all the legal answers to **wordle**.
    * all the legal guesses to **wordle**.
* when the vowels are common, we restrict the considered words to the legal answers; otherwise the legal guesses
    * e.g., if looking for with only "y" as a vowel, we use the legal guesses list, but for "a", we use the legal answers.
    * this speeds up the algorithm, and it prefers more common words when the word set is bountiful.

### Scoring
Without all the gory details, the scoring favors
* words with letters in the most frequent slot (i.e. a word with "s" is favored if "s" is in the first slot where it is found most often)
* sets of words that expose the most letters sooner rather than later.
The option, "-x {EXPONENT}" will favor the right slot with higher values of EXPONENT. The default EXPONENT is 2 which strongly favors the right slot.

## Sample Top 30 Results for Four Words
Here are the top 30 results with default arguments.
Using the first row as an example, the columns are:
* `855` - the adjusted score weighing the factors describe above,
* `[317, ...]` - in batting average style, the percentages of letters revealed after each word (so 317 means 31.7% after playing the first word, "slice"),
* `slice` ... bumph - the four canned words
* `/20` - the number of unique letters in the four words (20 is the most possible)
* `ei-a-oy-u` - the vowel sequence of the four words.
```
2832  [244, 517, 715, 949] slimy front whack pudge /bjqvxz iy-o-a-ue
2833  [242, 507, 734, 955] shiny brawl compt fudge /jkqvxz iy-a-o-ue
2834  [212, 495, 725, 955] showy print black mudge /fjqvxz oy-i-a-ue
2834  [244, 495, 729, 956] slimy frank potch budge /jqvwxz iy-a-o-ue
2835  [253, 481, 721, 942] briny smowt chalk fudge /jpqvxz iy-o-a-ue
2836  [242, 451, 722, 927] shiny block graft muxed /jpqvwz iy-o-a-ue
2838  [212, 436, 725, 946] showy brick plant fumed /gjqvxz oy-i-a-ue
2838  [244, 471, 722, 956] slimy botch frank pudge /jqvwxz iy-o-a-ue
2839  [253, 490, 710, 931] briny shack plotz fudge /jmqvwx iy-a-o-ue
2840  [244, 508, 735, 956] slimy prank botch fudge /jqvwxz iy-a-o-ue
2841  [212, 458, 722, 956] blimy shank croft pudge /jqvwxz iy-a-o-ue
2842  [235, 508, 735, 956] bliny shark compt fudge /jqvwxz iy-a-o-ue
2842  [253, 488, 712, 946] briny sowth flack pudge /jmqvxz iy-o-a-ue
2843  [212, 436, 725, 955] showy brick plant mudge /fjqvxz oy-i-a-ue
2845  [244, 442, 715, 942] slimy whack front budge /jpqvxz iy-a-o-ue
2846  [253, 515, 712, 917] briny slack fowth judge /mpqvxz iy-a-o-ue
2848  [253, 523, 721, 942] briny smolt whack fudge /jpqvxz iy-o-a-ue
2850  [212, 485, 722, 956] blimy front shack pudge /jqvwxz iy-o-a-ue
2851  [253, 485, 725, 946] briny swopt chalk fudge /jmqvxz iy-o-a-ue
2854  [212, 449, 722, 927] blimy shack front judge /pqvwxz iy-a-o-ue
2854  [212, 495, 719, 946] showy print flack budge /jmqvxz oy-i-a-ue
2858  [244, 495, 722, 956] slimy frank botch pudge /jqvwxz iy-a-o-ue
2862  [253, 515, 712, 942] briny slack fowth mudge /jpqvxz iy-a-o-ue
2865  [251, 478, 729, 956] shily compt frank budge /jqvwxz iy-o-a-ue
2869  [212, 495, 725, 946] showy print black fudge /jmqvxz oy-i-a-ue
2877  [212, 436, 725, 946] showy brick plant fudge /jmqvxz oy-i-a-ue
2877  [253, 515, 712, 946] briny slack fowth pudge /jmqvxz iy-a-o-ue
2879  [244, 517, 715, 942] slimy front whack budge /jpqvxz iy-o-a-ue
2886  [212, 449, 722, 956] blimy shack front pudge /jqvwxz iy-a-o-ue
2902  [251, 502, 729, 956] shily frank compt budge /jqvwxz iy-a-o-ue
```
All are good choices; I typically use:
```
2858  [244, 495, 722, 956] slimy frank botch pudge /jqvwxz iy-a-o-ue
```
It scores decently overall, uses four quite normal words, exposes the nearly the most letters, and only "jqvwxz" (the six least frequent letters) are uncovered.  If you're OK with wierd words, shily-frank-compt-budge scores best.

## Sample Top 30 Results for Three Words
This run is using `bestwords -3 -x0.5`:
```
817  [353, 632, 830] crane doilt spumy /bfghjkqvwxz ae-io-uy 3 [3, 0, 0]
817  [353, 597, 818] crane slimy fouth /bdgjkpqvwxz ae-iy-ou 4 [4, 1, 1]
817  [353, 597, 827] crane slimy tough /bdfjkpqvwxz ae-iy-ou 4 [4, 1, 2]
818  [312, 614, 828] brine slaty pouch /dfgjkmqvwxz ei-ay-ou 3 [2, 0, 3]
818  [364, 608, 830] crate slimy pound /bfghjkqvwxz ae-iy-ou 4 [3, 1, 4]
818  [364, 606, 823] crate shiny would /bfgjkmpqvxz ae-iy-ou 5 [5, 1, 1]
819  [334, 585, 831] shale pricy mount /bdfgjkqvwxz ae-iy-ou 3 [3, 1, 1]
819  [364, 615, 823] crate shily wound /bfgjkmpqvxz ae-iy-ou 5 [5, 0, 4]
819  [361, 612, 820] slate pricy wound /bfghjkmqvxz ae-iy-ou 4 [2, 2, 4]
819  [361, 614, 810] slate briny vouch /dfgjkmpqwxz ae-iy-ou 3 [2, 2, 3]
820  [364, 615, 830] trace shily bound /fgjkmpqvwxz ae-iy-ou 4 [2, 0, 4]
820  [364, 615, 837] trace shily pound /bfgjkmqvwxz ae-iy-ou 4 [2, 0, 4]
820  [353, 634, 830] crane sluit podgy /bfhjkmqvwxz ae-iu-oy 4 [4, 1, 0]
820  [361, 614, 816] slate briny dough /cfjkmpqvwxz ae-iy-ou 2 [2, 1, 1]
821  [334, 602, 837] shale point crudy /bfgjkmqvwxz ae-io-uy 3 [3, 1, 0]
821  [364, 615, 824] crate shily found /bgjkmpqvwxz ae-iy-ou 5 [5, 0, 4]
821  [361, 612, 821] slate pricy found /bghjkmqvwxz ae-iy-ou 4 [2, 2, 4]
821  [361, 634, 824] slate crony guimp /bdfhjkqvwxz ae-oy-iu 3 [3, 1, 0]
822  [364, 606, 833] crate shiny mould /bfgjkpqvwxz ae-iy-ou 4 [4, 1, 1]
822  [361, 612, 837] slate pricy hound /bfgjkmqvwxz ae-iy-ou 4 [2, 2, 4]
823  [364, 615, 833] crate shily mound /bfgjkpqvwxz ae-iy-ou 4 [4, 0, 4]
823  [361, 612, 830] slate pricy mound /bfghjkqvwxz ae-iy-ou 4 [2, 1, 4]
824  [353, 604, 830] crane shily doubt /fgjkmpqvwxz ae-iy-ou 5 [5, 0, 0]
826  [364, 615, 830] crate shily bound /fgjkmpqvwxz ae-iy-ou 5 [5, 0, 4]
826  [364, 615, 837] crate shily pound /bfgjkmqvwxz ae-iy-ou 4 [4, 0, 4]
826  [361, 612, 827] slate pricy bound /fghjkmqvwxz ae-iy-ou 4 [2, 2, 4]
827  [361, 614, 824] slate briny mouch /dfgjkpqvwxz ae-iy-ou 3 [3, 2, 3]
828  [361, 614, 824] slate briny gouch /dfjkmpqvwxz ae-iy-ou 3 [3, 1, 3]
828  [361, 614, 824] slate briny cough /dfjkmpqvwxz ae-iy-ou 3 [3, 1, 1]
831  [361, 614, 828] slate briny pouch /dfgjkmqvwxz ae-iy-ou 3 [3, 2, 3]
```
After using 'SLATE-BRINY-POUCH', you know 83% of the letters (versus 73% with the best four canned words). So, you learn more quickly and have a better chance of solving with fewer guesses (but not necessary less time spent).

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
