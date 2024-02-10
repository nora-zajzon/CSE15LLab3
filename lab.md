# Part 1 - Bugs

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

**Failed Test**
![Image](InputFail.png)
![Image](InputFail1.png)
**Passed Test**
![Image](InputPass.png)

## Bug Code Before and After
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

# Part 2 - Researching Commands

1. **Case-Insensitive Search:**  
Option: ` -E` or `--extended-regexp`
<br>Command Line with text file: `norazajzon@Noras-MacBook-Air-2 biomed % grep -E '\[ [0-9 ]+ \]' 1471-2091-2-9.txt`
<br> Output: ` ATPases [ 1 ] . Three isoforms that differ in the ratio of
        secretion, regulation of hemostasis and ectokinases [ 1 ] .
        [ 1 ] . The specific activities of NTPDases vary over a
        [ 9 10 ] . Sequence comparisons indicate that most of
        conserved region, ACR1 - ACR5 [ 9 11 ] . However, the
        respectively [ 9 ] .
        catalytic function [ 12 ] . Substitution of H59 in ACR1
        dependent manner [ 13 ] . Mutation of W187A in ACR3
        ADPase activity [ 14 ] . Mutations of D62 and G64 of ACR1
        superfamily [ 15 ] . These results suggest that the
        carboxypeptidase [ 16 ] , S-adenosylmethionine synthetase [
        17 18 ] , pyruvate kinase [ 19 20 ] , and F 
        1 -ATPase [ 21 22 ] . This cation
        cofactor [ 23 ] . Vanadyl has one axial and four equatorial
        equatorial metal ligands [ 24 ] , binding of VO 2+to CD39
        purified from insect cells [ 25 ] . Only one
          the nature of VO 2+equatorial ligands [ 22 ] . Of the
          || but not A⊥ [ 21 26 ] . In this
          presence of metal [ 25 ] .
        ligand [ 24 27 ] . By studying the EPR spectra of bound VO
        decreased rate when VO 2+replaces Mg 2+ [ 21 ] .
        only one nucleotide binding site [ 25 ] . The g and A
        1 -ATPase [ 22 28 ] , the γ- and
        1 -ATPase [ 21 ] , pyruvate kinase [ 19
        20 ] , AdoMet synthetase [ 17 18 ] , and carboxypeptidase [
        hydrolysis [ 25 ] , sCD39 probably has two conformations
        protein [ 2 25 ] . The two EPR species observed with VO
        that only ATP analogs were detected on sCD39 [ 25 ] .
        groups [ 25 ] . When ADP is the substrate and generates
          cultured as described by Chen and Guidotti [ 25 ] .
          Soluble CD39 were purified as described [ 25 ] with some
          according to Houseman et al. [ 21 ] . Dissolved molecular
          accomplished with the computer program QPOWA [ 30 31 ]
          constants obtained from model studies [ 24 32 ]
          for equatorial donor group i [ 24 ] . Similar equations`
<br> This command line option allows the grep to interpret patterns as extended regular expressions within the text file given.
<br> Command Line with working directory: `norazajzon@Noras-MacBook-Air-2 biomed % grep -E '\[ [0-9 ]+ \]' --directories=recurse`
<br> Output `./1471-2202-4-3.txt:          of the precursor [see [ 31 ] ]. Another possibility could
./1471-2202-4-3.txt:          [ 22 32 ] , in which we did not find NK-ir perikarya.
./1471-2202-4-3.txt:          somatostatin have been observed [ 33 34 ] . This
./1471-2202-4-3.txt:          indicated [ 15 ] . Finally, we hope that our study will
./1471-2202-4-3.txt:          disease [ 8 ] .
./1471-2202-4-3.txt:          human brain of Haines [ 36 ] , and the same atlas was
./1471-2202-4-3.txt:          addition, the atlas of Paxinos et al. [ 37 ] was
./1471-2202-4-3.txt:          series of densities [ 38 ] ......`
<br> This command line option allows the grep to interpret patterns as extended regular expressions within the working directory. (Output was shortened)


3. **Counting the Number of Matches:**
<br>Example: `grep -c "pattern" filename`
<br>Explanation: Rather of displaying the actual matching lines, this option counts and shows the number of lines that match the specified 
pattern in the provided file(s).

4. **Displaying Line Numbers with Matches:**
<br>Option: `-n` or `--line-number`
<br>Example: `grep -n "pattern" filename`
<br>Explanation: This option makes it easy to find the exact location of the pattern in the file by displaying the line numbers and the matched
lines.

5. **Recursive Search in Directories:**
<br>Option: `-r `or `-R` or `--recursive`
<br>Example: `grep -r "pattern" directory`
<br>Explanation: This option enables grep to do a recursive search for the given pattern across all files in the specified directory and all of its subdirectories. It is helpful for doing comprehensive directory structure searches.
