Vandana Agarwala
CS2 Final Project - Othello AI
March 2018

README - 

So I've written an (admittedly really bad) Othello AI before, because I coincidentally chose to do so for my final project in APCS in high school.  So for me, this project was less about writing a basic minimax and more about optimizing it.  The most useful part about this was that I've thought about the problem before - about good heuristics, importance of different factors, etc.

First, I completely changed the board to instead use bitwise operations.  We can express any board uniquely as two 64-bit integers, one containing the positions of the white discs and one for the black discs.  We then implement everything (flipping stones, counting pieces, etc) as bitwise operations.  This speeds everything up.

Next, I implemented the negascout search algorithm, which uses alpha-beta pruning.  The thing about negascout, though, is that its optimality depends on the order in which we search through moves.  Assuming that the first move it looks at is the best, it is able to eliminate more moves than regular alpha-beta.  So to determine the order in which to search moves, I implemented a transposition table, which is basically memoization but applied to this context.  Each entry records the three best moves and the depth to which they were searched.  Then it prevents us from recomputing identical boards which have been reached in different ways through the decision tree.

Finally, the heuristics checked six characteristics:
- stone imbalance: how many stones each player has
- mobility: how many moves each payer has
- potential mobility: how many spaces there are around each player's pieces
- corners: how many corners each player has
- potential corners: how many corners each player can capture
- stability: how vulnerable a stone is to being captured by the opposite player
The importance of each of these characteristics also changes as time progresses.