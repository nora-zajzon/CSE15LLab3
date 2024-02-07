## Part 1 - Bugs

```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

**A failure-inducing input for the buggy program, as a JUnit test**

```
@Test 
	public void testReverseInPlace() {
    int[] input1 = {1,2, 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3,2,1 }, input1);
	}
```

**An input that doesn't induce a failure**

```
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```

**The symptom, as the output of running the tests**

# Failed Test
![Image](FailInput.png)
![Image](FailInput1.png)
# Passed Test
![Image](PassInput.png)

# Bug Code Before and After
**Before**
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
**After**
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```
The issue with the Before code is that it attempts to reverse the array in place by changing elements with their corresponding elements from 
the end of the array. However, this overwrites the original values before they are stored. The After code fixes this issue by iterating only 
up to half of the array length and using a temporary variable `temp` to store the original value before it is swapped. Therefore, each 
element is swapped with its corresponding element from the end of the array without overwriting the original values prematurely.

## Part 2 - Researching Commands

Case-Insensitive Search:

1. Option: -i or --ignore-case
Example: grep -i "pattern" filename
Explanation: This option makes the search case-insensitive, allowing you to find matches regardless of whether the characters are uppercase or lowercase.
Counting the Number of Matches:
2. Option: -c or --count
Example: grep -c "pattern" filename
Explanation: This option counts and displays the number of lines that match the specified pattern in the given file(s) rather than displaying the actual matching lines.
Displaying Line Numbers with Matches:
3. Option: -n or --line-number
Example: grep -n "pattern" filename
Explanation: This option shows the line numbers along with the matching lines, making it useful to quickly locate where the pattern occurs within the file.
Recursive Search in Directories:
4. Option: -r or -R or --recursive
Example: grep -r "pattern" directory
Explanation: With this option, grep searches for the specified pattern recursively in all files within the specified directory and its subdirectories. Useful for searching through entire directory structures.
These options enhance the flexibility and functionality of the grep command, making it a powerful tool for text searching and pattern matching in the command line.
