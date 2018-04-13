## Artificial Intelligence Projects for [Udacity Artificial Intelligence ND](https://www.udacity.com/course/artificial-intelligence-nanodegree--nd889)

Udacity Artificial Intelligence ND is an advanced course. We built projects for broad field of artificial intelligence. The projects are:
* [Use HMM to Recognize ASL](#asl), 
* [Domain-Independent Planner](#planning), 
* [Adversarial Search Agent](#minmax), 
* [Solving Sudoku with AI](#sudoku)

<sub>*Udacity Deep Learning is an ongoing course. For academic integrity, the source code of my implementation are private. If you like to view the code, please let me know.*</sub>

<a id='asl'></a>
### American Sign Language Recognizer (Use HMM to Recognize ASL)
The overall goal of this project is to build a word recognizer for American Sign Language video sequences, demonstrating the power of probabalistic models.  In particular, this project employs  [hidden Markov models (HMM's)](https://en.wikipedia.org/wiki/Hidden_Markov_model) to analyze a series of measurements taken from videos of American Sign Language (ASL) collected for research (see the [RWTH-BOSTON-104 Database](http://www-i6.informatik.rwth-aachen.de/~dreuw/database-rwth-boston-104.php)).  In this video, the right-hand x and y locations are plotted as the speaker signs the sentence.
[![ASLR demo](http://www-i6.informatik.rwth-aachen.de/~dreuw/images/demosample.png)](https://drive.google.com/open?id=0B_5qGuFe-wbhUXRuVnNZVnMtam8)

I implemented a half of dozen features. Below is an example of feature selections:

![](images/ASLDemo.png)

The Model Selectors: 
* Cross Validation fold, use sklearn KFold 
* Bayesian information Criterion, use hmmlearn GaussianHMM 
* Discriminative Information Criterion, use hmmlearn GaussianHMM 

The Recognizer trains the models for each word and test the models with sentences for each combination of features and selectors. The best result I have achieved is 60% accuracy or 40% error rate (WER), see below. Under 60% WER is considerated as a reasonable model.  

``` 
**** WER = 0.4044943820224719
Total correct: 106 out of 178
Video  Recognized                                                    Correct
=====================================================================================================
  100: POSS NEW CAR BREAK-DOWN                                       POSS NEW CAR BREAK-DOWN
    2: JOHN WRITE HOMEWORK                                           JOHN WRITE HOMEWORK
    .......
```

<a id='planning'></a>
### Air Cargo Problem (Create a Domain-Independent Planner)

https://github.com/mingrutar/aind_project3_search

<a id='minmax'></a>
### Chess-like Isolated Game (Build an Adversarial Search Agent) 

|  |  |
|:-------:|:----------|
| ![](images/knights.jpg) | The task is to develop an adversarial search agent to play a chess-like game "Isolation".<br>Isolation is a deterministic, two-player game of perfect information in which the players <br>alternate turns moving a single piece from one cell to another with only L-shaped movements <br>(like a knight in chess) on a board. Whenever either player occupies a cell, that cell becomes<br>blocked for the remainder of the game. The first player with no remaining legal moves loses, <br>and the opponent is declared the winner. |

The code needed be modified was game_agent.py. The test code, test result and heuristic analysis are shown in paper [Heuristic Analysis for Game-Playing Agent](https://drive.google.com/open?id=17CtG2893zjYQYkXrKjg-5RZFnVQE1XdL970DZF1O48Q)

Wrote a review on IBM DeepBlue and Google AlphaGO "[From Rain Man to Thinking Man  A Huge Leap in AI Made by AlphaGo](https://drive.google.com/open?id=1VhK4Ip0_Q5D2tqDTFlrDPc2B-ULn1vK_3pHOWrZ2j_o)"

<a id='sudoku'></a>
### Sudoku (Solving Sudoku with AI)

https://github.com/mingrutar/aind_projects/tree/master/project1-sudoku

