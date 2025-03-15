# Homework-1-PCLP1
A program in C that manages a fictional city with a very complicated postal system

The aim is to implement a system that functions according to the following specifications:
  - The city is divided into a maximum of 32 districts, each having exactly one postman.
  - A district is a structure that contains:
      ∗ id – an integer;
      ∗ name – a string (dynamically allocated char*) that cannot contain spaces.
  - A package is represented by a structure containing the following fields:
    * packageId – an integer;
    * address – an array of 18 elements (int[18]) containing only values 0 or 1;
    * districtId– an integer;
    * street – an integer;
    * number – an integer;
    * priority – a value from the set {1, 2, 3, 4, 5}, where:
          -> 5 = highest priority;
          -> 1 = lowest priority.
    * weight – a floating-point number (float);
    * message – a string (dynamically allocated char*) representing a short message accompanying the package:
          -> The message can contain only letters, digits, spaces, and punctuation marks (.,!?:)
          -> It must end with a newline ('\n').
    * messageCode – an integer calculated after the package is distributed (task I).
  - Each package has an address represented by a vector of 18 positions containing only values 0 or 1, with the following meaning:
    * The first 5 positions represent the District ID, the next 5 positions represent the street, the last 8 positions represent the number.
  - Each postman will have an id that matches the id of the district they are responsible for, and they must distribute the packages within that district. The structure defining a postman contains the following fields:
      * id – an integer in the range [0, 31], where 32 is the maximum number of postmen;
      * nrPackages – an integer in the range [0, 49], where 50 is the maximum number of packages a postman can distribute;
      * A vector containing the packages they need to deliver.
  - There is a chief postman who initially receives all the packages and is responsible for distributing them to the regular postmen, ensuring that each one receives the packages corresponding to their district.
  - After receiving the packages, the postmen:
      * Sort the packages they are responsible for based on:
        -> Priority – packages with higher priority are delivered first;
        -> Weight – if two packages have the same priority, the package with the greater weight is delivered first.
        -> Encode the message received with the package by reversing the order of words in the sentence and removing all punctuation marks.
        -> Calculate a code, which is the sum of the products between the ASCII code of each character and the position of that character within the string after the previous processing steps. The character positions are numbered starting from 0.
        -> The final code is obtained by computing: code MOD (number * street + 1)

The program must be able to solve one of 7 different tasks with these packages and postmen, depending on an initial input that the user will provide: an integer between 1 and 7. All functions must be included in the same .c file (no header linked files beside standard libraries). There can be as many auxiliary user-defined functions as needed.

The data must be inputted in this format:
  1. request - The number of the task that will be solved (1-7)
  2. nrDistricts - The number of districts/mailmen
  3. nrDistricts lines containing the names of each district (no whitespaces, newline at the end)
  4. nrPackages - The number of packages
  5. 4 lines for each package:
      * 18 integers (0 or 1, separated by one whitespace each)
      * The priority (1-5)
      * The weight (maximum 3 decimals)
      * The message on the package
 
Possible tasks:
  1. Check the reading of the input by printing it, first for all districts, then for each package
  2. Extract the address of each package, completing the corresponding field, and print the information
  3. Distribute the packages to the corresponding mailmen and check it by printing each mailman's packages
  4. Sort each mailman's packages and check it by printing them
  5. Encode the message of each package, as well as calculate the code of the package, and check it by printing them
  6. For every package with an ID that has at least a common digit with the ID of its postman, alter the code of the package this way:
       * Find the prime divisors between 2 and 31 of the postman ID (if the ID is 0 or 1, that value will be considered the only divisor)
       * In the binary representation of the package code, flip the bits in the positions represented by the previously determined divisors
       * Consider the order of the bits LSB -> MSB
  7. Give a score to each mailman, equal to the number of successfully delivered packages divided by the total number of packages. A package is successfully delivered only if its code is not altered by the algorithm described at Task 6
