
TDD Tetris Tutorial
===================

In this tutorial you will be implementing a Tetris game using [Test-Driven Development](http://en.wikipedia.org/wiki/Test-driven_development) (TDD). Some 30 of the first tests have been provided, so that you just need to write code to pass them. The purpose of working with these pre-written test cases is to get accustomed to the TDD cycle, and to get some ideas on what kind of tests to write. After doing that for some while, it will be easier when it's time to begin writing your own tests towards the end of this tutorial.

For information about Test-Driven Development, here are some links. It is recommendable to read them before doing this tutorial, so that you would know what TDD is about.

General information about TDD:

- <http://www.butunclebob.com/ArticleS.UncleBob.TheThreeRulesOfTdd>
- <http://www.butunclebob.com/ArticleS.UncleBob.TheBowlingGameKata>
- <http://jamesshore.com/Agile-Book/test_driven_development.html>
- <http://www.agiledata.org/essays/tdd.html>

TDD is more about specifying behaviour than about testing:

- <http://dannorth.net/introducing-bdd>
- <http://blog.daveastels.com/files/BDD_Intro.pdf>
- <http://blog.orfjackal.net/2010/02/three-styles-of-naming-tests.html>

Summary:

- <http://blog.briandicroce.com/2008/03/14/three-index-cards-to-easily-remember-the-essence-of-test-driven-development/>
- <http://agileinaflash.blogspot.com/2009/03/unclebobs-three-rules-of-tdd.html>
- <http://agileinaflash.blogspot.com/2009/02/red-green-refactor.html>
- <http://agileinaflash.blogspot.com/2009/02/first.html>


The Steps of the Tutorial
-------------------------

Use the following tests to write a Tetris game. Implement code to pass the tests, one file and test at a time, in the same order as they are listed below, starting with `FallingBlocksTest.java`. First write code which passes the first test (`A_new_board.is_empty`) and then uncomment the following test (`A_new_board.has_no_falling_blocks`). When that test passes, uncomment the next one (`When_a_block_is_dropped.the_block_is_falling`) until finally you have written code which passes all tests in that class. Then open the next test class and keep on continuing in the same fashion.

Reference implementations for the steps of this tutorial have been provided at this tutorial's [Git repository](http://github.com/orfjackal/tdd-tetris-tutorial/downloads) (the [beyond branch](http://github.com/orfjackal/tdd-tetris-tutorial/tree/beyond) contains the most complete implementation). It might be helpful to have a look at them *after* you have yourself implemented this tutorial that far. The reference implementation may teach you something about writing clean code.

This material has been used on the [TDD programming technique and designing code](http://www.cs.helsinki.fi/u/luontola/tdd-2009/) course in the University of Helsinki. The [lecture slides](http://www.cs.helsinki.fi/u/luontola/tdd-2009/luennot) and [exercises](http://www.cs.helsinki.fi/u/luontola/tdd-2009/harjoitukset) of that course can also be helpful (the material is in English, but for the rest of the site you can use [Google Translate](http://translate.google.com/)).


1. **FallingBlocksTest.java**

    In Tetris, the most important feature is that there are blocks which fall down, so that is the first behaviour which we will specify by writing tests. It is good to start the writing of a program with a very trivial test. In this case, we will first make sure that we have an empty game board.

2. **RotatingPiecesOfBlocksTest.java**

    Rotating the pieces in Tetris is also very important, so let's code that next. You might need pen and paper when figuring out how the shape coordinates change when the shape is rotated.

    (I decided to go for a generic method of rotating any shapes. Another option would have been to hard-code the rotations of each shape. Both have their pros and cons. But even if this decision would prove to be bad when the game expands beyond this tutorial, good test coverage and decoupled code will make it possible to change it afterwards.)

3. **RotatingTetrominoesTest.java**

    [Tetrominoes](http://en.wikipedia.org/wiki/Tetromino) can have 1, 2 or 4 different positions when they are rotated. Now we can take advantage of the shape rotation code which we wrote just a moment ago.

    Notice that the first test specifies the Tetromino objects to be immutable. Check the Wikipedia article about [immutable objects](http://en.wikipedia.org/wiki/Immutable_object) if that concept is new to you.

4. **FallingPiecesTest.java**

    Next we will connect the falling blocks and the rotatable pieces. In order to make the first test pass, you will probably need to refactor your code quite much (for me it took 1½ hours). You need to build suitable abstractions, so that single-block pieces and multi-block pieces can be handled the same way (changing the test code should not be necessary). When refactoring, you must keep the tests passing between every small change, or you will end up in <a href="http://c2.c2.com/cgi/wiki?RefactoringHell">refactoring hell</a>. If more than five minutes has passed since the last time all tests passed, revert your code to the last version from source control where all tests passed.

    The difficulty of this refactoring depends on how well factored the code is. You could even say that the difficulty of this refactoring is inversely proportional to the length of the `Board.tick()` method (if most of the logic is in that one method, instead of using [Composed Method](http://www.infoq.com/presentations/10-Ways-to-Better-Code-Neal-Ford), then you're in trouble). If you get stuck, you may get some hints from [this example refactoring](http://www.cs.helsinki.fi/u/luontola/tdd-2009/kalvot/04.1-Refactoring-Example.pdf).

5. **MovingAFallingPieceTest.java**

    Now it's your turn to write the tests. I've provided some TODO items which should hint you on what kind of tests to write.

6. **RotatingAFallingPieceTest.java**

    Keep on writing your own tests. You're getting the hang of it!

7. **And beyond...**

    Next you should probably implement the following features in a suitable order: removing full rows, counting removed rows (maybe launch an event when a row is removed - <a href="http://mockito.org/">Mockito</a> might come in handly for testing that), counting score, choosing the next piece by random. It would also be good to replace the earlier algorithmic shape rotation (which was done in step 2) with one where each orientation of a shape is hardcoded, because that will simplify the code considerably.

    Soon after that you should be able to create a user interface which is only a thin wrapper over the already implemented functionality. Automated testing of user interfaces is generally hard to do, but by separating the UI model from its view it is possible (see [these articles](http://martinfowler.com/eaaDev/ModelViewPresenter.html)).


### What Next? ###

After you have completed this tutorial, you should have a rough understanding of how to use TDD - you should be at the [Practicing](http://sites.google.com/site/agileskillsprojectwiki/skill-levels) or [Shu](http://martinfowler.com/bliki/ShuHaRi.html) level. You will probably still struggle with things like always following the TDD cycle, using small enough steps, writing self-documenting tests, writing clean code etc. Also most of the tests in this tutorial are perhaps confusingly similar (verify all game board state using `toString()`) so you should practice writing tests for different kinds of situations.

You should continue practicing by writing lots of small applications using TDD, until TDD becomes second nature to you and you can use it ["when you have to get it done"](http://www.vimeo.com/groups/7657/videos/3756344). Learning that will take many months. It's also recommendable to read the books [Clean Code](http://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) and [Growing Object-Oriented Software, Guided by Tests](http://www.amazon.com/Growing-Object-Oriented-Software-Guided-Tests/dp/0321503627).


License
-------

Copyright © 2009-2010 Esko Luontola <<http://www.orfjackal.net>>  
You may use and modify this material freely for personal non-commercial use.  
This material may NOT be used as course material without prior written agreement.
