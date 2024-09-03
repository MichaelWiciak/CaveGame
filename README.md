# Cave Game

## Overview
This project is a simple cave exploration game where the player controls a character named Tom, navigating a grid-based cave system filled with obstacles and items. The game is implemented in C++ and consists of several interdependent classes to manage game mechanics, map generation, and command processing.

## Compilation and Execution
To compile and run the game, ensure all source files are in the same directory and then use the following commands:

```bash
g++ -o cave_game main.cpp cave.cpp command.cpp location.cpp move.cpp place.cpp test.cpp tom.cpp
./cave_game
```

The game is designed to run in a command-line interface (CLI). The player inputs commands to move Tom around the cave or interact with the environment.

## Code Structure

### Main Components

1. **Cave Class (`cave.cpp`)**:
   - **Constructor:** Initializes an 8x8 grid of `Location` objects representing the cave map. The map is bordered by `Rock` objects, and Tom is placed at the center.
   - **Destructor:** Attempts to delete dynamically allocated memory for the cave map, though some memory management issues (marked as `fixme`) need attention.
   - **Command Processing:** Handles user commands by invoking appropriate actions (`Move`, `Place`).
   - **Display:** Renders the cave grid to the console, showing Tom's position and any objects at each location.

2. **Command Class (`command.h`)**:
   - Acts as a base class for specific user commands like `Move` and `Place`.
   - **triggersOn():** Determines if the user's input matches the command's trigger word.
   - **fire():** A pure virtual function, to be overridden by derived classes, executing the command logic.

3. **Location Class (`location.cpp`)**:
   - **show():** Determines and returns a character representation for the location based on the objects present (e.g., rocks, Tom).
   - **add() and remove():** Manage the addition and removal of objects (`Thing` subclasses) from the location.
   - **isBlocking():** Checks if the location contains any blocking objects (e.g., `Rock`), which would prevent Tom from entering.

4. **Move Class (`move.cpp`)**:
   - **fire():** Handles Tom's movement based on user input. Validates movement to ensure Tom doesn’t walk into blocked or out-of-bound locations.

5. **Place Class (`place.cpp`)**:
   - **fire():** Allows Tom to place items such as coins or mushrooms at his current location.

6. **Testing (`test.cpp`)**:
   - A series of unit tests for validating the behavior of the game, including movement logic, map generation, and item placement. The tests check for correct initialization, boundary conditions, and object interactions.

### Memory Management
The project involves dynamic memory allocation for managing the cave grid and its contents. While the `Cave` class attempts to delete allocated memory in its destructor, the current implementation may not fully clean up all allocated resources, as indicated by `fixme` comments in the destructor.

### Important Notes
- The cave grid is fixed at 8x8. Adjustments to the grid size will require significant modifications to the `Cave::show()` method and potentially other parts of the code.
- The game relies on a basic text-based interface. User commands are typed directly into the console, and the game updates the display after each command.

### How the Project Works

The cave game project is a simple text-based simulation where the player navigates a character named Tom through an 8x8 grid representing a cave. The cave is populated with different objects like rocks, coins, and mushrooms. The player issues commands to move Tom around the cave or place objects in it. The game logic is implemented using a combination of classes that represent the cave, the objects within it, and the commands that control the game.

#### Key Components

1. **Cave Class (`cave.cpp`)**:
   - The `Cave` class represents the game environment, an 8x8 grid where each cell is a `Location` object.
   - The cave's size is currently hard-coded to 8x8, with boundary checks to ensure it does not run outside these dimensions.
   - The cave is initialized with rocks around its borders, and Tom starts in the center of the cave.

2. **Location Class (`location.cpp`)**:
   - Each `Location` object represents a cell in the cave grid.
   - A `Location` can contain multiple objects (things) such as rocks, coins, and Tom himself.
   - The `show()` method of `Location` determines the character representation of the cell based on the contents, like 'X' for a blocking object, '.' for empty space, and '|' or 'L' for Tom's presence.

3. **Thing Class**:
   - `Thing` is a base class representing objects that can be placed in the cave.
   - Derived classes like `Rock`, `Coin`, and `Mushroom` inherit from `Thing` and have specific behaviors or representations.

4. **Tom Class (`tom.cpp`)**:
   - Tom is the character that the player controls.
   - Tom's position is tracked and updated within the cave as he moves around.

5. **Command Handling (`command.h`, `move.cpp`, `place.cpp`)**:
   - The `Command` class serves as a base for various commands the player can issue, such as moving Tom or placing objects.
   - The `Move` class handles movement commands, adjusting Tom's position within the cave grid.
   - The `Place` class manages the placement of items like coins or mushrooms at Tom's current location.

6. **Main Execution Flow (`main.cpp`)**:
   - The main program loop runs in `main.cpp`, where the cave is initialized, and the player is prompted to enter commands.
   - The game continues to accept commands until the player chooses to exit.

7. **Testing (`test.cpp`)**:
   - A series of tests are implemented to verify the correct functionality of the game components, including movement, object placement, and the behavior of the cave environment under different conditions.
   - The tests also check for edge cases, such as trying to move Tom into a wall or placing objects on top of each other.

#### Memory Management

- The project uses dynamic memory allocation for the cave grid and its objects. However, there are some known issues with memory management, particularly in the `Cave` destructor, where not all allocated memory is properly freed.
- Proper handling of object lifetimes and memory deallocation is crucial to avoid memory leaks, and this is an area that might need further refinement.

