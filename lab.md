# Buggy Program
`static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
`
> A failure-inducing input for the buggy program, as a JUnit test
`@Test 
	public void testReverseInPlace() {
    int[] input1 = {1,2, 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3,2,1 }, input1);
	}
`
> An input that doesn't induce a failure
`@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
`
> The symptom, as the output of running the tests
