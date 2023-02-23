# <h1 align="center">Flappybird-AI-Website</h1>



## <h2 align="center">animation.js</h2>

defining a "Game" object constructor and setting its prototype to an object with several methods. The Game object represents a game where a user controls a bird to avoid hitting pipes and obstacles to score points. The methods of the Game object include:

 - initGame: initializes the position of the pipes, the number of living birds, the current score, and whether the game is over. It also calls dashboard.initDashboard() and animation.initAnimation() to initialize the dashboard and animation of the game.
 - initGame: initializes the position of the pipes, the number of living birds, the current score, and whether the game is over. It also calls dashboard.initDashboard() and animation.initAnimation() to initialize the dashboard and animation of the game.
 - setTimer: sets a timer that calls updateGame periodically, with the period specified by dashboard.getSimSpeed().
 - setTimer: sets a timer that calls updateGame periodically, with the period specified by dashboard.getSimSpeed().
 - _movePipe: a private method that moves the pipes to the left and generates new pipes when they reach the left edge of the screen. It also updates the currentScore if the bird has passed a pipe.
 - _findNextPipe: a private method that finds the next pipe that the bird needs to avoid hitting.
 - _findNextPipe: a private method that finds the next pipe that the bird needs to avoid hitting.
 - _checkGameOver: a private method that checks if all the birds are dead, and if so, it sets a timer to wait for a period of time and then generates a new generation of birds to start a new game.

Overall, this is a game loop that periodically updates the state of the game, handles user input, and checks whether the game is over. The Game object also interacts with other objects, such as the dashboard and animation objects, to display information about the game to the user.



## <h2 align="center">bird.js</h2>

The fly method first checks whether the bird is still alive. If it is, it increments the fitness property by one, which represents the distance the bird has flown. It then uses a neural network to decide whether to make the bird fly or not. The neural network takes in three inputs: the normalized distance to the next pipe, the normalized distance from the bird's y-coordinate to the upper part of the pipe, and the normalized distance from the bird's y-coordinate to the upper part of the next pipe if it can foresee two pipes ahead. The neural network returns a binary output, which determines whether the bird should fly or not. If the output is 1, the bird's speed property is set to a negative value, causing it to fly upwards. If the output is 0 or if the bird is not alive, the speed property is incremented by the value of GRAVITY (a constant defined elsewhere in the code), causing the bird to fall downwards. Finally, the y property of the bird is updated by adding its speed property.



## <h2 align="center">generation.js</h2>

Its a Generation constructor function that represents a generation of birds in a game. Each generation consists of a number of Bird instances, and the purpose of the Generation object is to evolve these birds over successive generations using a genetic algorithm.

The Generation constructor function initializes a new generation of birds by creating an array of Bird instances and assigning them to the birds property of the Generation object. Each Bird instance is mutated using the mutate() method of its neural network to make them different from each other.

The nextGeneration() method is the main method of the Generation object. It evolves the birds by selecting the fittest birds from the current generation to be the parents of the next generation, and breeding new birds from these parents.

The nextGeneration() method first sorts the birds in the current generation by fitness, with the fittest birds first. It then sets the number of survivors for the next generation based on a value returned by the getSurvivorNum() method of a dashboard object. The remaining birds in the current generation are deleted from the birds array.

The method then sets the number of birds for the next generation based on a value returned by the getBirdNum() method of the dashboard object. If this value is less than the number of survivors, some of the survivors are deleted from the birds array.

The method then creates new birds by breeding pairs of parents randomly chosen from the survivors. The new birds are added to the birds array to fill it up to the required number of birds. Each new bird is created by calling the _breed() method.

The _breed() method takes two parent birds as arguments and creates a new bird that is a combination of the two parents. The new bird has a neural network that is a combination of the neural networks of its parents. The weights of the edges in the network are randomly chosen from the corresponding edges in the parent networks, with a bias towards the edges of the fitter parent. The activation function of the new network is set to the value returned by the getActivationFunction() method of the dashboard object.

The _breed() method also applies a mutation to the network of the new bird with a probability specified by the MUTATE_CHANCE property of the Data.generation object.

Finally, the init() method of each bird in the new generation is called to reset their fitness and other properties to their initial values, and the generationNum property of the Generation object is incremented to indicate that a new generation has been created.



## <h2 align="center">network.js</h2>

This JavaScript program defines a "Network" object with various properties and methods. The purpose of the "Network" object is to represent a neural network that can be used for machine learning tasks.

The "Network" object is created using a constructor function that initializes two properties: "nodeSize" and "nodes", and an empty array called "edges". "nodeSize" is set to a constant value that is defined in another file called "Data", which is an object that contains various constants and configuration values for the neural network. "nodes" is set to an empty array, and "edges" is also set to an empty array.

The "Network" object also has several methods that can be called on it. The first method is called "mutate", which is used to randomly modify the edges of the neural network. It does this by randomly selecting two nodes, and then either adding a new node between them, changing the weight of the existing edge between them, or adding a new edge between them. The exact probability of each of these actions is determined by various constants defined in the "Data" object.

The second method is called "getOutput", which calculates the output of the neural network given a set of input values. It does this by initializing the "nodes" array with the input values and other constants, and then iterating over each node in the neural network to calculate its output value based on its input values and the weights of its incoming edges. Finally, the output value of the neural network is returned as a boolean.

The third method is called "setActivation", which allows the activation function used by the neural network to be changed. The activation function is used to calculate the output of each node in the neural network, and different activation functions can be used depending on the nature of the problem being solved.

The remaining methods are all internal helper functions that are used by the other methods to modify and calculate the edges and nodes of the neural network. These include functions to change the weight of an existing edge, add a new edge, and add a new node between two existing nodes.

Finally, the program defines an object called "Activation", which contains various functions that can be used as activation functions for the neural network. The specific activation function used by the neural network is set using the "setActivation" method.



## <h2 align="center">Author</h2>

<p align="center">- [@Goku-bot](https://github.com/Goku-bot/)</p>
