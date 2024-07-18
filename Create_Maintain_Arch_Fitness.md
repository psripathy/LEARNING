Book - Building Evolutionary Architectures

Fitness Functions for Code
  - Unit Tests
  - Code Coverage
  - Number of Warnings (treat warnings as error if possible)
      * You can fail Ci build if the number of warning goes up or code coverage goes lower than the current threshold
  - Load Time

Architectural Fitness Functions
  - ArchUnit
    - Used to express architectural constraints on your system. You can write code similar to Junit
      - For example detect Cyclic Dependency, 
    - This becomes an Executable Documentation for the architetural constraints of your project
Simian, CPD from PMD to detect code duplication
