## Part 1 - Bugs

```java
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

**A failure-inducing input for the buggy program, as a JUnit test**

```java
@Test 
	public void testReverseInPlace() {
    int[] input1 = {1,2, 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3,2,1 }, input1);
	}
```

**An input that doesn't induce a failure**

```java
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
```java
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
**After**
```java
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

1. **Case-Insensitive Search:**  
<br>Option: `-i` or `--ignore-case`
<br>Example: `grep -i "pattern" filename`
<br>This option makes the search case-insensitive, allowing you to find matches regardless of uppercase or lowercase.

2. **Counting the Number of Matches:**
<br>Option: `-c` or `--count`
<br>Example: `grep -c "pattern" filename`
<br>Explanation: Rather of displaying the actual matching lines, this option counts and shows the number of lines that match the specified 
pattern in the provided file(s).

3. **Displaying Line Numbers with Matches:**
<br>Option: `-n` or `--line-number`
<br>Example: `grep -n "pattern" filename`
<br>Explanation: This option makes it easy to find the exact location of the pattern in the file by displaying the line numbers and the matched
lines.

4. **Recursive Search in Directories:**
<br>Option: `-r `or `-R` or `--recursive`
<br>Example: `grep -r "pattern" directory`
<br>Explanation: This option enables grep to do a recursive search for the given pattern across all files in the specified directory and all of
its subdirectories. It is helpful for doing comprehensive directory structure searches.
