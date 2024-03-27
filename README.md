# prisoners-dilemma-cellular-automata
A Python project that explores the dynamics of cooperation and competition through the lens of game theory. By transforming **cellular automata into strategies** and employing classic tactics like **Tit For Tat,** the project investigates the performance of various strategies in the context of the **Prisoner's Dilemma.**

## Theoretical Background

### Prisoner’s Dilemma
Perhaps this is the most famous problem in game theory, which is fundamentally based on cooperation and where two subjects face the same dilemma of whether to cooperate or not, with the only certainty being that their subsequent reward or outcome will be closely related to the decision made by the other. This problem has different versions; however, for this project, we will use the **Symmetric 2×2 PD With Ordinal Payoffs** (explained in greater depth in the **Stanford Encyclopedia of Philosophy [2]**) as exemplified in the table below:

|               | cooperate | defect |
| :-----------: | :-------: | :----: |
| **cooperate** |   B, B    |  D, A  |
|   **defect**  |   A, D    |  C, C  |

Always satisfying: **A>B>C>D**. For this project, the equivalences used were as follows: **A=5, B=3, C=1, D=0.** The resulting table is shown below:

|               | cooperate | defect |
| :-----------: | :-------: | :----: |
| **cooperate** |   3, 3    |  0, 5  |
|   **defect**  |   5, 0    |  1, 1  |

If you're interested in learning more, I recommend watching the video titled ["What Game Theory Reveals About Life, The Universe, and Everything" by Veritasium,](https://youtu.be/mScpHTIi-kM?si=4yu0qFeFhT4j2h1S) which inspired this project, as well as the educational game created by [Nicky Case, "The Evolution of Trust",](https://ncase.me/trust/) which was a huge inspiration for the aforementioned video.

### Tit For Tat Strategy
This was the strategy submitted by **Anatol Rapoport** to participate in the competition held by **Robert Axelrod** in **1980** [3]. Tit For Tat not only won the competition but also demonstrated ***the importance of cooperation,*** as any rational first glance at the prisoner's dilemma will always suggest that the best strategy is not to cooperate.<br>
I must confess that this is ***my favorite strategy,*** which is why I decided to have it play against the 256 **8-bit cellular automata.** But before we proceed, let's understand a little about how it works:

Tit For Tat relies on **two very simple rules** as its principle.
1. **Start by cooperating** as a gesture of goodwill toward the other.
2. **Mirror the opponent's last move,** regardless of whether they cooperated or not.

> Robert Axelrod identified **four success qualities** that contributed to the effectiveness of strategies [3]:
> 1. **Nice:** Have good will and do not take advantage of your opponent.
> 2. **Forgiving:** Cooperate when necessary, even if you've been let down before.
> 3. **Retaliatory:** If your opponent defects, strike back immediately. Don't be a pushover
> 4. **Clear:** Be consistent with your strategy and actions.

### Cellular Automata
To explain this in the best way, we will make use of the definition provided by **Wolfram Research** regarding one-dimensional cellular automata, which, to specify the state of a cell in the next generation, utilizes the current state of the cell and its immediate neighbors (one to its left and one to its right):

> The simplest class of **one-dimensional cellular automata.** Elementary cellular automata have two possible values for each cell **(0 or 1)**, and rules that depend only on nearest neighbor values. As a result, the evolution of an elementary cellular automaton can completely be described by a table specifying the state a given cell will have in the next generation based on the value of the cell to its left, the value the cell itself, and the value of the cell to its right. Since there are **2×2×2=2^3=8 possible binary states** for the three cells neighboring a given cell, there are a total of **2^8=256 elementary cellular automata**, each of which can be indexed with an 8-bit binary number **(Wolfram 1983, 2002).**[1]

## Implementation and Simulation

### The 256 Rules as a Strategy
A rule is essentially an **8-bit binary number** corresponding to all possible responses to a 3-bit binary number. In other words, given one of the 8 possible inputs **(binary numbers between 0 and 7)**, the result will be either 0 or 1, which in the context of the project means to cooperate or not to cooperate.

To illustrate a rule, let's arbitrarily choose **rule 12** and **rule 21**:

|             |  111  |  110  |  101  |  100  |  011  |  010  |  001  |  000  |
| :---------: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **rule 12** |   0   |   0   |   0   |   0   |   1   |   1   |   0   |   0   |
| **rule 21** |   0   |   0   |   0   |   1   |   0   |   1   |   0   |   1   |

For rules to compete against each other, it's necessary that they have at least 3 bits as a starting point, which in the project we call ***preloads,*** and this defines the types of games created **(x8 and x64)**. The x8 game mode corresponds to both rules starting the game with the *same preload*, while the x64 mode allows them to start with different preloads, resulting in **8^2 = 64 pairings**. Let's see both examples below:

#### x8 Game Example:

|             |    010    |    101    |    010    |    101    |    010    |    101    |    010    |    101    |    010    |    101    |        |
| :---------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :----: |
| **rule 12** |     1     |     0     |     1     |     0     |     1     |     0     |     1     |     0     |     1     |     0     |   20   |
| **rule 21** |     1     |     0     |     1     |     0     |     1     |     0     |     1     |     0     |     1     |     0     |   20   |
|             |  **010**  |  **101**  |  **010**  |  **101**  |  **010**  |  **101**  |  **010**  |  **101**  |  **010**  |  **101**  |        |

> Game of 10 moves, same preload, x8 mode. A complete x8 game involves repeating the same process, but with all 8 possible binary states as preload.

#### x64 Game Example:

|             |    101    |    011    |    110    |    100    |    000    |    000    |    001    |    010    |    100    |    000    |        |
| :---------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :----: |
| **rule 12** |     1     |     0     |     0     |     0     |     0     |     1     |     0     |     0     |     0     |     1     |   29   |
| **rule 21** |     0     |     0     |     0     |     1     |     1     |     1     |     0     |     1     |     1     |     1     |   14   |
|             |  **010**  |  **100**  |  **000**  |  **000**  |  **001**  |  **011**  |  **111**  |  **110**  |  **101**  |  **011**  |        |

> Game of 10 moves, different preloads, x64 mode. A complete x64 game involves repeating the same process, but with all possible 64 pairings of binary states as preloads.

### The Anti-Automata

When I thought about putting the 256 automatons to compete, the idea of ​​creating a strategy called the anti-automata occurred to me, **capable of recognizing the opponent's strategy** in a series of movements **(to which specific rule it faces)** and subsequently, with this information, knowing the opponent's next move and defeating it.

I theorized that with the correct sequence of initial outputs, the anti-automata could in 8 moves determine all the binary states of the opponent. For example, starting from the preload **000,** it's possible to generate the sequence **1110100** to obtain the binary states in the order **01376524**, or also the sequence **1011100** to obtain the responses of **01253764**; this idea could be extended to all binary states and possible pairings, but ultimately, *it's a futile concept.* Let's see why:

|               | cooperate | defect |                |
| :-----------: | :-------: | :----: | :------------: |
| **cooperate** |     3     |    0   |   3 + 0 = 3    |
|  **defect**   |     5     |    1   |   5 + 1 = 6    |

There are two possible responses from our opponent regardless of what we do, these are to cooperate or not to cooperate. Assuming that our criterion for making the best decision per turn is **to gain the highest number of points,** then we will discover that **not cooperating is always the only response in this strategy.** *Notice that in the table above, the row with the most points is the defect.*

> In the table, the largest sum of cells would be **3 + 5 = 8**. However, this strategy could not be considered feasible, as both cells are mutually exclusive; that's why **5 + 1 = 6** is the strategy that would yield the most points.

All this means that the 8 bits of the anti-automaton are all 0 and that it corresponds to rule 0 **(the most selfish rule)**.

|                            |  111  |  110  |  101  |  100  |  011  |  010  |  001  |  000  |
| :------------------------: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **rule 0 (anti-automata)** |   0   |   0   |   0   |   0   |   0   |   0   |   0   |   0   |

### Tit For Tat Rule

## Results and Analysis

### The Best Rule

### Tit For Tat Performance

## Contributions
Contributions to prisoners-dilemma-cellular-automata are welcome from researchers, developers, and enthusiasts interested in game theory, computational modeling, and strategic analysis. Collaborative efforts to expand the project's scope, refine simulation methodologies, and interpret results are encouraged and appreciated.

## References
[1] Wolfram Research, Inc. (s. f.). Elementary Cellular Automaton -- from Wolfram MathWorld. https://mathworld.wolfram.com/ElementaryCellularAutomaton.html

[2] Prisoner’s Dilemma (Stanford Encyclopedia of Philosophy). (2019, 2 abril). https://plato.stanford.edu/entries/prisoner-dilemma/

[3] Veritasium. (2023, 23 diciembre). What Game Theory Reveals About Life, The Universe, and Everything [Vídeo]. YouTube. https://www.youtube.com/watch?v=mScpHTIi-kM