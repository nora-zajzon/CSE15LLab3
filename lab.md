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
<br> Output: 
<br> `ATPases [ 1 ] . Three isoforms that differ in the ratio of
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
<br> Output
<br> `./1471-2202-4-3.txt:          of the precursor [see [ 31 ] ]. Another possibility could
`<br>`./1471-2202-4-3.txt:          somatostatin have been observed [ 33 34 ] . This
`<br>`./1471-2202-4-3.txt:          indicated [ 15 ] . Finally, we hope that our study will
`<br>`./1471-2202-4-3.txt:          disease [ 8 ] .
`<br>`./1471-2202-4-3.txt:          human brain of Haines [ 36 ] , and the same atlas was
`<br>`./1471-2202-4-3.txt:          addition, the atlas of Paxinos et al. [ 37 ] was
`<br>`./1471-2202-4-3.txt:          series of densities [ 38 ]` . . . 
<br> This command line option allows the grep to interpret patterns as extended regular expressions within the working directory. (Output was shortened)


2. **Counting the Number of Matches:**
<br> Option: ` -c` or `--count`
<br>Command Line for text file: `norazajzon@Noras-MacBook-Air-2 biomed % grep -c -E '\[ [0-9 ]+ \]' 1471-2091-2-9.txt`
<br> Output: `35`
<br>Explanation: Rather of displaying the actual matching lines, this option counts and shows the number of lines that match the specified 
pattern in the provided file.
<br>Command Line for text file: `norazajzon@Noras-MacBook-Air-2 biomed % grep -c -E '\[ [0-9 ]+ \]' --directories=recurse`
<br> Output:
<br>`./1472-6807-2-2.txt:30
`<br>`./1471-2350-4-3.txt:29
`<br>`./1471-2156-2-3.txt:0
`<br>`./1471-2156-3-11.txt:16
`<br>`./1471-2121-3-10.txt:48
`<br>`./1471-2172-3-4.txt:31
`<br>`./gb-2002-4-1-r2.txt:0
`<br>`./gb-2003-4-6-r41.txt:20
`<br>`./1471-2466-1-1.txt:29` . . .
<br>Explanation: Rather of displaying the actual matching lines, this option counts and shows the number of lines that match the specified 
pattern in each text file in the working directoy. (Output was shortened)

4. **Displaying Line Numbers with Matches:**
<br> Option: ` -n` or `--line-number`
<br>Command Line for text file: `norazajzon@Noras-MacBook-Air-2 biomed % grep -n -E '\[ [0-9 ]+ \]' 1471-2091-2-9.txt`
<br> Output:
<br> `10:        ATPases [ 1 ] . Three isoforms that differ in the ratio of
`<br>`16:        secretion, regulation of hemostasis and ectokinases [ 1 ] .
`<br>`31:        [ 1 ] . The specific activities of NTPDases vary over a
`<br>`34:        [ 9 10 ] . Sequence comparisons indicate that most of
`<br>`36:        conserved region, ACR1 - ACR5 [ 9 11 ] . However, the
`<br>`39:        respectively [ 9 ] .
`<br>`45:        catalytic function [ 12 ] . Substitution of H59 in ACR1
`<br>`47:        dependent manner [ 13 ] . Mutation of W187A in ACR3
`<br>`50:        ADPase activity [ 14 ] . Mutations of D62 and G64 of ACR1
`<br>`54:        superfamily [ 15 ] . These results suggest that the
`<br>`63:        carboxypeptidase [ 16 ] , S-adenosylmethionine synthetase [
`<br>`64:        17 18 ] , pyruvate kinase [ 19 20 ] , and F 
`<br>`65:        1 -ATPase [ 21 22 ] . This cation
`<br>`68:        cofactor [ 23 ] . Vanadyl has one axial and four equatorial
`<br>`75:        equatorial metal ligands [ 24 ] , binding of VO 2+to CD39
`<br>`80:        purified from insect cells [ 25 ] . Only one
`<br>`123:          the nature of VO 2+equatorial ligands [ 22 ] . Of the
`<br>`140:          || but not A⊥ [ 21 26 ] . In this
`<br>`152:          presence of metal [ 25 ] .
`<br>`251:        ligand [ 24 27 ] . By studying the EPR spectra of bound VO
`<br>`260:        decreased rate when VO 2+replaces Mg 2+ [ 21 ] .
`<br>`266:        only one nucleotide binding site [ 25 ] . The g and A
`<br>`273:        1 -ATPase [ 22 28 ] , the γ- and
`<br>`280:        1 -ATPase [ 21 ] , pyruvate kinase [ 19
`<br>`281:        20 ] , AdoMet synthetase [ 17 18 ] , and carboxypeptidase [
`<br>`290:        hydrolysis [ 25 ] , sCD39 probably has two conformations
`<br>`297:        protein [ 2 25 ] . The two EPR species observed with VO
`<br>`323:        that only ATP analogs were detected on sCD39 [ 25 ] .
`<br>`334:        groups [ 25 ] . When ADP is the substrate and generates
`<br>`394:          cultured as described by Chen and Guidotti [ 25 ] .
`<br>`395:          Soluble CD39 were purified as described [ 25 ] with some
`<br>`438:          according to Houseman et al. [ 21 ] . Dissolved molecular
`<br>`455:          accomplished with the computer program QPOWA [ 30 31 ]
`<br>`462:          constants obtained from model studies [ 24 32 ]
`<br>`473:          for equatorial donor group i [ 24 ] . Similar equations`
<br>Explanation: This option makes it easy to find the exact location of the pattern in the file by displaying the line numbers as a prefix and the matched lines.
<br>Command Line for directory: `norazajzon@Noras-MacBook-Air-2 biomed % grep -n -E '\[ [0-9 ]+ \]' --directories=recurse`
<br> Output:
<br>`./1471-2202-4-3.txt:328:          of the precursor [see [ 31 ] ]. Another possibility could
`<br>`./1471-2202-4-3.txt:338:          [ 22 32 ] , in which we did not find NK-ir perikarya.
`<br>`./1471-2202-4-3.txt:361:          somatostatin have been observed [ 33 34 ] . This
`<br>`./1471-2202-4-3.txt:365:          indicated [ 15 ] . Finally, we hope that our study will
`<br>`./1471-2202-4-3.txt:372:          disease [ 8 ] .
`<br>`./1471-2202-4-3.txt:460:          human brain of Haines [ 36 ] , and the same atlas was
`<br>`./1471-2202-4-3.txt:462:          addition, the atlas of Paxinos et al. [ 37 ] was
`<br>`./1471-2202-4-3.txt:475:          series of densities [ 38 ] .` . . .
<br>Explanation: This option makes it easy to find the exact location of the pattern in the files in the working directory by displaying the line numbers as a prefix and the matched lines. (Output was shortened)

7. **Recursive Search in Directories:**
<br>Option: `-m NUM` or `--max-count=NUM`
<br>Command Line for text file: `norazajzon@Noras-MacBook-Air-2 biomed % grep -m 3 -E '\[ [0-9 ]+ \]' 1471-2091-2-9.txt`
<br> Output:
<br>`ATPases [ 1 ] . Three isoforms that differ in the ratio of
        secretion, regulation of hemostasis and ectokinases [ 1 ] .
        [ 1 ] . The specific activities of NTPDases vary over a`
<br>Explanation: This option in the grep command is used to limit the number of matches returned by grep. It specifies the maximum number of matching lines to be displayed in the specified text file.
<br>Command Line for directory: `norazajzon@Noras-MacBook-Air-2 biomed % grep -m 3 -E '\[ [0-9 ]+ \]' 1471-2091-2-9.txt`
<br> Output:
<br>`./1471-213X-2-8.txt:          cells [ 7 ] . These cells express several members of the
`<br>`./1472-6793-1-12.txt:        cross-bridge cycling and 20% to calcium cycling [ 2 ] .
`<br>`./1472-6793-1-12.txt:        myocytes [ 3 4 ] , examining the energetic effects of
`<br>`./1472-6793-1-12.txt:        Consistent with this Brandes et al [ 5 ] have studied the
`<br>`./1471-2199-4-4.txt:        [ 1 ] , interleukin-12 [ 2 ] , and human endostatin [ 3 ] .
`<br>`./1471-2199-4-4.txt:        [ 4 5 ] . However, the kinetics of the vector encoded
`<br>`./1471-2199-4-4.txt:        transaminase levels [ 6 ] - a marker of hepatolysis -
`<br>`./1471-2199-4-5.txt:        several organisms - in bacteria [ 1 2 ] , yeast [ 3 ] and
`<br>`./1471-2199-4-5.txt:        chicken cells [ 4 ] .
`<br>`./1471-2199-4-5.txt:        altered replication (for review, see [ 5 ] ). DNA ds breaks
`<br>`./1471-2369-3-1.txt:        most common cause of end-stage renal disease [ 2 ] ,
`<br>`./1471-2369-3-1.txt:        high-salt diet [ 5 ] . The pathology is identical to human
`<br>`./1471-2369-3-1.txt:        and associates [ 6 ] .
`<br>`./1471-2229-2-8.txt:        stands when compared to southern-selected cultivars [ 1 ] .
`<br>`./1471-2229-2-8.txt:        naturally in the autumn after planting [ 2 ] . It also may
`<br>`./1471-2229-2-8.txt:        at near freezing temperatures [ 3 ] . Kenefick and Swanson
`<br>`./1471-2474-4-8.txt:        daily to treat hyperlipidemia with few side effects [ 7 ] .
`<br>`./1471-2474-4-8.txt:        [ 8 ] . Data from the National Health and Nutrition
`<br>`./1471-2474-4-8.txt:        annually [ 9 ] .` . . .
<br>Explanation: This option in the grep command is used to limit the number of matches returned by grep. It specifies the maximum number of matching lines to be displayed in all files in the working directory.
