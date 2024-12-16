# idontbelieveit
This repository is dedicated to the course of Advanced Technologies and Application Development

# Solve me first (Easy)
1. Importing the I/O Module
- use std::io;
-- The std::io module provides functionalities for input and output operations, such as reading user input and writing output to the console.
-- In this case, it allows us to read user input from the standard input (keyboard).

2. Main Function
fn main() {
- The main function is the entry point of the program. When the program runs, execution starts here.

3. Variable Declaration
let mut _num_str_1 = String::new();
let mut _num_str_2 = String::new();
- Declares two mutable (mut) variables, _num_str_1 and _num_str_2, and initializes them with an empty String.
- String::new() creates an empty String object that will later store user input.
- The underscore (_) at the start of the variable names indicates that the variables are not necessarily expected to be used further, though this convention is not strictly followed here.

4. Reading Input
io::stdin().read_line(&mut _num_str_1).ok().expect("read error");
io::stdin().read_line(&mut _num_str_2).ok().expect("read error");
- io::stdin(): Captures standard input from the user (keyboard input).
- read_line(&mut _num_str_1): Reads a line of input from the user and stores it in _num_str_1.
The &mut means that _num_str_1 is passed as a mutable reference, so the function can modify its value.
- .ok(): Returns an Option type to check if the read operation was successful.
- .expect("read error"): If the read_line operation fails, the program panics and displays the message "read error". This ensures the program doesn't continue with invalid input.

5. Parsing Input into Integers
let mut _num_1: i32 = _num_str_1.trim().parse().ok().expect("parse error");
let mut _num_2: i32 = _num_str_2.trim().parse().ok().expect("parse error");
- _num_str_1.trim(): Removes any leading/trailing whitespace or newline characters from the input string (e.g., "\n" from pressing "Enter").
- .parse(): Converts the trimmed string into an integer (i32 in this case).
- .ok(): Checks if the conversion is successful, returning an Option.
- .expect("parse error"): If the parsing fails (e.g., input is not a valid number), the program panics and displays "parse error".

6. Printing the Sum
println!("{}", _num_1 + _num_2);
- println!: Outputs formatted text to the console.
- {}: Placeholder for the result of _num_1 + _num_2.
- This line calculates the sum of the two parsed integers and prints the result to the console.

How the Code Works Overall
1. The program declares two empty strings to hold user input.
2. It reads two lines of input from the user (each representing a number).
3. The input strings are trimmed and converted to integers.
4. It calculates the sum of the two integers.
5. The sum is printed to the console.

Example Input and Output
Input:
5
10

Execution Steps:
_num_str_1 becomes "5\n", trimmed to "5", parsed to 5.
_num_str_2 becomes "10\n", trimmed to "10", parsed to 10.
Output:
15

# Simple array sum (easy)
Imports
use std::env;
use std::fs::File;
use std::io::{self, BufRead, Write};
- std::env: Provides access to environment variables (used to retrieve OUTPUT_PATH).
- std::fs::File: Used for file operations, such as creating or writing to a file.
- std::io: Used for handling input and output operations.
- BufRead: Enables efficient line-by-line reading of input.
- Write: Enables writing to files or other output streams.

The simpleArraySum Function
fn simpleArraySum(ar: &[i32]) -> i32 {
    ar.iter().sum()
}
- Parameters:
  ar: &[i32]: Accepts a slice of integers (&[i32]) as input.
- Logic:
  ar.iter(): Creates an iterator over the elements of the array ar.
  .sum(): Sums up all the elements in the iterator and returns the result.
- Returns:
The sum of the integers in the input array.

The main Function
1. Reading Input
let stdin = io::stdin();
let mut stdin_iterator = stdin.lock().lines();
- io::stdin(): Captures standard input.
- stdin.lock(): Locks the input for efficient reading.
- stdin.lock().lines(): Reads input line by line, returning an iterator where each line is wrapped in a Result<String>.

2. Creating Output File
let mut fptr = File::create(env::var("OUTPUT_PATH").unwrap()).unwrap();
- env::var("OUTPUT_PATH"): Retrieves the value of the OUTPUT_PATH environment variable, which specifies the file path where the output will be written.
  .unwrap(): Panics if the environment variable is not set or invalid.
- File::create(...): Creates a new file at the path specified by OUTPUT_PATH. If the file already exists, it is overwritten.
- .unwrap(): Panics if the file creation fails.

3. Parsing Input
let _ar_count = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();
- stdin_iterator.next(): Reads the next line from the input iterator.
  .unwrap(): Panics if no line is available or an error occurs.
- .trim(): Removes leading and trailing whitespace or newline characters from the line.
- .parse::<i32>(): Converts the trimmed string into an i32 integer.
.unwrap(): Panics if parsing fails.
_ar_count: Stores the number of elements in the array (though it is not used in the program).

let ar: Vec<i32> = stdin_iterator.next().unwrap().unwrap()
    .trim_end()
    .split(' ')
    .map(|s| s.to_string().parse::<i32>().unwrap())
    .collect();
    
- stdin_iterator.next(): Reads the next line from the input.
- .trim_end(): Removes trailing whitespace or newline characters from the line.
- .split(' '): Splits the line into substrings using spaces as the delimiter.
- .map(|s| s.to_string().parse::<i32>().unwrap()):
   Converts each substring (s) into a String.
   Parses the String into an integer (i32).
   .unwrap(): Panics if parsing fails.
- .collect(): Collects the parsed integers into a vector (Vec<i32>).
  
4. Calculating the Result
let result = simpleArraySum(&ar);
- Passes the array reference (&ar) to the simpleArraySum function.
- Stores the sum of the array elements in result.

6. Writing the Output
writeln!(&mut fptr, "{}", result).ok();
- writeln!: Writes formatted output (e.g., the result value) to a file or output stream.
- &mut fptr: Specifies the file handle as the output target.
- "{}": A placeholder for the value of result.
- .ok(): Silently ignores any errors while writing to the file.

How the Code Works Overall
1. Reads input from standard input:
   - The first line contains the number of elements in the array (not used in calculations).
   - The second line contains the space-separated integers of the array.
2. Parses the input into a vector of integers (ar).
3. Calls simpleArraySum to compute the sum of the array.
4. Writes the result to a file specified by the OUTPUT_PATH environment variable.

Example Input and Output
Input:
5
1 2 3 4 5

Execution Steps:
_ar_count = 5 (not used).
ar = [1, 2, 3, 4, 5].
result = 1 + 2 + 3 + 4 + 5 = 15.

Output (written to the file specified by OUTPUT_PATH):
15

# Compare the triplets (easy)
The compareTriplets Function
fn compareTriplets(a: &[i32], b: &[i32]) -> Vec<i32> {
    let mut alice_score = 0;
    let mut bob_score = 0;

    for (a_val, b_val) in a.iter().zip(b.iter()) {
        if a_val > b_val {
            alice_score += 1;
        } else if a_val < b_val {
            bob_score += 1;
        }
    }

    vec![alice_score, bob_score]
}

Function Purpose
- Compares two arrays of integers (a and b), representing scores from Alice and Bob for multiple categories.
- Returns a vector containing two integers:
  First integer: Alice's total score.
  Second integer: Bob's total score.

Key Points
1. Parameters:
   a: &[i32]: A slice of integers representing Alice's scores.
   b: &[i32]: A slice of integers representing Bob's scores.
   
3. Logic:
   a.iter().zip(b.iter()):
     Combines the two slices into pairs of corresponding elements.
     For example, if a = [5, 6, 7] and b = [3, 6, 10], it produces [(5, 3), (6, 6), (7, 10)].
     For each pair:
       If Alice's score is greater (a_val > b_val), increase alice_score.
       If Bob's score is greater (a_val < b_val), increase bob_score.
     If scores are equal, no points are awarded.

3. Return Value:
   The scores are returned as a vector: vec![alice_score, bob_score].

The main Function
1. Reading Input
let stdin = io::stdin();
let mut stdin_iterator = stdin.lock().lines();
- io::stdin(): Captures standard input.
- stdin.lock().lines(): Reads input line by line, returning an iterator where each line is a Result<String>.

2. Creating the Output File
let mut fptr = File::create(env::var("OUTPUT_PATH").unwrap()).unwrap();
- env::var("OUTPUT_PATH"):
  Retrieves the value of the OUTPUT_PATH environment variable, which specifies the path of the file where the output will be written.
  .unwrap(): Panics if the variable is not set or invalid.
- File::create(...):
  Creates a new file at the specified path. Overwrites the file if it already exists.
  .unwrap(): Panics if the file cannot be created.

3. Parsing Input
let a: Vec<i32> = stdin_iterator.next().unwrap().unwrap()
    .trim_end()
    .split(' ')
    .map(|s| s.to_string().parse::<i32>().unwrap())
    .collect();

- Reads the first line of input (Alice's scores):
  stdin_iterator.next(): Retrieves the next line of input.
  .unwrap(): Panics if no line is available or an error occurs.
  .trim_end(): Removes trailing whitespace or newline characters from the line.
  .split(' '): Splits the line into substrings using spaces as the delimiter.
  .map(|s| s.to_string().parse::<i32>().unwrap()):
     Converts each substring into a String and parses it into an integer (i32).
     Panics if parsing fails.
  .collect(): Collects the parsed integers into a vector (Vec<i32>).
- Similarly, parses the second line of input (Bob's scores) into vector b.

4. Calling compareTriplets
let result = compareTriplets(&a, &b);
- Calls compareTriplets with references to a and b.
- Stores the result (scores of Alice and Bob) in the result vector.

5. Writing Output
for i in 0..result.len() {
    write!(&mut fptr, "{}", result[i]).ok();

    if i != result.len() - 1 {
        write!(&mut fptr, " ").ok();
    }
}
writeln!(&mut fptr).ok();

- Iterates over the result vector and writes each score to the output file:
  write!(&mut fptr, "{}"): Writes the current score to the file.
  If it is not the last score, a space is appended after it.
- writeln!(&mut fptr):
  Writes a newline to the file after the scores.

How the Code Works Overall
- Reads two lines of input:
  First line: Alice's scores (a).
  Second line: Bob's scores (b).
- Parses the input into vectors a and b.
- Compares the scores using compareTriplets:
  Iterates over corresponding elements in a and b.
  Updates scores for Alice and Bob based on the comparisons.
- Writes the results (Alice's and Bob's scores) to the file specified by OUTPUT_PATH.

Example Input and Output
Input:
5 6 7
3 6 10

Execution Steps:
1. Parse a = [5, 6, 7] and b = [3, 6, 10].
2. Compare:
   First category: 5 > 3, Alice gets 1 point.
   Second category: 6 == 6, no points.
   Third category: 7 < 10, Bob gets 1 point.
3. Result: [1, 1] (Alice: 1, Bob: 1).

Output (written to the file):
1 1

# A very big sum (easy)
The aVeryBigSum Function
fn aVeryBigSum(ar: &[i64]) -> i64 {
    ar.iter().sum()
}

Purpose
- Computes the sum of an array of integers, specifically 64-bit integers (i64), which can handle very large numbers.

Steps
- ar.iter():
  Creates an iterator over the elements of the array ar.
- .sum():
  Computes the sum of all elements in the iterator and returns the result.
- Return Value:
  The total sum of the array elements as an i64 integer.

The main Function
1. Standard Input Setup
let stdin = io::stdin();
let mut stdin_iterator = stdin.lock().lines();
- io::stdin():
  Captures standard input.
- stdin.lock().lines():
  Locks the standard input and enables reading it line by line. Returns an iterator where each line is a Result<String>.

2. Creating an Output File
let mut fptr = File::create(env::var("OUTPUT_PATH").unwrap()).unwrap();
- env::var("OUTPUT_PATH"):
  Retrieves the value of the OUTPUT_PATH environment variable, which specifies the path of the output file.
  .unwrap():
  Panics if the environment variable is not set or invalid.
- File::create(...):
  Creates a new file at the specified path. Overwrites the file if it already exists.
  .unwrap():
    Panics if the file cannot be created.

3. Reading the Number of Elements
let _ar_count = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();
- stdin_iterator.next():
  Reads the next line from the input iterator.
- .unwrap().unwrap():
  The first .unwrap() extracts the Result, and the second .unwrap() extracts the Option value.
  Panics if no line is available or an error occurs.
- .trim():
  Removes leading and trailing whitespace or newline characters.
- .parse::<i32>():
  Converts the trimmed string into a 32-bit integer.
  Panics if parsing fails.
- _ar_count:
  Holds the number of elements in the array (but is not used in this program).

4. Parsing the Array of Numbers
let ar: Vec<i64> = stdin_iterator.next().unwrap().unwrap()
    .trim_end()
    .split(' ')
    .map(|s| s.to_string().parse::<i64>().unwrap())
    .collect();

- Reads the second line of input, which contains space-separated integers.
- .trim_end():
Removes trailing whitespace or newline characters from the line.
- .split(' '):
  Splits the string into substrings using spaces as the delimiter.
- .map(|s| s.to_string().parse::<i64>().unwrap()):
  For each substring:
    Converts it into a String.
    Parses it as a 64-bit integer (i64).
    Panics if parsing fails.
- .collect():
  Collects the parsed integers into a vector (Vec<i64>).

5. Calling aVeryBigSum
let result = aVeryBigSum(&ar);
- Passes the reference of the vector ar to the aVeryBigSum function.
- Stores the result (the sum of the array elements) in the variable result.

6. Writing the Output
writeln!(&mut fptr, "{}", result).ok();
- writeln!:
  Writes the value of result to the output file, followed by a newline.
- &mut fptr:
  Specifies the output file as the target.
- .ok():
  Silently ignores any errors while writing to the file.

How the Code Works Overall
1. Reads two lines of input:
   First line: The number of elements in the array (not used in the program).
   Second line: Space-separated integers to be summed.
2. Parses the integers into a vector ar of type i64.
3. Passes the vector to aVeryBigSum to compute the sum.
4. Writes the result (the sum) to a file specified by the OUTPUT_PATH environment variable.

Example Input and Output
Input:
5
1000000001 1000000002 1000000003 1000000004 1000000005

Execution Steps:
Parse _ar_count = 5 (not used).
Parse ar = [1000000001, 1000000002, 1000000003, 1000000004, 1000000005].
Compute result = 1000000001 + 1000000002 + 1000000003 + 1000000004 + 1000000005 = 5000000015.

Output (written to the file):
5000000015

# Diagonal difference (easy)
The diagonalDifference Function
rust
Copy code
fn diagonalDifference(arr: &[Vec<i32>]) -> i32 {
    let n = arr.len(); // Size of the square matrix
    let mut primary_diagonal_sum = 0;
    let mut secondary_diagonal_sum = 0;
    
    for i in 0..n {
        primary_diagonal_sum += arr[i][i];            // Primary diagonal
        secondary_diagonal_sum += arr[i][n - i - 1]; // Secondary diagonal
    }

    // Return the absolute difference
    (primary_diagonal_sum - secondary_diagonal_sum).abs()
}
Purpose
- Computes the absolute difference between the sums of the primary diagonal and the secondary diagonal of a square matrix.

Steps
1. Determine Matrix Size (n):
   let n = arr.len();
   Calculates the size of the matrix (number of rows or columns, since it's a square matrix).

2. Initialize Diagonal Sums:
   let mut primary_diagonal_sum = 0;
   let mut secondary_diagonal_sum = 0;
   These variables will store the sum of the primary and secondary diagonals, respectively.

3. Iterate Through the Matrix:
for i in 0..n {
    primary_diagonal_sum += arr[i][i];            // Primary diagonal
    secondary_diagonal_sum += arr[i][n - i - 1]; // Secondary diagonal
}

- The for loop iterates over each row index i.
- Primary Diagonal (arr[i][i]):
  Adds the element at row i and column i to primary_diagonal_sum.
- Secondary Diagonal (arr[i][n - i - 1]):
  Adds the element at row i and column (n - i - 1) to secondary_diagonal_sum.
  This calculates the reverse diagonal.

4. Return Absolute Difference:
- (primary_diagonal_sum - secondary_diagonal_sum).abs()
- Computes the difference between the two sums and returns its absolute value.

The main Function
1. Standard Input Setup
let stdin = io::stdin();
let mut stdin_iterator = stdin.lock().lines();
- Reads input from standard input line by line.

2. Create an Output File
let mut fptr = File::create(env::var("OUTPUT_PATH").unwrap()).unwrap();
- Creates an output file at the path specified by the OUTPUT_PATH environment variable.

3. Read the Matrix Size (n)
let n = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();
- Reads the first line of input, which contains the size of the square matrix (n).
- .parse::<i32>():
  Converts the string to a 32-bit integer.

4. Initialize the Matrix (arr)
let mut arr: Vec<Vec<i32>> = Vec::with_capacity(n as usize);
- Initializes a 2D vector arr to represent the matrix.
- Vec::with_capacity(n as usize):
  Allocates memory for n rows.

5. Read Matrix Rows
for i in 0..n as usize {
    arr.push(Vec::with_capacity(n as usize));

    arr[i] = stdin_iterator.next().unwrap().unwrap()
        .trim_end()
        .split(' ')
        .map(|s| s.to_string().parse::<i32>().unwrap())
        .collect();
}

- Iterates n times to read each row of the matrix:
  1. arr.push(Vec::with_capacity(n as usize)):
     Prepares memory for each row.
  2. stdin_iterator.next():
     Reads the next line of input.
  3. trim_end():
     Removes trailing whitespace or newline characters.
  4. split(' '):
     Splits the line into space-separated numbers.
  5. .map(|s| s.to_string().parse::<i32>().unwrap()):
     Converts each substring into a 32-bit integer (i32).
  6. .collect():
     Collects the parsed integers into a vector, representing a row of the matrix.
  7. arr[i]:
     Assigns the row vector to the ith position in the matrix.

6. Compute the Result
let result = diagonalDifference(&arr);
- Calls the diagonalDifference function with a reference to the matrix arr.
=- Stores the computed difference in result.

7. Write the Result to the File
writeln!(&mut fptr, "{}", result).ok();
- Writes the result to the output file specified by fptr.

How the Code Works Overall
1. Reads:
   The size of the square matrix n.
   The matrix elements (space-separated integers for each row).
2. Constructs the matrix as a 2D vector (arr).
3. Computes the absolute difference between the sums of the primary and secondary diagonals using the diagonalDifference function.
4. Writes the result to a file.

Example Input and Output
Input:
3
11 2 4
4 5 6
10 8 -12

Execution Steps:
1. n = 3
2. Parse arr:
arr = [
    [11, 2, 4],
    [4, 5, 6],
    [10, 8, -12]
]

3. Compute sums:
   Primary diagonal: 11 + 5 + (-12) = 4
   Secondary diagonal: 4 + 5 + 10 = 19

4. Compute absolute difference:
|4 - 19| = 15

Output (written to the file):
15
