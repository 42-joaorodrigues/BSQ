# BSQ - Biggest Square

![42 Badge](https://img.shields.io/badge/42-BSQ-brightgreen)
![C Badge](https://img.shields.io/badge/Language-C-blue)
![Status Badge](https://img.shields.io/badge/Status-Completed-success)

## What I Learned

This final project of the C Piscine challenged me to develop advanced algorithmic thinking and optimize performance for large datasets:

- **Dynamic Programming** - Implemented efficient algorithms to find optimal solutions in 2D grids
- **Map Parsing & Validation** - Built robust input parsing with comprehensive error handling
- **Memory Management** - Handled large buffers and dynamic memory allocation for variable-sized maps
- **File I/O Operations** - Processed multiple file formats and standard input streams
- **Algorithm Optimization** - Developed brute-force and optimized approaches for square detection
- **Edge Case Handling** - Managed invalid maps, empty inputs, and boundary conditions
- **Modular Architecture** - Separated concerns across parsing, validation, solving, and utility modules
- **Performance Analysis** - Understood time complexity trade-offs in grid-based algorithms
- **Buffer Management** - Implemented dynamic buffer growth for unknown input sizes
- **Error Propagation** - Designed clean error handling throughout the entire pipeline

This project reinforced my ability to break down complex problems, implement efficient algorithms, and write production-quality C code with proper memory management.

## About the Project

BSQ (Biggest Square) finds the largest possible square that can be placed on a 2D map while avoiding obstacles. The program reads maps from files or standard input, validates the format, and outputs the solution with the square filled in.

## Problem Description

Given a map with:
- Empty spaces (represented by a character like '.')
- Obstacles (represented by a character like 'o') 
- A fill character for the solution (like 'x')

The algorithm must find the biggest square of empty spaces and fill it with the designated character.

## Map Format

The first line contains the map metadata:
```
[number_of_rows][empty_char][obstacle_char][full_char]
```

Example:
```
9.ox
...........................
....o......................
............o..............
...........................
....o......................
...............o...........
...........................
......o..............o.....
..o.......o................
```

## Algorithm Implementation

The program uses a **brute-force approach** with optimizations:

1. **Grid Traversal**: Iterates through each position as a potential top-left corner
2. **Square Expansion**: For each position, expands the square size until hitting an obstacle or boundary
3. **Boundary Checking**: Validates that the expanding square stays within map limits
4. **Obstacle Detection**: Stops expansion when encountering any obstacle within the square area
5. **Solution Selection**: Keeps track of the largest valid square found (prioritizing top-left positioning for ties)

### Key Algorithm Functions

```c
// Core solving function that finds the biggest square
void ft_solve(t_map *map);

// Checks if a square of given size can be placed at position (x,y)
bool ft_check(t_map *map, int x, int y, int expand);

// Expands square from position and updates best solution if larger
void ft_expand(t_map *map, int x, int y, t_square *square);

// Fills the final solution square with the designated character
void ft_print_result(t_map *map, t_square *square);
```

## Project Structure

```
BSQ/
├── Makefile          # Build configuration
├── main.c            # Entry point and program flow
├── map.h             # Data structures and function prototypes
├── parse.c           # File reading and map parsing
├── solver.c          # Core algorithm implementation
├── utils.c           # Utility functions (strlen, strdup, etc.)
└── validate.c        # Input validation and error handling
```

## Data Structures

```c
typedef struct s_map {
    int    rows;        // Number of rows in the map
    int    cols;        // Number of columns in the map
    char   empty;       // Character representing empty space
    char   obstacle;    // Character representing obstacles
    char   full;        // Character to fill the solution square
    char   **map;       // 2D array containing the map data
    bool   valid;       // Flag indicating if map is valid
} t_map;

typedef struct s_square {
    int size;           // Size of the square (width/height)
    int x;              // X coordinate of top-left corner
    int y;              // Y coordinate of top-left corner
} t_square;
```

## Features

- **Multiple Input Sources**: Handles both file arguments and standard input
- **Batch Processing**: Processes multiple map files in sequence
- **Comprehensive Validation**: Validates map format, characters, and dimensions
- **Error Handling**: Provides clear error messages for invalid inputs
- **Memory Management**: Properly allocates and frees dynamic memory
- **Large Buffer Support**: Handles maps up to 3MB in size

## Usage

```bash
# Compile the program
make

# Run with map files
./bsq map1.txt map2.txt map3.txt

# Run with standard input
./bsq < map.txt

# Generate test maps using the provided Perl script
perl map_generator.pl 50 50 3 > test_map.txt
./bsq test_map.txt
```

## Example Output

Input:
```
9.ox
...........................
....o......................
............o..............
...........................
....o......................
...............o...........
...........................
......o..............o.....
..o.......o................
```

Output:
```
.....xxxxxxx...............
....oxxxxxxx...............
.....xxxxxxxo..............
.....xxxxxxx...............
....oxxxxxxx...............
.....xxxxxxx...o...........
.....xxxxxxx...............
......o..............o.....
..o.......o................
```

## Algorithm Complexity

- **Time Complexity**: O(n²m²) where n×m is the map size
- **Space Complexity**: O(nm) for storing the map
- **Optimization**: Early termination when obstacles are encountered

## Technical Challenges Overcome

- **Large Input Handling** - Dynamic buffer growth for unknown input sizes
- **Memory Efficiency** - Minimal memory footprint while processing large maps
- **Parsing Robustness** - Handling various edge cases in map format
- **Algorithm Optimization** - Balancing between simplicity and performance
- **Error Recovery** - Graceful handling of invalid maps in batch processing

## Map Generator

The project includes a Perl script to generate test maps:

```perl
#!/usr/bin/perl
# Usage: perl generator.pl width height density
perl map_generator.pl 100 100 5 > large_map.txt
```

---

*This project was completed as the final challenge of the 42 School C Piscine, demonstrating proficiency in algorithm design, file processing, and complex C programming concepts.*

## License

This project is licensed under the [MIT License](./LICENSE).
