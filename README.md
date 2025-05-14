# monteCarlo Simulator
DS5100 Final Project
Hariss Rai

Install numpy and pandas before installing this.


Installation
pip install MonteCarloMain 
  or pip install e-. in package folder
from monteCarloMain import Die, Game, Analyzer


Die Class
# Create a six-sided die
my_die = Die([1, 2, 3, 4, 5, 6])

# Create a coin (Heads or Tails) and weight it towards Heads
weighted_coin = Die(['Heads', 'Tails'])
weighted_coin.modify_weight('Heads', 0.75)

# Roll a die
weighted_coin.roll()

# Show roll sides + weighta
show_weights(weighted_coin)

Game Class

# Play 88 games
flip = show_weights.play(88)
 # Get roll results
flip.get_results()

Die Class

# Calc number of Jackpots (all the same result)
flip.calculate_jackpot()

# Get dataframe of rolls that were jackpots
flip.get_jackpot_rolls()

# Calculate combinations of rolls
calculate_combinations.roll()

# calculate permutation of rolls
flip.calculate_combinations(include_permutations=True)

# Get datafram for freq of combinations/perms
flip.get_combinations_data()

# Counts how many times each face value appears in each roll across all dice
flip.count_faces_per_roll()

# Get counts of each face per roll.
flip.get_face_counts_data()





API Description
This section details the public classes and methods available in the Monte Carlo Simulator library.

##Class: Die

Represents a single die with a set of sides and associated weights.

#__init__(self, sides)

Description: Initializes a new Die object with the given sides and default weights (Default weight 1.0).
  Parameters:
sides (list or numpy.ndarray): A list or array of values representing the faces of the die.
Raises:
TypeError: If sides is not a list or numpy.ndarray.
ValueError: If sides is empty or contains non-unique values.
Returns: None

#modify_weight(self, side_value, new_weight)

Description: Updates the weight for a specific side of the die.
Parameters:
side_value: The value of the side whose weight is updated.
new_weight (float): New weight for the specified side, must be >0.
Raises:
ValueError: If side_value does not exist on the die, or if new_weight is not >0 or cannot be converted to a float.
Returns: None

#roll(self, num_rolls=1)

Description: Rolls the die a specified number of times. The outcome of each roll is determined by the weights assigned to each side.
Parameters:
num_rolls (int, optional): The number of times to roll the die. Must be a positive integer. Defaults to 1.
Raises:
ValueError: If num_rolls &lt; 1.
Returns:
list: list containing the results of each roll.

#show_weights(self)

Description: Display sides of die + current weights.
Parameters: None
Returns:
pandas.DataFrame: A DataFrame with 'side' and 'weight' columns.

##Class: Game

Represents a game involving one or more dice.

#__init__(self, dice_list)

Description: Initializes new Game object with a list of Die objects.
Parameters:
dice_list (list): A list of Die objects.
Raises:
TypeError: If dice_list is not a list or has non-Die objects.
ValueError: If dice_list is empty.
Returns: None

#play(self, num_rolls)

Description: Rolls each die in the game a specified number of times.
Parameters:
num_rolls (int): The number of times to roll each die, must be a positive integer.
Raises:
ValueError: If num_rolls is not a positive integer.
Returns: None

#get_results(self, format_type="wide")

Description: Returns the results of the most recent game rolls in the specified format.
Parameters:
format_type (str, optional): Desired format for the results, accepts 'wide' or 'narrow'. Defaults to 'wide'.
'wide': Returns a DataFrame where rows = roll numbers and columns = dice, cell values = the rolled face. Shape = (num_rolls x num_dice).
'narrow': Returns a DataFrame with a MultiIndex (Roll, Die) and a single column, 'Rolled Face'. Shape: (num_rolls * num_dice x 1).
Raises:
ValueError: If format_type is not 'wide' or 'narrow'.
Returns:
pandas.DataFrame: DataFrame with the roll results in the specified format.

##Class: Analyzer

Allows calculating jackpots, combinations/permutations, and face counts from the game's roll results.

#__init__(self, game)

Description: Initializes the Analyzer with a Game object.
Parameters:
game (Game): The Game object whose results will be analyzed.
Raises:
TypeError: If game isn't a Game object.
Returns: None

#calculate_jackpot(self)

Description: Identifies and counts all "jackpot" rolls (where all dice show the same face).
Parameters: None
Returns:
int: The total number of jackpot rolls found.

#get_jackpot_rolls(self)

Description: Returns the DataFrame containing the rolls that resulted in a jackpot.
Parameters: None
Returns:
pandas.DataFrame: A DataFrame with the jackpot rolls.

#calculate_combinations(self, include_permutations=False)

Description: Computes the frequencies of combinations or permutations of dice rolls.
Parameters:
include_permutations (bool, optional): If True, counts are based on the ordered tuple (permutation). If False (default), counts are based on sorted tuples ignoring the order of faces within a roll. Defaults to False.
Returns:
pandas.DataFrame: A DataFrame with index from face-tuples with a 'Frequency' column.

#get_combinations_data(self)

Description: Returns the DataFrame containing the frequencies of combinations/permutations.
Parameters: None
Returns:
pandas.DataFrame: A DataFrame with combination/permutation frequencies.

#count_faces_per_roll(self)

Description: Counts how many times each face value appears in each roll across all dice.
Parameters: None
Returns:
pandas.DataFrame: DataFrame where rows = roll numbers, columns = face values, and entries = counts of each face in that specific roll.

#get_face_counts_data(self)

Description: Returns the DataFrame containing the counts of each face per roll.
Parameters: None
Returns: pandas.DataFrame: DataFrame with face counts per roll.
