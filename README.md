# idontbelieveit
This repository is dedicated to the course of Advanced Technologies and Application Development

# Solve me first (Easy)
1. Importing the I/O Module
   
use std::io;

- The std::io module provides functionalities for input and output operations, such as reading user input and writing output to the console.
- In this case, it allows us to read user input from the standard input (keyboard).

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
- read_line(&mut _num_str_1): Reads a line of input from the user and stores it in _num_str_1. The &mut means that _num_str_1 is passed as a mutable reference, so the function can modify its value.
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
1. Imports
   
use std::env;

use std::fs::File;

use std::io::{self, BufRead, Write};

- std::env: Provides access to environment variables (used to retrieve OUTPUT_PATH).
- std::fs::File: Used for file operations, such as creating or writing to a file.
- std::io: Used for handling input and output operations.
- BufRead: Enables efficient line-by-line reading of input.
- Write: Enables writing to files or other output streams.

2. The simpleArraySum Function

fn simpleArraySum(ar: &[i32]) -> i32 {

    ar.iter().sum()
}

- Parameters:
  - ar: &[i32]: Accepts a slice of integers (&[i32]) as input.
  
- Logic:
  - ar.iter(): Creates an iterator over the elements of the array ar.
  - .sum(): Sums up all the elements in the iterator and returns the result.
  
- Returns:
  - The sum of the integers in the input array.

3. The main Function

3.1. Reading Input
   
let stdin = io::stdin();

let mut stdin_iterator = stdin.lock().lines();

- io::stdin(): Captures standard input.
- stdin.lock(): Locks the input for efficient reading.
- stdin.lock().lines(): Reads input line by line, returning an iterator where each line is wrapped in a Result<String>.

3.2. Creating Output File

let mut fptr = File::create(env::var("OUTPUT_PATH").unwrap()).unwrap();

- env::var("OUTPUT_PATH"): Retrieves the value of the OUTPUT_PATH environment variable, which specifies the file path where the output will be written.
  - .unwrap(): Panics if the environment variable is not set or invalid.
- File::create(...): Creates a new file at the path specified by OUTPUT_PATH. If the file already exists, it is overwritten.
- .unwrap(): Panics if the file creation fails.

3.3. Parsing Input
   
let _ar_count = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();

- stdin_iterator.next(): Reads the next line from the input iterator.
  - .unwrap(): Panics if no line is available or an error occurs.
- .trim(): Removes leading and trailing whitespace or newline characters from the line.
- .parse::<i32>(): Converts the trimmed string into an i32 integer.
  - .unwrap(): Panics if parsing fails.
- _ar_count: Stores the number of elements in the array (though it is not used in the program).

let ar: Vec<i32> = stdin_iterator.next().unwrap().unwrap()

    .trim_end()
    
    .split(' ')
    
    .map(|s| s.to_string().parse::<i32>().unwrap())
    
    .collect();
    
- stdin_iterator.next(): Reads the next line from the input.
- .trim_end(): Removes trailing whitespace or newline characters from the line.
- .split(' '): Splits the line into substrings using spaces as the delimiter.
- .map(|s| s.to_string().parse::<i32>().unwrap()):
  - Converts each substring (s) into a String.
  - Parses the String into an integer (i32).
  - .unwrap(): Panics if parsing fails.
- .collect(): Collects the parsed integers into a vector (Vec<i32>).

3.4. Calculating the Result
   
let result = simpleArraySum(&ar);

- Passes the array reference (&ar) to the simpleArraySum function.
- Stores the sum of the array elements in result.

3.5. Writing the Output
   
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
1. The compareTriplets Function

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
  - First integer: Alice's total score.
  - Second integer: Bob's total score.

Key Points
1. Parameters:
   - a: &[i32]: A slice of integers representing Alice's scores.
   - b: &[i32]: A slice of integers representing Bob's scores.
   
3. Logic:
   - a.iter().zip(b.iter()):
     - Combines the two slices into pairs of corresponding elements.
     - For example, if a = [5, 6, 7] and b = [3, 6, 10], it produces [(5, 3), (6, 6), (7, 10)].
   - For each pair:
     - If Alice's score is greater (a_val > b_val), increase alice_score.
     - If Bob's score is greater (a_val < b_val), increase bob_score.
   - If scores are equal, no points are awarded.

3. Return Value:
   - The scores are returned as a vector: vec![alice_score, bob_score].

The main Function
1. Reading Input
   
let stdin = io::stdin();
let mut stdin_iterator = stdin.lock().lines();
- io::stdin(): Captures standard input.
- stdin.lock().lines(): Reads input line by line, returning an iterator where each line is a Result<String>.

2. Creating the Output File
let mut fptr = File::create(env::var("OUTPUT_PATH").unwrap()).unwrap();
- env::var("OUTPUT_PATH"):
  - Retrieves the value of the OUTPUT_PATH environment variable, which specifies the path of the file where the output will be written.
  - .unwrap(): Panics if the variable is not set or invalid.
- File::create(...):
  - Creates a new file at the specified path. Overwrites the file if it already exists.
  - .unwrap(): Panics if the file cannot be created.

3. Parsing Input
   
let a: Vec<i32> = stdin_iterator.next().unwrap().unwrap()
    .trim_end()
    .split(' ')
    .map(|s| s.to_string().parse::<i32>().unwrap())
    .collect();

- Reads the first line of input (Alice's scores):
  - stdin_iterator.next(): Retrieves the next line of input.
  - .unwrap(): Panics if no line is available or an error occurs.
  - .trim_end(): Removes trailing whitespace or newline characters from the line.
  - .split(' '): Splits the line into substrings using spaces as the delimiter.
  - .map(|s| s.to_string().parse::<i32>().unwrap()):
    - Converts each substring into a String and parses it into an integer (i32).
    - Panics if parsing fails.
  - .collect(): Collects the parsed integers into a vector (Vec<i32>).
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
  - write!(&mut fptr, "{}"): Writes the current score to the file.
  - If it is not the last score, a space is appended after it.
- writeln!(&mut fptr):
  - Writes a newline to the file after the scores.

How the Code Works Overall
1. Reads two lines of input:
   - First line: Alice's scores (a).
   - Second line: Bob's scores (b).
2. Parses the input into vectors a and b.
3. Compares the scores using compareTriplets:
   - Iterates over corresponding elements in a and b.
   - Updates scores for Alice and Bob based on the comparisons.
4. Writes the results (Alice's and Bob's scores) to the file specified by OUTPUT_PATH.

Example Input and Output

Input:

5 6 7

3 6 10

Execution Steps:

1. Parse a = [5, 6, 7] and b = [3, 6, 10].
2. Compare:
   - First category: 5 > 3, Alice gets 1 point.
   - Second category: 6 == 6, no points.
   - Third category: 7 < 10, Bob gets 1 point.
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
1. ar.iter():
   - Creates an iterator over the elements of the array ar.
2. .sum():
   - Computes the sum of all elements in the iterator and returns the result.
3. Return Value:
   - The total sum of the array elements as an i64 integer.

The main Function

1. Standard Input Setup
   
let stdin = io::stdin();

let mut stdin_iterator = stdin.lock().lines();

- io::stdin():
  - Captures standard input.
- stdin.lock().lines():
  - Locks the standard input and enables reading it line by line. Returns an iterator where each line is a Result<String>.

2. Creating an Output File
   
let mut fptr = File::create(env::var("OUTPUT_PATH").unwrap()).unwrap();

- env::var("OUTPUT_PATH"):
  - Retrieves the value of the OUTPUT_PATH environment variable, which specifies the path of the output file.
  - .unwrap():
  - Panics if the environment variable is not set or invalid.
- File::create(...):
  - Creates a new file at the specified path. Overwrites the file if it already exists.
  - .unwrap():
    - Panics if the file cannot be created.

3. Reading the Number of Elements
   
let _ar_count = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();

- stdin_iterator.next():
  - Reads the next line from the input iterator.
- .unwrap().unwrap():
  - The first .unwrap() extracts the Result, and the second .unwrap() extracts the Option value.
  - Panics if no line is available or an error occurs.
- .trim():
  - Removes leading and trailing whitespace or newline characters.
- .parse::<i32>():
  - Converts the trimmed string into a 32-bit integer.
  - Panics if parsing fails.
- _ar_count:
  - Holds the number of elements in the array (but is not used in this program).

4. Parsing the Array of Numbers
   
let ar: Vec<i64> = stdin_iterator.next().unwrap().unwrap()

    .trim_end()
    .split(' ')
    .map(|s| s.to_string().parse::<i64>().unwrap())
    .collect();

- Reads the second line of input, which contains space-separated integers.
- .trim_end():
  - Removes trailing whitespace or newline characters from the line.
- .split(' '):
  - Splits the string into substrings using spaces as the delimiter.
- .map(|s| s.to_string().parse::<i64>().unwrap()):
  - For each substring:
    - Converts it into a String.
    - Parses it as a 64-bit integer (i64).
    - Panics if parsing fails.
- .collect():
  - Collects the parsed integers into a vector (Vec<i64>).

5. Calling aVeryBigSum
   
let result = aVeryBigSum(&ar);
- Passes the reference of the vector ar to the aVeryBigSum function.
- Stores the result (the sum of the array elements) in the variable result.

6. Writing the Output
   
writeln!(&mut fptr, "{}", result).ok();
- writeln!:
  - Writes the value of result to the output file, followed by a newline.
- &mut fptr:
  - Specifies the output file as the target.
- .ok():
  - Silently ignores any errors while writing to the file.

How the Code Works Overall
1. Reads two lines of input:
   - First line: The number of elements in the array (not used in the program).
   - Second line: Space-separated integers to be summed.
2. Parses the integers into a vector ar of type i64.
3. Passes the vector to aVeryBigSum to compute the sum.
4. Writes the result (the sum) to a file specified by the OUTPUT_PATH environment variable.

Example Input and Output

Input:

5

1000000001 1000000002 1000000003 1000000004 1000000005

Execution Steps:

1. Parse _ar_count = 5 (not used).
2. Parse ar = [1000000001, 1000000002, 1000000003, 1000000004, 1000000005].
3. Compute result = 1000000001 + 1000000002 + 1000000003 + 1000000004 + 1000000005 = 5000000015.

Output (written to the file):

5000000015

# Diagonal difference (easy)
The diagonalDifference Function

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
   - let n = arr.len();
   - Calculates the size of the matrix (number of rows or columns, since it's a square matrix).

2. Initialize Diagonal Sums:
   - let mut primary_diagonal_sum = 0;
   - let mut secondary_diagonal_sum = 0;
   - These variables will store the sum of the primary and secondary diagonals, respectively.

3. Iterate Through the Matrix:
   
for i in 0..n {

    primary_diagonal_sum += arr[i][i];            // Primary diagonal
    secondary_diagonal_sum += arr[i][n - i - 1]; // Secondary diagonal
}

- The for loop iterates over each row index i.
- Primary Diagonal (arr[i][i]):
  - Adds the element at row i and column i to primary_diagonal_sum.
- Secondary Diagonal (arr[i][n - i - 1]):
  - Adds the element at row i and column (n - i - 1) to secondary_diagonal_sum.
  - This calculates the reverse diagonal.

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
  - Converts the string to a 32-bit integer.

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
     - Prepares memory for each row.
  2. stdin_iterator.next():
     - Reads the next line of input.
  3. trim_end():
     - Removes trailing whitespace or newline characters.
  4. split(' '):
     - Splits the line into space-separated numbers.
  5. .map(|s| s.to_string().parse::<i32>().unwrap()):
     - Converts each substring into a 32-bit integer (i32).
  6. .collect():
     Collects the parsed integers into a vector, representing a row of the matrix.
  7. arr[i]:
     - Assigns the row vector to the ith position in the matrix.

6. Compute the Result
   
let result = diagonalDifference(&arr);
- Calls the diagonalDifference function with a reference to the matrix arr.
- Stores the computed difference in result.

7. Write the Result to the File
   
writeln!(&mut fptr, "{}", result).ok();
- Writes the result to the output file specified by fptr.

How the Code Works Overall
1. Reads:
   - The size of the square matrix n.
   - The matrix elements (space-separated integers for each row).
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

# Plus Minnus (easy)
The plusMinus Function

fn plusMinus(arr: &[i32]) {

    let n = arr.len() as f64; // Total number of elements
    let mut positive_count = 0;
    let mut negative_count = 0;
    let mut zero_count = 0;

    // Count positives, negatives, and zeros
    for &num in arr {
        if num > 0 {
            positive_count += 1;
        } else if num < 0 {
            negative_count += 1;
        } else {
            zero_count += 1;
        }
    }

    // Print the results with 6 decimal places
    println!("{:.6}", positive_count as f64 / n);
    println!("{:.6}", negative_count as f64 / n);
    println!("{:.6}", zero_count as f64 / n);
}

Purpose

- The function calculates and prints the proportion of positive, negative, and zero elements in an array of integers. Each proportion is printed to six decimal places.

Steps
1. Find the Size of the Array (n):

let n = arr.len() as f64;
- The size of the array is stored as a f64 (floating-point number) to perform accurate division later.

2. Initialize Counters:

let mut positive_count = 0;

let mut negative_count = 0;

let mut zero_count = 0;

- positive_count: Counts the number of positive elements.
- negative_count: Counts the number of negative elements.
- zero_count: Counts the number of zeros.

3. Iterate Over the Array:

for &num in arr {

    if num > 0 {
        positive_count += 1;
    } else if num < 0 {
        negative_count += 1;
    } else {
        zero_count += 1;
    }
}

- Loop through each number in the array:
  - If the number is positive, increment positive_count.
  - If the number is negative, increment negative_count.
  - Otherwise, increment zero_count.

4. Calculate and Print Proportions:

println!("{:.6}", positive_count as f64 / n);

println!("{:.6}", negative_count as f64 / n);

println!("{:.6}", zero_count as f64 / n);

- Each count is divided by the total number of elements (n) to calculate the proportion.
- The result is formatted to six decimal places using "{:.6}".

The main Function
1. Input Setup

let stdin = io::stdin();

let mut stdin_iterator = stdin.lock().lines();
- Standard input is prepared to read lines of input.
  
2. Read the Size of the Array (n)

let n = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();
- Reads the first line of input, which contains the size of the array (n).
  
3. Read the Array (arr)

let arr: Vec<i32> = stdin_iterator.next().unwrap().unwrap()

    .trim_end()
    .split(' ')
    .map(|s| s.to_string().parse::<i32>().unwrap())
    .collect();
- Reads the second line of input, which contains the elements of the array, separated by spaces.
  
- Steps:
  1. .trim_end() removes trailing whitespace.
  2. .split(' ') splits the string into substrings based on spaces.
  3. .map(|s| s.to_string().parse::<i32>().unwrap()) converts each substring into an integer.
  4. .collect() collects all integers into a Vec<i32>.
     
4. Call the Function

plusMinus(&arr);
- Passes the array arr as a reference to the plusMinus function to calculate and print the proportions.
- 
How the Code Works Overall
1. Reads:
   - The size of the array (n).
   - The array elements.
2. Calculates the proportions of positive, negative, and zero elements in the array.
3. Prints the proportions to six decimal places.
   
Example Input and Output

Input:

6

-4 3 -9 0 4 1

Execution Steps:

1. Parse the array:
   
arr = [-4, 3, -9, 0, 4, 1]

2. Calculate counts:
- positive_count = 3 (elements: 3, 4, 1)
- negative_count = 2 (elements: -4, -9)
- zero_count = 1 (element: 0)

3. Calculate proportions:
- positive_proportion = 3 / 6 = 0.500000
- negative_proportion = 2 / 6 = 0.333333
- zero_proportion = 1 / 6 = 0.166667
- 
Output:

0.500000

0.333333

0.166667

# Staircase (easy)
The staircase Function

fn staircase(n: i32) {

    for i in 1..=n {
        let spaces = (n - i) as usize; // Calculate spaces for current row
        let hashes = i as usize;      // Calculate hashes for current row
        println!("{}{}", " ".repeat(spaces), "#".repeat(hashes)); // Print spaces and hashes
    }
}

Purpose
- The function prints a staircase pattern of height n. Each step of the staircase consists of spaces followed by hashes (#), aligned to the right.
  
Steps
1. Iterate Over Rows (1..=n):

for i in 1..=n {
- The loop runs from 1 to n, where i represents the current row number.

2. Calculate the Number of Spaces (spaces):

let spaces = (n - i) as usize;

- For each row:
  - The number of spaces required is equal to the difference between n (total rows) and i (current row).
  - spaces is cast to usize because .repeat() requires it.

3. Calculate the Number of Hashes (hashes):

let hashes = i as usize;
- The number of hashes (#) increases as the row number increases, equal to the current row number (i).

4. Print the Row:

println!("{}{}", " ".repeat(spaces), "#".repeat(hashes));
- " ".repeat(spaces) generates a string of spaces.
- "#".repeat(hashes) generates a string of hashes.
- These two strings are concatenated and printed as a single line.
  
The main Function

fn main() {

    let stdin = io::stdin();
    let mut stdin_iterator = stdin.lock().lines();

    let n = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();

    staircase(n);
}

Steps in main:
1. Read Input:

let stdin = io::stdin();

let mut stdin_iterator = stdin.lock().lines();
- Standard input is set up for reading.

2. Parse the Input (n):

let n = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();
- Reads the first line of input and parses it into an integer (n), which represents the height of the staircase.

3. Call the Function:

staircase(n);
- Passes the value of n to the staircase function to generate and print the pattern.

How the Code Works
1. Reads an integer n (height of the staircase).
2. Prints a staircase pattern of height n, with:
   - The first row containing n-1 spaces followed by 1 hash (#).
   - The second row containing n-2 spaces followed by 2 hashes (##)
   - ...
   - The last row containing 0 spaces followed by n hashes.

Example Input and Output

Input:

6

Execution Steps:
1. For i = 1:
   - Spaces: 6 - 1 = 5 → " "
   - Hashes: 1 → "#"
   - Row: " #"
2. For i = 2:
   - Spaces: 6 - 2 = 4 → " "
   - Hashes: 2 → "##"
   - Row: " ##"
3. For i = 3:
   - Spaces: 6 - 3 = 3 → " "
   - Hashes: 3 → "###"
   - Row: " ###"
4. Continue this pattern for rows 4, 5, and 6.
   
Output:

     #
     
    ##
    
   ###
   
  ####
  
 #####
 
######

Edge Cases
1. n = 1:
   
#
- A staircase with just one step.

2. n = 0:

No output (an empty staircase).

# Mini Max Sum (easy)
The miniMaxSum Function

fn miniMaxSum(arr: &[i32]) {

    let total_sum: i64 = arr.iter().map(|&x| x as i64).sum(); // Convert to i64 and calculate total sum
    let min_value = *arr.iter().min().unwrap() as i64;        // Find the minimum value and cast to i64
    let max_value = *arr.iter().max().unwrap() as i64;        // Find the maximum value and cast to i64

    // Min sum excludes the max value; Max sum excludes the min value
    let min_sum = total_sum - max_value;
    let max_sum = total_sum - min_value;

    println!("{} {}", min_sum, max_sum);
}

Purpose
- This function calculates:
  - The minimum sum by excluding the largest element in the array.
  - The maximum sum by excluding the smallest element in the array.
  - It then prints both results in a single line, separated by a space.

Steps
1. Calculate the Total Sum (total_sum):

let total_sum: i64 = arr.iter().map(|&x| x as i64).sum();
- Iterate through all elements in the array (arr.iter()).
- Convert each element (x) to i64 using x as i64 to prevent overflow when adding large integers.
- Calculate the total sum of the array using .sum().

2. Find the Minimum and Maximum Values:

let min_value = *arr.iter().min().unwrap() as i64;

let max_value = *arr.iter().max().unwrap() as i64;
- Use .min() and .max() on the iterator to find the smallest and largest values in the array.
- The unwrap() ensures these operations return valid values (works because the array always has at least one element).
- Dereference the results with * and convert them to i64.

3. Calculate the Minimum and Maximum Sums:

let min_sum = total_sum - max_value;

let max_sum = total_sum - min_value;
- The minimum sum excludes the largest element (max_value).
- The maximum sum excludes the smallest element (min_value).

4.Print the Results:

println!("{} {}", min_sum, max_sum);
- Outputs the results in a single line, separated by a space.
  
The main Function

fn main() {

    let stdin = io::stdin();
    let mut stdin_iterator = stdin.lock().lines();

    let arr: Vec<i32> = stdin_iterator.next().unwrap().unwrap()
        .trim_end()
        .split(' ')
        .map(|s| s.to_string().parse::<i32>().unwrap())
        .collect();

    miniMaxSum(&arr);
}

Steps in main:

1. Read Input:

let stdin = io::stdin();

let mut stdin_iterator = stdin.lock().lines();
- Standard input is prepared for reading.
- stdin_iterator is used to read multiple lines.

2. Parse the Input Array (arr):

let arr: Vec<i32> = stdin_iterator.next().unwrap().unwrap()

    .trim_end()
    .split(' ')
    .map(|s| s.to_string().parse::<i32>().unwrap())
    .collect();
- Read the first line of input (stdin_iterator.next()).
- Trim any trailing spaces using .trim_end().
- Split the string into individual numbers using .split(' ').
- Parse each number into an i32 and collect them into a vector (Vec<i32>).

3. Call the Function:

miniMaxSum(&arr);
- Pass the array (arr) to the miniMaxSum function.
- 
How the Code Works

Given an array of 5 integers, it calculates:
1. The minimum sum by excluding the largest number.
2. The maximum sum by excluding the smallest number.
3. Outputs the two results on a single line.

Example Input and Output

Input:

1 2 3 4 5

Execution Steps:

Calculate the Total Sum:

1 + 2 + 3 + 4 + 5 = 15

Find the Minimum and Maximum Values:

Minimum value: 1

Maximum value: 5

Calculate the Sums:

Minimum Sum: 15 - 5 = 10 (Excludes the maximum value 5).

Maximum Sum: 15 - 1 = 14 (Excludes the minimum value 1).

Output the Results:

10 14

Edge Cases

All Elements Are the Same:

Input: 3 3 3 3 3

Output: 12 12 (Since the minimum and maximum values are the same).

Array Contains Negative Numbers:

Input: -1 -2 -3 -4 -5

Output: -14 -10

Array of Size Larger Than 5:

The logic is not restricted to arrays of size 5. It works for any non-empty array.

# Birthday cake candles (easy)
The birthdayCakeCandles Function

fn birthdayCakeCandles(candles: &[i32]) -> i32 {

    // Find the maximum height among the candles
    let max_height = *candles.iter().max().unwrap();
    
    // Count how many candles have this maximum height
    candles.iter().filter(|&&height| height == max_height).count() as i32
}

Purpose
- This function determines how many candles on a birthday cake are the tallest, as only the tallest candles can be blown out.

Steps
1. Find the Maximum Height:

let max_height = *candles.iter().max().unwrap();
- Use the .iter() method to iterate over the elements of the candles array.
- Call .max() to find the maximum value in the array.
- The unwrap() ensures that the operation succeeds (assuming the array is not empty).
- Use * to dereference the value returned by .max().

2.Count the Candles with Maximum Height:

candles.iter().filter(|&&height| height == max_height).count() as i32
- Use .filter() to keep only the candles whose height equals max_height.
- Use &&height to dereference the value being checked in the filter condition.
- Call .count() to get the total number of candles with the maximum height.
- Convert the result to an i32 using as i32.

The main Function

fn main() {

    let stdin = io::stdin();
    let mut stdin_iterator = stdin.lock().lines();

    let mut fptr = File::create(env::var("OUTPUT_PATH").unwrap()).unwrap();

    let _candles_count = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();

    let candles: Vec<i32> = stdin_iterator.next().unwrap().unwrap()
        .trim_end()
        .split(' ')
        .map(|s| s.to_string().parse::<i32>().unwrap())
        .collect();

    let result = birthdayCakeCandles(&candles);

    writeln!(&mut fptr, "{}", result).ok();
}

Steps in main
1. Prepare Input:

let stdin = io::stdin();

let mut stdin_iterator = stdin.lock().lines();
- Initialize a reader for standard input.
- Use stdin_iterator to read multiple lines.

2. Parse the Number of Candles:

let _candles_count = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();
- Read the first line of input, which specifies the number of candles.
- Use .trim() to remove any extra whitespace and .parse::<i32>() to convert it to an integer.

3. Parse the Candle Heights:

let candles: Vec<i32> = stdin_iterator.next().unwrap().unwrap()

    .trim_end()
    .split(' ')
    .map(|s| s.to_string().parse::<i32>().unwrap())
    .collect();
- Read the second line of input, which contains the heights of the candles.
- Use .split(' ') to break the string into individual heights.
- Convert each height to an i32 and collect the results into a vector.

4. Call the Function:

let result = birthdayCakeCandles(&candles);
- Pass the vector of candle heights (candles) to the birthdayCakeCandles function.

5. Write the Result:

writeln!(&mut fptr, "{}", result).ok();
- Write the result (number of tallest candles) to the output file specified by the OUTPUT_PATH environment variable.

Example Input and Output

Input:

4

3 2 1 3

Execution Steps:
1. Parse the number of candles: 4.
2. Parse the candle heights: [3, 2, 1, 3].
3. Find the maximum height: 3.
4. Count the candles with height 3: 2.

Output:

2

Edge Cases

All Candles Are the Same Height:

Input: 5 5 5 5

Output: 4 (All candles are the tallest).

Only One Candle:

Input: 1

Output: 1.

Array with Negative Heights:

Input: -1 -2 -3 -1

Output: 2 (Tallest candles are -1).

# Time conversion (easy)
The timeConversion Function

fn timeConversion(s: &str) -> String {

    let mut hours = s[0..2].parse::<i32>().unwrap(); // Extract hours
    let minutes_seconds = &s[2..8]; // Extract minutes and seconds
    let period = &s[8..]; // Extract AM or PM

    if period == "AM" {
        if hours == 12 {
            hours = 0; // Convert midnight to 00
        }
    } else { // PM case
        if hours != 12 {
            hours += 12; // Convert PM hours to 24-hour format
        }
    }

    format!("{:02}{}", hours, minutes_seconds) // Return the formatted time
}

Purpose
- The function converts a 12-hour clock format time string (e.g., 07:05:45PM) to a 24-hour clock format (e.g., 19:05:45).

Steps
1. Extract Hours:

let mut hours = s[0..2].parse::<i32>().unwrap();
- Extract the first two characters of the string (s[0..2]), which represent the hour part.
- Parse them into an integer (i32) using .parse::<i32>().

2. Extract Minutes and Seconds:

let minutes_seconds = &s[2..8];
- Extract the portion of the string from index 2 to 8 (s[2..8]), which includes the :MM:SS part.

3. Extract the Period (AM/PM):

let period = &s[8..];
- Extract the last two characters of the string (s[8..]), which represent either "AM" or "PM".

4. Handle the AM/PM Conversion:
- If the time is in AM:

if period == "AM" {

    if hours == 12 {
        hours = 0; // Convert midnight (12 AM) to 00
    }
}
  - If the time is 12:XX:XXAM, set the hour to 0 (midnight in 24-hour format).
  - Otherwise, leave the hour unchanged.

- If the time is in PM:

else {

    if hours != 12 {
        hours += 12; // Convert PM hours (other than 12 PM) to 24-hour format
    }
}

  - If the time is not 12:XX:XXPM, add 12 to convert it to 24-hour format.
  - Otherwise, leave the hour unchanged (since 12:XX:XXPM remains 12 in 24-hour format).

- Format the Result:

format!("{:02}{}", hours, minutes_seconds)
- Use format!() to create the output string.
- Use {:02} to ensure the hour is always two digits (e.g., 00, 01, ..., 23).
- Append the minutes and seconds.

The main Function

fn main() {

    let stdin = io::stdin();
    let mut stdin_iterator = stdin.lock().lines();

    let mut fptr = File::create(env::var("OUTPUT_PATH").unwrap()).unwrap();

    let s = stdin_iterator.next().unwrap().unwrap();

    let result = timeConversion(&s);

    writeln!(&mut fptr, "{}", result).ok();
}

Steps in main
1. Prepare Input:

let stdin = io::stdin();

let mut stdin_iterator = stdin.lock().lines();
- Initialize a reader for standard input.
- Use stdin_iterator to read multiple lines.

2. Read the Input Time:

let s = stdin_iterator.next().unwrap().unwrap();
- Read the input time string (e.g., 07:05:45PM).

3. Call the Function:

let result = timeConversion(&s);
- Pass the input time string (s) to the timeConversion function.

4. Write the Result:

writeln!(&mut fptr, "{}", result).ok();
- Write the converted time to the output file specified by the OUTPUT_PATH environment variable.

Example Input and Output

Input:

07:05:45PM

Execution Steps:
1. Extract hours: 07.
2. Extract minutes and seconds: :05:45.
3. Extract period: PM.
4. Convert:
   - Since the period is "PM" and 07 != 12, add 12 to hours: 07 + 12 = 19.

Output:

19:05:45

Input:

12:00:00AM

Execution Steps:
1. Extract hours: 12.
2. Extract minutes and seconds: :00:00.
3. Extract period: AM.
4. Convert:
   - Since the period is "AM" and 12 == 12, set hours to 0.

Output:

00:00:00

Edge Cases
1. No Conversion Needed for Noon:
   - Input: 12:45:54PM.
   - Output: 12:45:54.

2. Midnight:
   - Input: 12:00:00AM.
   - Output: 00:00:00.

3. Single-Digit Hour in AM/PM:
   - Input: 01:00:00PM.
   - Output: 13:00:00.
  
# Grading Students (easy)
The gradingStudents Function

fn gradingStudents(grades: &[i32]) -> Vec<i32> 

    grades
        .iter()
        .map(|&grade| {
            if grade < 38 {
                grade
            } else {
                let next_multiple_of_5 = ((grade / 5) + 1) * 5;
                if next_multiple_of_5 - grade < 3 {
                    next_multiple_of_5
                } else {
                    grade
                }
            }
        })
        .collect()
}

Function Purpose

The function adjusts students' grades based on the following rules:
1. Grades less than 38 are not rounded since they cannot be converted to passing grades.
2. Grades are rounded up to the nearest multiple of 5 if the difference between the grade and the next multiple of 5 is less than 3.
3. Grades that do not meet the above criteria remain unchanged.

Steps
1. Iterate Over the Grades:
   - Use .iter() to create an iterator over the input grades array.

2. Apply the Rounding Rules:
   - For each grade, check if it is less than 38:

if grade < 38 {

    grade
}

     - Grades below 38 remain unchanged.
     
   - Otherwise, calculate the next multiple of 5:

let next_multiple_of_5 = ((grade / 5) + 1) * 5;

     - Divide the grade by 5, add 1 to move to the next multiple, and multiply by 5 to find the next multiple.
     
   - Check if the difference between the grade and the next multiple is less than 3:

if next_multiple_of_5 - grade < 3 {

    next_multiple_of_5
} else {
    grade
}

     - If the difference is less than 3, round the grade up to the next multiple of 5.
     
     - Otherwise, leave the grade unchanged.

3. Return the Adjusted Grades:
- Use .collect() to gather the adjusted grades into a Vec<i32>.

The main Function

fn main() {

    let stdin = io::stdin();
    let mut stdin_iterator = stdin.lock().lines();

    let mut fptr = File::create(env::var("OUTPUT_PATH").unwrap()).unwrap();

    let grades_count = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();

    let mut grades: Vec<i32> = Vec::with_capacity(grades_count as usize);

    for _ in 0..grades_count {
        let grades_item = stdin_iterator.next().unwrap().unwrap().trim().parse::<i32>().unwrap();
        grades.push(grades_item);
    }

    let result = gradingStudents(&grades);

    for i in 0..result.len() {
        write!(&mut fptr, "{}", result[i]).ok();

        if i != result.len() - 1 {
            writeln!(&mut fptr).ok();
        }
    }

    writeln!(&mut fptr).ok();
}

Steps in main
1. Input Handling:
   - Use stdin to read input from the console.
   - Parse the number of grades (grades_count).
2. Collect Grades:
   - Read each grade and store it in a Vec<i32>.
3. Call the Function:
   - Pass the grades to the gradingStudents function to calculate the adjusted grades.
4. Write the Output:
   - Write each grade to the output file specified by the OUTPUT_PATH environment variable.

Example Input and Output

Input:

4

73

67

38

33

Execution Steps:
1. Input Grades: [73, 67, 38, 33].
2. Rounding Rules:
   - Grade 73:
     - Next multiple of 5: 75.
     - Difference: 2 (< 3).
     - Adjusted grade: 75.
   - Grade 67:
     - Next multiple of 5: 70.
     - Difference: 3 (not < 3).
     - Adjusted grade: 67.
   - Grade 38:
     - Next multiple of 5: 40.
     - Difference: 2 (< 3).
     - Adjusted grade: 40.
   - Grade 33:
     - Less than 38.
     - Remains unchanged: 33.

Output Grades: [75, 67, 40, 33].

Output:

75

67

40

33

Edge Cases
1. Grades Exactly on a Multiple of 5:
   - Input: [75, 80, 90].
   - Output: [75, 80, 90] (no rounding needed).
2. Grades Just Below Passing Threshold:
   - Input: [37, 36].
   - Output: [37, 36] (no rounding since they are below 38).
3. Grades Close to the Next Multiple:
   - Input: [39, 73, 78].
   - Output: [40, 75, 80].

# Queen's attack II (medium)
