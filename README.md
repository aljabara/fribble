# FRIBBLE - Using SPITBOL to trifle with words and to play word games with your friends

Fribble is a collection of SPITBOL programs created to have fun with -- and play --  word games such as Scrabble and Words With Friends (WWF).

The original goal was to construct a program that can play WWF.  A copy of the offical rules for WWF can be found in Appendix A.

FRIBBLE is licensed under the GNU GENERAL PUBLIC LICENSE V2 (or later).

This means you can use the code under any of the following license terms:

  GPL v2
  GPL v2 (or later)
  GPL v3
  GPL v3 (or later)

##Strategy

Fribble's strategy is at its core "brute force" in that each new move is determined by generating **all** possible moves and then picking the one that has a score at least as high as any other.

The reasoning behind this approach is based on the observation that each new move will consists of at most about 10000 possible permutations of the tiles in the rack that can be placed starting at a given blank cell.  If we consider all moves, then there are 7! (about 5,000) ways to play seven tiles, 6! to play six tiles, and so forth. This gives about 7! + 6! ... +1! possibilities (about 6,000).

As the game progresses there will be fewer and fewer blank cells to consider.

While this at first sight a large space to search, the number of  moves is limited by the size of the dictionary  -- about 180,000 words --  and the structure of English. 

For example, consider the number of plural words in the dictionary, that is words such adding 's' at the end of
the word results in a word that is also in the dictionary.  There are just under 50,000 plurals in the ENABLE list, 
which is about 30% of the total.

Almost all the possible moves will consist of nonsense strings that are  not in the dictionary.   Consider for example a  move that starts with 'zqiij.' We can find such nonsense strings by constructing a list of all the possibilites for the first four characters in a valid word, and so forth.

SPITBOL is very fast, or at least fast enough. The game is not played in real time, but over the internet, so that it is acceptable to take minutes, if not hours, to find the best move for a given position.

The first version of Fribble takes about 20 seconds to find a move, using a circa-2011 64-bit x86-64 processor.


## Usage 

Fribble can be used to play wwf in three ways:

- **self**
  In *self* mode, Fribble plays against itself. This is primarily used to test the program.

- **solo**
  In *solo* mode, you play against Fribble. This is similar to the *solo* game optin available in wwf.

- **team**
  In *team* mode, you and Fribble play as a team against a foe. You enter the foe's moves and your tiles, and
Fribble finds the best move for you to play.

Fribble is shipped with two binary versions of the SPITBOL system:

- **sbl** SPITBOL for Unix/Linux.
- **sbl_osx**  SPITBOL for OSX. If you are using OSX, copy *sbl_osx* to *sbl*.

Here are some sample usages:

```
	sbl fribble.sbl -uself
	sbl fribble.sbl -usolo
	sbl fribble.sbl -uteam
```

When using *solo* or *team* modes you need to enter the tiles for your rack and moves. To enter a tileset, just type in up to
seven characters indicating your current tileset.

Moves can be entered in one of two ways:

- Use *m(row/col,pos,'text')* for a move in which all the tiles are played next to each other.

- Use *mf(row/col,free,'text')* for a move in which not all the tiles are played next to each other.

The first argument to each is a row or column specification:

- A row specification is one of: *r1*, *r2*,..., *r10*, ... , *r15* or *r01*, *r02*, ... *r10*, ..., *r15*.

- A column specification is one of: *c1*, *c2*,..., *c10*, ... , *c15* or *c01*, *c02*, ... *c10*, ..., *c15*.

- *pos* gives the starting position in the row or column.

- *'text'* give the tiles (letters) to be played.

- *free* is a list of the free (open) cells used in the move.

Examples:

```
  m(r8,8,'fribble') plays the word *fribble* in row 8, starting at position 8.
  m(c8,9,'riends') plays the string *riends* in column 8, starting at position 9, making the word 'friends' in column 8.
  mf(c13,'7,9,10','pay') plays the string 'pay' in column 13, at positions 7, 9 and 10, making the word 'play' in column 13.
```







# Wordplay

The [Wordplay project](http://github.com/daveshields/wordplay/) contains various programs used to 
study the dictionary structure, and to explore other issues of interest in the early days of writing Fribble.


#Appendix A - Words with Friends Rules

The Offical Rules for WWF can be found at:

http://www.zyngawithfriends.com/wordswithfriends/support/WWF_Rulebook.html

1. Overall Objective

    Players exchange turns forming words horizontally or vertically on the board, trying to score as many points as possible for each word.

2. Tile Placement

  1. The first word must be placed so that one of the tiles is on the star in the center of the board.

  2. Every word following that must be placed so that at least one tile is shared from an existing word on the board.

  3. Tiles can only be placed in the same line vertically or horizontally each turn. (The rules don't state,
 but experience confirms, that no spaces are allowed between the placed tiles.)

  4. Tiles can be placed so that multiple new words are formed simultaneously using neighboring letters.

  5. Words cannot be placed if they create an illegal word using neighboring letters.

  6. All words labeled as a part of speech (including those listed of foreign origin, and as archaic, obsolete, colloquial, slang, etc.)
       are permitted with the exception of the following: proper nouns (words always capitalized), abbreviations, prefixes and suffixes
       standing alone or words requiring a hyphen or an apostrophe.

3. Scoring

  1. Double the value of any tiles that were played this turn on a Double Letter (DL) space, and triple the value of 
any tile that was played on a triple letter (TL) TL space this turn. 
Do not double the value of tiles on DL and TL spaces for tiles that were played on previous rounds.

  2. Add up the values of all letters in the word, even if some were played on a previous turn.

  3. Double the value of the word if any tiles this turn were played on a DW space (and double it again 
in the case were two DW spaces were played upon). Triple the value of the word if any tiles this turn were played on a 
TW space (and triple it again if two TW spaces were used). Do not multiply words if tiles on DW or 
TW spaces were used from a previous turn.

  4. It is possible to create multiple words with the same play. In this case, score each new word separately,
 including bonuses, and sum all of the new words together.  

  5. Words cannot be placed if they create an illegal word using neighboring letters.

  6. Thirty-five bonus points are awarded whenever a player uses all seven tiles on their rack in a single turn.

4. End Game

  1. The game ends when one player plays every tile in his rack, and there are no tiles remaining to draw from.
The game could also end if three successive turns have occurred with no scoring and as long as the score is not zero-zero.

  2. After the last tile is played, the opposing player will lose points equal to the sum of the value of his remaining tiles.
This amount is then awarded to the player who placed the last tile.

5. Dictionary

Words With Friends has more than 173,000 acceptable words for use in the game. Our list is based on the Enhanced North American Benchmark

   Lexicon (ENABLE), a public domain list used by many word games.  

The ENABLE word list for WWF has been copied to file 

	enable1.txt

in the fribble main directory.

WWF also allows some additional words though this is no official list of them.  For example, consider QI 
(force whose existence and properties are the basis of much Chinese philosophy and medicine).

A list of such words, created by peusing some web sites and also based on actual playing experience, can be
found in the definition of the variable *g.wwf* in file *util.sbl*.




