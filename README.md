Download Link: https://assignmentchef.com/product/solved-ve492-project-2-multi-agent-search-2
<br>
In this project, you will design agents for the classic version of Pacman, including ghosts. Along the way, you will implement both minimax and expectimax search and try your hand at evaluation function design.

The code base has not changed much from the previous project, but please start with a fresh installation, rather than intermingling files from project 1. The code for this project consists of several Python files, some of which you will need to read and understand in order to complete the assignment, and some of which you can ignore You can download all the code and supporting files as a <a href="https://umjicanvas.com/files/215674/download?download_frd=1">zip archive</a> in the folder VE492 Projects on Canvas.

<strong>Files to Edit and Submit: </strong>You will fill in portions of multiAgents.py during the assignment. Please <em>do not </em>change the other files in this distribution or submit any of our original files other than these files.

<table width="0">

 <tbody>

  <tr>

   <td colspan="2" width="514"><strong>Files you’ll edit:</strong></td>

  </tr>

  <tr>

   <td width="164">multiAgents.py</td>

   <td width="349">Where all of your multi-agent search agents will reside.</td>

  </tr>

  <tr>

   <td colspan="2" width="514"><strong>Files you might want to look at:</strong></td>

  </tr>

  <tr>

   <td width="164">pacman.py</td>

   <td width="349">The main file that runs Pacman games. This file describes a Pacman GameState type, which you use in this project.</td>

  </tr>

  <tr>

   <td width="164">game.py</td>

   <td width="349">The logic behind how the Pacman world works. This file describes several supporting types like AgentState, Agent, Direction, and Grid.</td>

  </tr>

  <tr>

   <td width="164">util.py</td>

   <td width="349">Useful data structures for implementing search algorithms.</td>

  </tr>

  <tr>

   <td colspan="2" width="514"><strong>Supporting files you can ignore:</strong></td>

  </tr>

  <tr>

   <td width="164">graphicsDisplay.py</td>

   <td width="349">Graphics for Pacman</td>

  </tr>

  <tr>

   <td width="164">graphicsUtils.py</td>

   <td width="349">Support for Pacman graphics</td>

  </tr>

  <tr>

   <td width="164">textDisplay.py</td>

   <td width="349">ASCII graphics for Pacman</td>

  </tr>

  <tr>

   <td width="164">ghostAgents.py</td>

   <td width="349">Agents to control ghosts</td>

  </tr>

  <tr>

   <td width="164">keyboardAgents.py</td>

   <td width="349">Keyboard interfaces to control Pacman</td>

  </tr>

  <tr>

   <td width="164">layout.py</td>

   <td width="349">Code for reading layout files and storing their contents</td>

  </tr>

 </tbody>

</table>

<h1>Welcome to Multi-Agent Pacman</h1>

After downloading the code (<a href="https://umjicanvas.com/files/215674/download?download_frd=1">P2.zip</a><a href="https://umjicanvas.com/files/215674/download?download_frd=1">)</a>, unzipping it, and changing to the directory, you should be able to play a game of Pacman by typing the following at the command line: python pacman.py

and using the arrow keys to move. Now, run the provided ReflexAgent in multiAgents.py python pacman.py -p ReflexAgent

Note that it plays quite poorly even on simple layouts: python pacman.py -p ReflexAgent -l testClassic

Inspect its code (in multiAgents.py) and make sure you understand what it’s doing.

<h1>Question 1 : Reflex Agent</h1>

Improve the ReflexAgent in multiAgents.py to play respectably. The provided reflex agent code provides some helpful examples of methods that query the GameState for information. A capable reflex agent will have to consider both food locations and ghost locations to perform well. Your agent should easily and reliably clear the testClassic layout: python pacman.py -p ReflexAgent -l testClassic

Try out your reflex agent on the default mediumClassic layout with one ghost or two (and animation off to speed up the display):

python pacman.py –frameTime 0 -p ReflexAgent -k 1 python pacman.py –frameTime 0 -p ReflexAgent -k 2 How does your agent fare? It will likely often die with 2 ghosts on the default board, unless your evaluation function is quite good.

<em>Note: </em>Remember that newFood has the function asList()

<em>Note: </em>As features, try the reciprocal of important values (such as distance to food) rather than just the values themselves.

<em>Note: </em>The evaluation function you’re writing is evaluating state-action pairs; in later parts of the project, you’ll be evaluating states.

<em>Note: </em>You may find it useful to view the internal contents of various objects for debugging. You can do this by printing the objects’ string representations.

For example, you can print newGhostStates with print(newGhostStates). <em>Options: </em>Default ghosts are random; you can also play for fun with slightly smarter directional ghosts using -g DirectionalGhost. If the randomness is preventing you from telling whether your agent is improving, you can use -f to run with a fixed random seed (same random choices every game). You can also play multiple games in a row with -n. Turn off graphics with -q to run lots of games quickly.

<em>Grading: </em>We will run your agent on the openClassic layout 10 times. You will receive full points if your agent’s average score is greater than 1000. Don’t spend too much time on this question, though, as the meat of the project lies ahead.

<h1>Question 2 (5 points): Minimax</h1>

Now you will write an adversarial search agent in the provided MinimaxAgent class stub in multiAgents.py. Your minimax agent should work with any number of ghosts, so you’ll have to write an algorithm that is slightly more general than what you’ve previously seen in lecture. In particular, your minimax tree will have multiple min layers (one for each ghost) for every max layer.

Your code should also expand the game tree to an arbitrary depth. Score the leaves of your minimax tree with the supplied self.evaluationFunction, which defaults to scoreEvaluationFunction. MinimaxAgent extends MultiAgentSearchAgent, which gives access to self.depth and self.evaluationFunction. Make sure your minimax code makes reference to these two variables where appropriate as these variables are populated in response to command line options.

<em>Important: </em>A single search ply is considered to be one Pacman move and all the ghosts’ responses, so depth 2 search will involve Pacman and each ghost moving two times.

<em>Grading: </em>We will be checking your code to determine whether it explores the correct number of game states. This is the only reliable way to detect some very subtle bugs in implementations of minimax. <em>Hints and Observations</em>

<ul>

 <li>Hint: Implement the algorithm recursively using helper function(s).</li>

 <li>The correct implementation of minimax will lead to Pacman losing the game in some tests. This is not a problem: as it is correct behaviour, it will pass the tests.</li>

 <li>The evaluation function for the Pacman test in this part is already written (evaluationFunction). You shouldn’t change this function, but recognize that now we’re evaluating <em>states </em>rather than actions, as we were for the reflex agent. Look-ahead agents evaluate future states whereas reflex agents evaluate actions from the current state.</li>

 <li>The minimax values of the initial state in the minimaxClassic layout are 9, 8, 7, -492 for depths 1, 2, 3 and 4 respectively. Note that your minimax agent will often win (665/1000 games for us) despite the dire prediction of depth 4 minimax.</li>

</ul>

python pacman.py -p MinimaxAgent -l minimaxClassic -a depth=4

<ul>

 <li>Pacman is always agent 0, and the agents move in order of increasing agent index.</li>

 <li>All states in minimax should be GameStates, either passed in to getAction or generated via generateSuccessor. In this project, you will not be abstracting to simplified states.</li>

 <li>On larger boards such as openClassic and mediumClassic (the default), you’ll find Pacman to be good at not dying, but quite bad at winning. He’ll often thrash around without making progress. He might even thrash around right next to a dot without eating it because he doesn’t know where he’d go after eating that dot. Don’t worry if you see this behavior, question 5 will clean up all of these issues.</li>

 <li>When Pacman believes that his death is unavoidable, he will try to end the game as soon as possible because of the constant penalty for living. Sometimes, this is the wrong thing to do with random ghosts, but minimax agents always assume the worst:</li>

</ul>

python pacman.py -p MinimaxAgent -l trappedClassic -a depth=3

Make sure you understand why Pacman rushes the closest ghost in this case.

<h1>Question 3 : Alpha-Beta Pruning</h1>

Make a new agent that uses alpha-beta pruning to more efficiently explore the minimax tree, in AlphaBetaAgent. Again, your algorithm will be slightly more general than the pseudocode from lecture, so part of the challenge is to extend the alpha-beta pruning logic appropriately to multiple minimizer agents.

You should see a speed-up (perhaps depth 3 alpha-beta will run as fast as depth 2 minimax) Ideally, depth 3 on smallClassic should run in just a few seconds per move or faster.

python pacman.py -p AlphaBetaAgent -a depth=3 -l smallClassic

The AlphaBetaAgent minimax values should be identical to the MinimaxAgent minimax values, although the actions it selects can vary because of different tie-breaking behavior Again, the minimax values of the initial state in the minimaxClassic layout are 9, 8, 7 and -492 for depths 1, 2, 3 and 4 respectively.

<em>Grading: </em>Because we check your code to determine whether it explores the correct number of states, it is important that you perform alpha-beta pruning without reordering children. In other words, successor states should always be processed in the order returned by GameState.getLegalActions. Again, do not call GameState.generateSuccessor more than necessary. The pseudo-code below represents the algorithm you should implement for this question.

<h1>Question 4 : Expectimax</h1>

Minimax and alpha-beta are great, but they both assume that you are playing against an adversary who makes optimal decisions. As anyone who has ever won tic-tac-toe can tell you, this is not always the case. In this question you will implement the ExpectimaxAgent, which is useful for modeling probabilistic behavior of agents who may make suboptimal choices. As with the search and constraint satisfaction problems covered so far in this class, the beauty of these algorithms is their general applicability.

Random ghosts are of course not optimal minimax agents, and so modeling them with minimax search may not be appropriate. ExpectimaxAgent, will no longer take the min over all ghost actions, but the expectation according to your agent’s model of how the ghosts act. To simplify your code, assume you will only be running against an adversary which chooses amongst their getLegalActions uniformly at random.

To see how the ExpectimaxAgent behaves in Pacman, run:

python pacman.py -p ExpectimaxAgent -l minimaxClassic -a depth=3

You should now observe a more cavalier approach in close quarters with ghosts. In particular, if Pacman perceives that he could be trapped but might escape to grab a few more pieces of food, he’ll at least try. Investigate the results of these two scenarios:

python pacman.py -p AlphaBetaAgent -l trappedClassic -a depth=3

-q -n 10 python pacman.py -p ExpectimaxAgent -l trappedClassic -a depth=3 -q -n 10

You should find that your ExpectimaxAgent wins about half the time, while your AlphaBetaAgent always loses. Make sure you understand why the behavior here differs from the minimax case.

The correct implementation of expectimax will lead to Pacman losing some of the tests. This is not a problem: as it is correct behaviour, it will pass the tests.

<h1>Question 5 : Evaluation Function</h1>

Write a better evaluation function for pacman in the provided function betterEvaluationFunction. The evaluation function should evaluate states, rather than actions like your reflex agent evaluation function did. You may use any tools at your disposal for evaluation, including your search code from the last project. With depth 2 search, your evaluation function should clear the smallClassic layout with one random ghost more than half the time and still run at a reasonable rate (to get full credit, Pacman should be averaging around 1000 points when he’s winning).

<em>Grading: </em>OJ will run your agent on the smallClassic layout 10 times. We will assign points to your evaluation function in the following way:

<ul>

 <li>Win at least once without timing out the OJ</li>

 <li>Winning all 10 times.</li>

 <li>An average score of at least 1000</li>

 <li>Take on average less than 30 seconds on OJ</li>

</ul>