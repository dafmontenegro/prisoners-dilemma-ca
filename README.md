# prisoners-dilemma-cellular-automata

## Prisoner’s Dilemma
Perhaps this is the most famous problem in game theory, which is fundamentally based on cooperation and where two subjects face the same dilemma of whether to cooperate or not, with the only certainty being that their subsequent reward or outcome will be closely related to the decision made by the other. This problem has different versions; however, for this project, we will use the Symmetric 2×2 PD With Ordinal Payoffs (explained in greater depth in the Stanford Encyclopedia of Philosophy [2]) as exemplified in the table below:

|           | cooperate | defect |
| :-------: | :-------: | :----: |
| cooperate |   B, B    |  D, A  |
|  defect   |   A, D    |  C, C  |

Always satisfying: **A>B>C>D**. For this project, the equivalences used were as follows: **A=5, B=3, C=1, D=0.** The resulting table is shown below:

|           | cooperate | defect |
| :-------: | :-------: | :----: |
| cooperate |   3, 3    |  0, 5  |
|  defect   |   5, 0    |  1, 1  |

If you're interested in learning more, I recommend watching the video titled ["What Game Theory Reveals About Life, The Universe, and Everything" by Veritasium,](https://youtu.be/mScpHTIi-kM?si=4yu0qFeFhT4j2h1S) which inspired this project, as well as the educational game created by [Nicky Case, "The Evolution of Trust",](https://ncase.me/trust/) which was a huge inspiration for the aforementioned video.

## Tit For Tat Strategy
This was the strategy submitted by **Anatol Rapoport** to participate in the competition held by **Robert Axelrod** in **1980** [3]. Tit For Tat not only won the competition but also demonstrated *the importance of cooperation,* as any rational first glance at the prisoner's dilemma will always suggest that the best strategy is not to cooperate.<br>
I must confess that this is my favorite strategy, which is why I decided to have it play against the 256 8-bit cellular automata. But before we proceed, let's understand a little about how it works:

Tit For Tat relies on two very simple rules as its principle.
1. Start by cooperating as a gesture of goodwill toward the other.
2. Mirror the opponent's last move, regardless of whether they cooperated or not.

> Robert Axelrod identified **four success qualities** that contributed to the effectiveness of strategies[3]:
> 1. **Nice:** Have good will and do not take advantage of your opponent.
> 2. **Forgiving:** Cooperate when necessary, even if you've been let down before.
> 3. **Retaliatory:** If your opponent defects, strike back immediately. Don't be a pushover
> 4. **Clear:** Be consistent with your strategy and actions.

## Cellular Automata
To explain this in the best way, we will make use of the definition provided by **Wolfram Research** regarding one-dimensional cellular automata, which, to specify the state of a cell in the next generation, utilizes the current state of the cell and its immediate neighbors (one to its left and one to its right):

> The simplest class of one-dimensional cellular automata. Elementary cellular automata have two possible values for each cell (0 or 1), and rules that depend only on nearest neighbor values. As a result, the evolution of an elementary cellular automaton can completely be described by a table specifying the state a given cell will have in the next generation based on the value of the cell to its left, the value the cell itself, and the value of the cell to its right. Since there are 2×2×2=2^3=8 possible binary states for the three cells neighboring a given cell, there are a total of 2^8=256 elementary cellular automata, each of which can be indexed with an 8-bit binary number (Wolfram 1983, 2002).[1]

## References

[1] Wolfram Research, Inc. (s. f.). Elementary Cellular Automaton -- from Wolfram MathWorld. https://mathworld.wolfram.com/ElementaryCellularAutomaton.html

[2] Prisoner’s Dilemma (Stanford Encyclopedia of Philosophy). (2019, 2 abril). https://plato.stanford.edu/entries/prisoner-dilemma/

[3] Veritasium. (2023, 23 diciembre). What Game Theory Reveals About Life, The Universe, and Everything [Vídeo]. YouTube. https://www.youtube.com/watch?v=mScpHTIi-kM