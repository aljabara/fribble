# FRIBBLE - Using SPITBOL to trifle with words and to play Words With Friends

Fribble is a collection of SPITBOL programs related to word games such as Scrabble and Words With Friends (WWF).

The goal is to construct a program that can play WWF.

A copy of the offical rules for WWF can be found in Appendix A.

##Representation of WWF playing board, tiles, etc.

The WWF board is a 15x15 grid, with rows 1..15 and columns 1..15.

We will encode the location of each cell as r*100 * c. So row 1 consists of cells 101,102, ... 115. Row 2 consists
of cells 201,202, ..., 215.

The game is played with tiles, each representing a letter, and 'blank' tiles that can be used
to represent any letter.  Each player has at most seven tiles at any turn. We refer to these tiles as the 'rack.'

At the end of a turn the board must contain only words that occur in the WWF dictionary.

In SPITBOL terms, we can think of the board as two sets of lines, with each line having 15 characters. The
rows form one set of lines, the columns form the other. So at the end of a turn -- reading from left to right for
the rows and top to bottom for the columns -- each line must contain only words in the WWF dictionary.

We need only maintain the list of rows, since the columns can be obtained once the rows are known. 
We define the initial board with

	rows = array(16)
board.1
	gt(i = i + 1, 15)			:s(board.2)
	rows[i] = dupl'-',15)			:(board.1)
board.2


Need function to check a line for validity:

	define('valid(line)...') which succeeds if line is all blank or contains only valid words, and fails
				otherwise.


util.sbl summary

	add(str,word add word to string prefixing with space if string not null
	backwords(dict) - return dictionary with words reversed
	getcolumns(rows) - return columns as array of lines corresponding to the columns
	getwords(filename) - read list of words in file
	getdict(filename) - read list of words from file and build table mapping words to non-zero value
	isword(word,words)) - return nonzero value if word is contained in table words
	less(str,ch) - return character from string
	prefix(s,p) - insert p as prefix to each word in s
	words(s) return number of words (separated by spaces) in s
	
Representation of board as two-dimensional array
	board = array(15,15)

	getrows(board)
	getcolumns(board)

# Study

The directory *study* contains various programs used to study the dictionary structure, to assist in
refining the brute force approach to make the WWF player faster.



#Appendix A - Words with Friends Rules

The Offical Rules for WWF can be found at:

http://www.zygnawithfriends.com/wordswithfriends/support/WWF_Rulebook.html

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

The ENABLE word list for WWF can be found at:

http://code.google.com/archive/p/dotnetperls-controls/downloads/enable1.txt

WWF also allows some additional words though this is no official list of them. File **wwf.txt** is a list of additional words
created by peusing some web sites and also based on actual playing experience For example, consider QI 
(force whose existence and properties are the basis of much Chinese philosophy and medicine).




