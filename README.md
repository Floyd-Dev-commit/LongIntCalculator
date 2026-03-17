# Long Int Calculator

#1.Overview

An arbitrary-precision integer calculator designed to handle extremely large numbers that exceed the capacity of standard C++ data types. This project implements arithmetic operations including addition, subtraction, multiplication, and integer division using a custom doubly circular linked list data structure.

Data Structure DesignTo optimize processing speed and simplify operations, this calculator does not store a single digit per node. Instead, it groups digits into blocks of up to four decimal digits per node.The core Abstract Data Type (ADT) is a Doubly Circular Linked List with a Head Node (NodeOfDoubleList / DList).

Key Architectural Choices:4-Digit Grouping: Each node stores an int value representing up to 4 digits (e.g., 0000 to 9999).Sign Bit in Head Node: The head node does not store numerical data; instead, its data field acts as the sign flag for the entire long integer (+1 for positive, -1 for negative).Circular Traversal: The doubly circular nature allows for highly efficient $O(1)$ access to the tail node (least significant digits) via L->prior, which is highly advantageous for arithmetic operations that start from the lowest digit.

#2.Core Modules & Algorithm Details

The calculation logic is broken down into several independent modules :

Data Conversion (StringNumberToDList / DListToStringNumber): Parses user input strings from right to left, splitting them into 4-digit chunks and inserting them into the linked list. 

Output conversion automatically handles zero-padding for intermediate nodes.

Input Validation (LegalCheck): Checks for invalid characters and ensures the input strictly follows the comma-separated format (e.g., preventing omitted leading zeros in intermediate 4-digit chunks).

Addition (DListNumberAdd): Traverses two linked lists from the tail to the head, summing corresponding nodes and applying carry-over logic.

Subtraction (DListNumberMinus): To avoid code duplication, the subtraction module smartly transforms the operation and internally calls the addition function (DListNumberAdd).

Multiplication (DListNumberMulti): Optimizes the multiplication process by treating the linked list chunks as polynomials, multiplying components and storing them, followed by a normalization step.

Division (DListNumberDivision): Computes integer division (floor division). It implements a highly efficient algorithm utilizing binary search (x1 = (x1 + x2) / 2) and enumeration to quickly converge on the quotient.

Normalization (NumAdjust): A crucial utility function called after mathematical operations to clean up the resulting linked list (e.g., handling cross-node carries, borrowing, and stripping leading zero nodes).

#3.Environment & Setup
Ensure your compiler supports C++11 !!!
Language: C++
Standard: Requires C++11 or higher (utilizes the std::to_string library function).
IDE/Compiler: Developed and tested on Microsoft Visual Studio 2019 (Windows OS), but fully compatible with GCC/Clang.

Execution & Formatting
Run the executable. The program operates via an interactive terminal interface.
Input Rules: Numbers must be formatted in groups of 4 decimal digits separated by commas ,. Leading zeros in the middle groups cannot be omitted.

#4.File Structure

DouCirList.h: Header file containing the definition of the doubly circular linked list and basic ADT operations.


LongIntCalculator.cpp: Contains the core mathematical algorithms (Add, Minus, Multi, Division) and the interactive main function.
