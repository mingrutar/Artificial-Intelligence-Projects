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

|  |  |
|:-------:|:----------|
| ![](images/cargo.jpg) | This project is to solve deterministic logistics planning problems for an Air Cargo transport<br> system using a planning search agent. With progression search algorithms, optimal plans<br> for each problem will be computed. implement domain-independent heuristics to aid the agent search.

The code needed be modified were my_air_cargo_problems.py and my_planning_graph.py. The test code, test result and heuristic analysis are shown in paper __[Heuristic Analysis for the Planning Search Agent](https://drive.google.com/open?id=1dZzBZM9w-8cmJxprcO-IAgS1V_JDeEiO7AZCjXkEXak)__

*code example of get actions*
```
def get_actions(self):
    """
    This method creates concrete actions (no variables) for all actions in the problem
    domain action schema and turns them into complete Action objects as defined in the
    aimacode.planning module. It is computationally expensive to call this method directly;
    however, it is called in the constructor and the results cached in the `actions_list` property.
    Returns:
    ----------
    list<Action>: list of Action objects
    """

    # concrete actions definition: specific literal action that does not include variables as with the schema
    # for example, the action schema 'Load(c, p, a)' can represent the concrete actions 'Load(C1, P1, SFO)'
    # or 'Load(C2, P2, JFK)'.  The
    def load_actions():
        """Create all concrete Load actions and return a list
        :return: list of Action objects
        """
        loads = []
        for cargo in self.cargos:
            for plane in self.planes:
                for ap in self.airports:
                    precond_pos = [expr("At({}, {})".format(cargo, ap)), expr("At({}, {})".format(plane, ap))]
                    precond_neg = []
                    effect_add = [expr("In({}, {})".format(cargo, plane))]
                    effect_rem = [expr("At({}, {})".format(cargo, ap))]
                    load = Action(expr("Load({}, {}, {})".format(cargo, plane, ap)),
                                  [precond_pos, precond_neg],
                                  [effect_add, effect_rem])
                    loads.append(load)
        return loads
```

wrote research paper __"[The History of AI Planning](https://drive.google.com/open?id=1KglOWcA0A5OVquWRGrnCtiQzlffe38M86VGfOBNKMSI)"__

<a id='minmax'></a>
### Chess-like Isolated Game (Build an Adversarial Search Agent) 

|  |  |
|:-------:|:----------|
| ![](images/knights.jpg) | The task is to develop an adversarial search agent to play a chess-like game "Isolation".<br>Isolation is a deterministic, two-player game of perfect information in which the players <br>alternate turns moving a single piece from one cell to another with only L-shaped<br> movements (like a knight in chess) on a board. Whenever either player occupies a <br>cell, that cell becomesblocked for the remainder of the game. The first player with<br> no remaining legal moves loses, and the opponent is declared the winner. |

The code needed be modified was game_agent.py. The test code, test result and heuristic analysis are shown in paper __[Heuristic Analysis for Game-Playing Agent](https://drive.google.com/open?id=17CtG2893zjYQYkXrKjg-5RZFnVQE1XdL970DZF1O48Q)__

*Code example of a score algorithm*
```
def custom_score(game, player):
    """Calculate the heuristic value of a game state from the point of view of the given player.
    This should be the best heuristic function for your project submission. Note: this function 
    should be called from within a Player instance as `self.score()`.
    Parameters
    ----------
    game : `isolation.Board`
        An instance of `isolation.Board` encoding the current state of the
        game (e.g., player locations and blocked cells).
    player : object
        A player instance in the current game (i.e., an object corresponding to
        one of the player objects `game.__player_1__` or `game.__player_2__`.)
    Returns
    -------
    float
        The heuristic value of the current game state to the specified player.
    <=> based on improved_score. randonly reduce score a bit if the location is close to edge,  
    """
    if game.is_loser(player):
        return float("-inf")

    if game.is_winner(player):
        return float("inf")

    own_moves = len(game.get_legal_moves(player))
    opp_moves = len(game.get_legal_moves(game.get_opponent(player)))
    score = own_moves - opp_moves
    w, h = game.width / 2., game.height / 2.
    y, x = game.get_player_location(player)
    ratio = (abs(h - y) + abs(w - x))/(w+h)     # how close to center
    return score * (2 + ratio)                  # weight score more than the closeness    
```

Wrote a review on IBM DeepBlue and Google AlphaGO __"[From Rain Man to Thinking Man, A Huge Leap in AI Made by AlphaGo](https://drive.google.com/open?id=1VhK4Ip0_Q5D2tqDTFlrDPc2B-ULn1vK_3pHOWrZ2j_o)"__

<a id='sudoku'></a>
### Sudoku (Solving Sudoku with AI)

*code example of search*
```
def search(values):
    values = reduce_puzzle(values)
    if not values:
        return False               # end, out
    if all(len(v) == 1 for v in values.values()):
        return values              # got values, out
    unsolved = {k: v for k, v in values.items() if len(v) > 1}
    if unsolved:
        sorted_unsolved = sorted(unsolved.items(), key=lambda x: len(x[1]))
        for s, v in sorted_unsolved:
            for d in v:
                copy_of_values = values.copy()
                copy_of_values[s] = d
                attempt = search(copy_of_values)      # recurse
                if attempt:
                    return attempt
        print("unsolved=", unsolved)
```

Screenshot of run result
![](images/sudoku.jpg)
