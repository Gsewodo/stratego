# dev4-stratego

Gracziela Sewodo, 52949
Iuliana Costil, 55994
This README allows you to better understand the project.

the structure of our project: (V2)
stratego
├── metier
│   ├── header
│   │   ├── utils
│   │   │   ├── observer.h
│   │   │   └── subject.h
│   │   ├── game.h
│   │   ├── board.h
│   │   ├── square.h
│   │   ├── position.h
│   │   ├── common_piece.h
│   │   ├── common_moveable_piece.h
│   │   ├── Common_piece_factory.h
│   │   ├── spy.h
│   │   ├── miner.h
│   │   ├── direction.h
│   │   ├── player.h
│   │   ├── playerColor.h
│   │   ├── model.h
│   │   ├── state.h
│   │   ├── action_result.h
│   │   └── constants.h
│   └── sources
│       ├── utils
│       │   └── subject.cpp
│       ├── game.cpp
│       ├── board.cpp
│       ├── common_piece.cpp
│       ├── common_moveable_piece.cpp
│       └── player.cpp
│  
├── console
│   ├── view
│   │   ├── header
│   │   │   └── view.h
│   │   └── sources
│   │       └── view.cpp
│   ├── controller
│   │   ├── header
│   │   │   └── controller.h
│   │   └── sources
│   │       └── controller.cpp
│   └── main.cpp
│ 
├── Gui
|     ├──images
|     ├── headers
│     |     ├── mainwindow.h
|     |     └── PieceButton.h
|     └── sources
│            ├── mainwindow.cpp
|            ├── main.cpp
|            └── PieceButton.cpp     
│ 
└── tests
    └── sources
        ├── main.cpp
        └── tst_model.cpp


 Explanation of classes: 

 Board : represents the board(10x10) of the game, that will contain our pieces
 Square : refers to a square of our 10x10 squares game board
 CommonPiece : class that represents a simple piece that is not moveable
 CommonMoveablePiece : class that represents a simple piece that is moveable. cub-class of Commonpiece
 Miner : class that represents a Miner piece that is moveable. sub-class of CommonMoveablePiece
 Spy : class that represents a Spy piece that is moveable. sub-class of CommonMoveablePiece
 Position:The position class represents a position in the game board.
 Model: the class that will structure our project joining all the other classes together

Explanation of enums:

ActionResult : The ActionResult enum represents the result of the movement made :   BOTH_LOST, CURRENT_LOST, OPPONENT_LOST,NOBODY_LOST

 State : The state enum represents the game state :  NOT_STARTED,END,IN_PROGRESS,INTERACTIVE

 PlayerColor : The Player enum represents the color of the player :  BLUE,RED

 ranks :   ranks enum represents the rank of a piece 
            
 max_squares : max_squares enum represents the maximum number of steps of a piece 
              
 numberOfPieces : numberOfPieces enum represents the number of pieces of a certain type per player



Changes made since the first submission: 

PIECES: 
we made 2 type of pieces 
1) CommonPiece that can't move (rank,color)
2) CommonMoveablePiece piece a sub class of common_piece. it can move and has a number of maximum steps(max_squares).the number of steps depends of the type of the piece ( the rank ). 

we add some subclass of CommonMoveablePiece: 
-Spy that represents a spy piece. we added it because a spy can kills a Marshall despite his rank. (spy rank 1, Marshall rank 10) 
But it gets kill by any other pieces. 
-Miner that represents a miner piece. we added it because the miner is the only piece that can defuse a bomb.
 
we overrided  == ,> and < operators of CommonPiece that now all check the rank of the pieces 

we added Common_piece_factory to deal with the instantiation of the piece and to deal with polymorphism 

GAME: 
we added a method that swaps the player (Blue becomes RED and vice versa) after every move. it is private so the user can't access it through the console .

we added selectedSquare.

to know if a move is allowed we use a vector that contains every positions where a selected piece(that is in selectedSquare) can go 

we added some methods to fill the board through the console row by row and through 2 files (placement_blue.tx and placement_red.txt)

SQUARE:
we add a position to Square. 

we change the "std::optional<piece>" with a "std::shared_ptr<CommonPiece>" to deal with polymorphism.(Square)

GENERAL: 

 we implements observer observable + mvc pattern

more details + class diagram in our pdf file 

V3 gui part :
we changed the Game class of model: 
-we added ActionResult currentResult_ to know who win a battle, who lose, both lose ? 
move method: 
the method return is now void.
when we move the currentResult_ change depending on who win after that we notify with the PROPERTY_NEWRESULT property. then we swap the player and we notify with PROPERTY_BOARD property.  
more details + class diagram in our pdf file 
