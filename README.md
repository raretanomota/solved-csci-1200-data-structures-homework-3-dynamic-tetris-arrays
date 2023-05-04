Download Link: https://assignmentchef.com/product/solved-csci-1200-data-structures-homework-3-dynamic-tetris-arrays
<br>
In this assignment you will use dynamically-allocated arrays to keep track of blocks on the 2D grid of the classic <em>Tetris </em>computer game. Follow these links to read about the history of the game and play an online interactive version: <a href="https://en.wikipedia.org/wiki/Tetris">http://en.wikipedia.org/wiki/Tetris</a> <a href="http://tetris.com/play-tetris/">http://tetris.com/play-tetris/</a>

There are 7 different piece shapes in the game of Tetris – each named by the letter that most closely matches its shape. Each piece is built from 4 small squares and can optionally be rotated <em>clockwise </em>by 90<sup>◦</sup>, 180<sup>◦</sup>, or 270<sup>◦</sup>, before being dropped onto the board. The different pieces are drawn below in their default orientations (0<sup>◦ </sup>rotation).

<strong>I       O         T           Z           S         L         J</strong>

In each step of the game, a piece will fall down vertically from the sky onto the board – stopping when it collides either with the bottom of the board, or with another piece. Below is a small example of game play.

<table width="676">

 <tbody>

  <tr>

   <td width="488">               <strong>0 </strong><strong>2 2 </strong><strong>0 0 0              0 2 </strong><strong>3 3 3 3              </strong><strong>0 2 3 3 </strong><strong>7 </strong><strong>3              0 2 3 </strong><strong>9 9 </strong><strong>3              </strong><strong>4 4 </strong><strong>3 9 9 3</strong>The sequence of commands on the right will create the above example.</td>

   <td width="188"><strong>4 4 3 9 9 3                 </strong><strong>3 3 2 8 8 0</strong></td>

  </tr>

  <tr>

   <td width="488">We start by constructing an empty board with width = 6. Then we drop 5 shapes onto the board using the add_piece member function. This function takes in 3 arguments: a single character naming the piece shape, an integer indicating piece rotation from default orientation, and an integer specifying the horizontal placement of the leftmost square of the piece. Each new piece is highlighted in green.</td>

   <td width="188">Tetris tetris(6); tetris.add_piece(‘O’, 0,1); tetris.add_piece(‘I’,90,2); tetris.add_piece(‘I’, 0,4); tetris.add_piece(‘O’, 0,3); tetris.add_piece(‘O’, 0,0);</td>

  </tr>

 </tbody>

</table>

The final two frames of the sequence above illustrate the scoring mechanism for Tetris. When a horizontal row stretching across the entire board is filled with blocks (no air gaps!), then that entire row (shown in red) is deleted. All squares above the deleted row are shifted down by 1 unit (or shifted <em>n </em>units if <em>n </em>rows were deleted). Note that we might be left with squares that are unsupported and floating. These unsupported squares <em>do not </em>fall after a score. The member function remove_full_rows should search the board for rows that are full and should be removed. This function returns the number of rows removed.

<table width="623">

 <tbody>

  <tr>

   <td width="550">In the illustrations above we track the integer height of each column of the board. This is not the count of how many squares are in each</td>

   <td width="73"> </td>

  </tr>

  <tr>

   <td width="550">column, but the height of the topmost square in that column.<strong>The Data Representation</strong></td>

   <td width="73"><strong>I</strong><strong>I</strong><strong>I</strong></td>

  </tr>

 </tbody>

</table>

<table width="133">

 <tbody>

  <tr>

   <td width="22"><strong>0</strong></td>

   <td width="22"><strong>2</strong></td>

   <td width="22"><strong>3</strong></td>

   <td width="22"><strong>3</strong></td>

   <td width="22"><strong>7</strong></td>

   <td width="22"><strong>3</strong></td>

  </tr>

 </tbody>

</table>

<table width="528">

 <tbody>

  <tr>

   <td width="459">column data.               <em>NOTE: You may not use the STL </em>vector <em>class for</em></td>

   <td width="62"> </td>

   <td width="7"> </td>

  </tr>

  <tr>

   <td width="459"><em>the implementation of this assignment.</em></td>

   <td width="62"><strong>width:</strong></td>

   <td width="7"><strong>6</strong></td>

  </tr>

 </tbody>

</table>

Your task is to implement a class named Tetris with a tetris.h header file and tetris.cpp implementation file. You are required to follow the specific memory layout diagrammed on the right (which corresponds to the 3rd step of the earlier example). The class has 3 member variables: the integer width, an array of integer column heights, and a two dimensional array structure holding the character <strong>heights:</strong>




As the game progresses and the board changes, the data structure must be updated. When we add the next piece we must first identify which columns increase in height and by how much. New column arrays of the appropriate size are dynamically allocated, data from the old column arrays are copied to the new arrays, and the new piece squares are filled in with the appropriate piece letter. The old arrays are deleted, pointers are shuffled, and the heights array is updated with the new column array sizes. Note that often pockets of air will be trapped under pieces. We will represent air with the space character.

<table width="245">

 <tbody>

  <tr>

   <td width="16"><strong>0</strong></td>

   <td width="16"><strong>2</strong></td>

   <td width="16"><strong>3</strong></td>

   <td width="16"><strong>9</strong></td>

   <td width="16"><strong>9</strong></td>

   <td width="16"><strong>3</strong></td>

   <td width="53"><strong>heights:</strong></td>

   <td width="16"><strong>4</strong></td>

   <td width="16"><strong>4</strong></td>

   <td width="16"><strong>3</strong></td>

   <td width="16"><strong>9</strong></td>

   <td width="16"><strong>9</strong></td>

   <td width="16"><strong>3</strong></td>

  </tr>

 </tbody>

</table>

<table>

 <tbody>

  <tr>

   <td width="14"></td>

  </tr>

  <tr>

   <td></td>

   <td></td>

  </tr>

 </tbody>

</table>

<strong>heights:</strong>

<strong>width:      6                                    width:   6</strong>




Similarly, when a full row is identified during scoring, all of the columns will decrease in height. You are required to re-allocate new, smaller arrays for every column and copy the remaining squares of data to the new arrays. <em>The board representation should always use the smallest size arrays possible. </em>The data structure for this assignment (intentionally) involves a lot of memory allocation &amp; deallocation. Certainly there are other implementation designs for the game of Tetris, and it is possible to revise this design for improved performance and efficiency. However, please implement the data structure <em>exactly </em>as presented. Our version of Tetris also allows us to increase or decrease the width of the board. Note that when the board is decreased in width, we may lose some squares. See the provided main.cpp for examples of these functions and the corresponding expected program output. Draw your own diagrams to understand which parts of the data structure must be reallocated and copied, and which parts can be reused just by changing pointers.

Finally, you will need to implement the destroy helper function to clean up all dynamically allocated member variables for the class so you don’t have any memory leaks. <em>Note: In the coming weeks, we will learn about C++ class destructors, copy constructors, and assignment operators. You don’t need to worry about them for this homework.</em>

<h1>Testing, Debugging, and Printing</h1>

We provide a main.cpp file with a wide variety of tests of the Tetris data structure. Some of these tests are initially commented out. We recommend that you get your class working on the basic tests, and then uncomment the additional tests as you implement and debug the remaining functionality. Study the provided test cases to understand the arguments and return values. We provide an ASCII art print function, and your board output should match the samples exactly to receive full marks on the submission server.

<em>Note: Do not edit the provided </em>main.cpp <em>file, except to uncomment the provided test cases as you work through your implementation and to add your own test cases where specified.</em>

We recommend using a memory debugging tool to find memory errors and memory leaks. Information on installation and use of the memory debuggers “Dr. Memory” (available for Linux/MacOSX/Windows) and “Valgrind” (available for Linux/OSX) is presented on the course webpage:

<a href="http://www.cs.rpi.edu/academics/courses/spring16/csci1200/memory_debugging.php">http://www.cs.rpi.edu/academics/courses/spring16/csci1200/memory_debugging.php</a>

The homework submission server will also run your code with Dr. Memory to search for memory problems. Your program must be memory error free and memory leak free to receive full credit.


