Download Link: https://assignmentchef.com/product/solved-fit2004-assignment-4-graph-algorithms
<br>
<ol>

 <li>Think of test cases that you can use to check if your algorithm works.

  <ul>

   <li>Use the edge cases you found during the previous phase to inspire your test cases.</li>

   <li>It is also a good idea to generate large random test cases.</li>

   <li>Sharing test cases is allowed, as it is not helping solve the assignment.</li>

  </ul></li>

 <li>Code up your algorithm, (remember decomposition and comments) and test it on the tests you have thought of.</li>

 <li>Try to break your code. Think of what kinds of inputs you could be presented with which your code might not be able to handle.

  <ul>

   <li>Large inputs</li>

   <li>Small inputs</li>

   <li>Inputs with strange properties</li>

   <li>What if everything is the same?</li>

   <li>What if everything is different?</li>

   <li>..</li>

  </ul></li>

</ol>

<h1>Documentation</h1>

For this assignment (and all assignments in this unit) you are required to document and comment your code appropriately. This documentation/commenting must consist of (but is not limited to)

<ul>

 <li>For each function, high level description of that function. This should be a one or two sentence explanation of what this function does. One good way of presenting this information is by specifying what the input to the function is, and what output the function produces (if appropriate)</li>

 <li>For each function, the Big-O complexity of that function, in terms of the input. Make sure you specify what the variables involved in your complexity refer to. Remember that the complexity of a function includes the complexity of any function calls it makes.</li>

 <li>Within functions, comments where appropriate. Generally speaking, you would comment complicated lines of code (which you should try to minimise) or a large block of code which performs a clear and distinct task (often blocks like this are good candidates to be their own functions!).</li>

</ul>

<h1>Graph class</h1>

This assignment is about graphs and graph algorithms. As such, both problems relate to graphs in some way. You must write a class WordGraph , and the solutions to the tasks in this assignment will be implemented as methods of that class.

Both tasks relate to word ladders. An instance of WordGraph represents all the words we are allowed to use in order to construct word ladder. In other words, you will not be constructing word ladders from all possible English words, but rather from whichever strings are stored in the graph you are working with.

The __init__ method of WordGraph must take as input a nonempty list of words and construct an appropriate graph from them. The words will contain only lowercase a-z characters, and will all be the same length, which will not be 0.

In later tasks, we will sometimes refer to a word by its index in this input list (i.e. we associate each word/vertex with an index 0<em>..n </em>−1 in the usual way).

A very basic example implementation of an adjacency-list based graph class will be provided on Ed, and you may use this as your starting point for a class.

<h1>1                     Word ladders</h1>

Consider the following problem: You are given a collection of words, all of which are target words for word ladders. You need to find the start word for which finding word ladders to all the targets is as easy as possible.

To solve this problem, you will write a method of your Graph class, best_start_word(self, target_words).

1.1       Input

target_words is a nonempty list of indices of words in the graph.

<h2>1.2       Output</h2>

best_start_word returns an integer, which is the index of the word in the graph which produces the overall shortest word ladders to each of the words in target_words.

More precisely, it returns the index of the word for which the longest word ladder to any of the words in target_words is as short as possible.

If there are multiple such words, just return one arbitrarily (i.e. it does not matter which one you return, but only return one).

If no such word exists, return -1.

<h2>1.3        Example</h2>

<table width="642">

 <tbody>

  <tr>

   <td width="642">words = [“aaa”,”aad”,”dad”,”daa”,”aca”,”acc”,”aab”,”abb”] g = WordGraph(words)#target words are dad, abb, acc. Best start word is aaa print(g.best_start_word([2,7,5])) &gt;&gt;&gt; 0#target words are dad, aab. Best start word is aad print(g.best_start_word([6,2])) &gt;&gt;&gt; 1#target words are aaa, aca, acc. Best start word is aca print(g.best_start_word([0,4,5]))&gt;&gt;&gt; 4</td>

  </tr>

 </tbody>

</table>

To visualise these examples, the graph below is provided.

<h2>1.4        Complexity</h2>

best_start_words must run in <em>O</em>(<em>W</em><sup>3</sup>) time where

<ul>

 <li><em>W </em>is the number of words in the instance of WordGraph</li>

</ul>

Note that this time complexity is larger than needed in most cases. There are several simple optimisations which can be made, in order to reduce the complexity of the solution for various classes of graphs. Doing this is not necessary for full marks.

<h1>2                       Constrained word ladders</h1>

In this task, we want to construct a word ladder with some additional constraints.

The first constraint is that we want to minimise the alphabetic distance of the word ladder. The alphabetic distance of a word ladder is the sum of the alphabetic distances between each pair of consecutive words in that ladder.

We define the alphabetic distance between two words in a ladder as the difference in alphabetic position between the letters in the two words which are different. For example,

<ul>

 <li>“cat” and “bat” have distance 1, since “b” is the second letter of the alphabet, and “c” is the third.</li>

 <li>“bat” and “bet” have distance 4, since “a” is the first letter of the alphabet, and “e” is the fifth.</li>

 <li>“”bet” and “wet” have distance 21, since “b” is the second letter of the alphabet, and “w” is the twenty-third</li>

</ul>

So the alphabetic distance of the word ladder “cat” → “bat” → “bet” → “wet” is 1+4+21=26. The second constraint is that we need to use one of a set of particular words in the ladder.

To solve this problem, you will write a method of WordGraph, constrained_ladder(self, start, target, constraint_words)

<h2>2.1       Input</h2>

start and target are indices of vertices. start is the index of the word where the word ladder must start, and target is the index of the word where the word ladder must end.

constraint_words is a list of indices. At least one of these words must appear in the word ladder.

<h2>2.2       Output</h2>

constrained_ladder returns the list of indices of vertices (in order) corresponding to words representing the word ladder which

<ul>

 <li>starts with start</li>

 <li>ends with end</li>

 <li>contains at least one word from constraint_words (it may contain more than one, and the word can appear at any point in the word ladder, including the first or last word)</li>

 <li>has the minimum alphabetic distance out of all word ladders which satisfy the first three conditions.</li>

</ul>

If there are multiple word ladders which satisfy all of the above properties, return any one of them.

If there are no such ladders, return None.

<h2>2.3        Example</h2>

<table width="642">

 <tbody>

  <tr>

   <td width="642">words = [’aaa’,’bbb’,’bab’,’aaf’,’aaz’,’baz’,’caa’,’cac’,’dac’,’dad’,’ead’,’eae’,’bae’,’abf’,’bbf’] start = 0 end = 1 detour = [12] g = WordGraph(words)g.constrained_ladder(start, end, detour) &gt;&gt;&gt;[0, 6, 7, 8, 9, 10, 11, 12, 2, 1]#this corresponds to the list of words#[’aaa’, ’caa’, ’cac’, ’dac’, ’dad’, ’ead’, ’eae’, ’bae’, ’bab’, ’bbb’]detour = [2]g.constrained_ladder(start, end, detour) &gt;&gt;&gt;[0, 3, 13, 14, 1, 2, 1]#this corresponds to the list of words#[’aaa’, ’aaf’, ’abf’, ’bbf’, ’bbb’, ’bab’, ’bbb’]</td>

  </tr>

 </tbody>

</table>

This graph corresponds to the first of the two examples above. Green indicates the start vertex, red the end vertex, and purple the constraint vertices (only one vertex is a constraint in each example above). The numbers on edges represent the alphabetic distance between words.

The second example differs from the diagram in that “bab” is a constraint, instead of “bae”.

<h2>2.4        Complexity</h2>

constrained_ladder must run in <em>O</em>(<em>Dlog</em>(<em>W</em>)+ <em>Wlog</em>(<em>W</em>))) where

<ul>

 <li><em>D </em>is the number of pairs of words in WordGraph which differ by exactly one letter</li>

 <li><em>W </em>is the number of words in WordGraph</li>

</ul>

Note that the required complexity does not involve any term related to the size of constraint_words. In other words, the algorithm should run in the same time complexity regardless of how large this list is.