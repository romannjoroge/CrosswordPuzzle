# Crossword Puzzle 

As I was at my grandmother's house I saw the crossword puzzle below, I also noticed that my mum does these challenges:

![Example of crossword](./cucu_crossword.jpg "Example of crossword")

Instead of being given hints of what the word is, you're given the letters that are in the word. Each of these letters are numbered 1 - 26. The aim of the crossword is to find the letter for each of these numbers. 

To begin with you're given 4 of the letters as a hint.

This looked like a crossword puzzle that could be perfect for a computer to solve!

## My understanding of the problem

The crossword is made up of a list of words where each number is assigned to letter. Each number is assigned to a unique letter.

These words are in a *horizontal or vertical line*. 

```
Vertical line = {(x,y) | x = constant, start <= y <= end, start > end}
```

```
Horizontal line = {(x,y) | y = constant, start <= x <= end, start > end}
```

A cell can be in **at most 2 words** and the **lines of these words can't overlap**.

At the beginning of the crossword we only know 4 letters for sure, the rest need to be found.

*We know the crosswords is solved if all of the words in the crossword are in a **all_found** state*. A word can be in one of 4 states:

```
state(word) => {
                no_found  , if none of the numbers in the word have letter
                some_found, if some of the numbers in word have letter
                all_found , if all of the numbers in word have letter and it is in dictionary
                invalid   , if all numnbers in word have letter but it isn't in dictionary
               }
```

## Possible Algorithm

We can use the possible algorithm below to solve the crossword:

1. Get words in crossword
2. For each word, process it
3. Repeat until all words are in **all_found** state.

To get words in the crossword, we can **go through all of the cells and check for possible words** on its horizontal and vertical line. *A word, x,  should be added if there isn't any other word, y,  whose line overlaps with x*.

```
get_word(cell) => {
                    skip, if cell is not a letter
                    skip, if words already exist
                    add word, if word didn't exist
                  }
```

To process a word we can do the following:

```
process(word) => {
                    skip, if state(word) = no_found
                    find_match(word), if state(word) = some_found
                    skip, if state(word) = all_found
                    unassign(word), if state(word) = invalid
                 }
```

A matching word is a word that has the same length and same letters for each of the known letters, it also respects rules of different letters e.g. if word is (1, 2, 3) it has 3 different letters following each other. After a matching word is found the letters for numbers found is updated

When a word is unassigned, the latest number found in the word is unassigned and the next word is processed.