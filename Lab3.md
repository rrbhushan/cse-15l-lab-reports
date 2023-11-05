# Lab Report 3
### Part 1
For this section, I will be focusing on the Array methods bugs, which were in the methods `reversed` and `reversedInPlace` .

#### Failure-Inducing Input (as JUnit test):

Testing `reversed` with an array with multiple elements:
```java
@Test
public void testReversedMult() {
  int[] input1 = { 2 , 4 , 6};
  assertArrayEquals(new int[]{ 6 , 4 , 2 }, ArrayExamples.reversed(input1));
}
```
Testing `reversedInPlace` with an array with multiple elements:
```java
@Test 
public void testReverseInPlaceMult() {
  int[] input1 = { 3 , 5 , 1 , 7 , 9 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 9 , 7 , 1 , 5 , 3 }, input1);
}
```

#### Input that does not induce failure (as JUnit test):

Testing `reversed` with an array with zero elements:
```java
@Test
public void testReversed() {
  int[] input1 = { };
  assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
}
```
Testing `reversedInPlace` with an array with one element:
```java
@Test 
public void testReverseInPlace() {
  int[] input1 = { 3 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 3 }, input1);
}
```

#### Symptoms:

![Image](/lab3images/l3symp.png)

The reason for the number of tests displaying 5 is due to a fifth test which is not included here.

#### Bugs:

Bug for `reversed`, before on top and fix on bottom:
```java
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
}
```
```java
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    newArray[arr.length - i - 1] = arr[i];
  }
  return newArray;
}
```
Before, we had our original array being the only one updated, having all its elements replaced with 0s as `newArray` was initialized with all 0s. Because of that, the entire array elements were just turned to 0s, which is not what the `reversed` method should be doing. To fix this, I swapped the ordering of the fourth line so instead of `arr[i]` taking values from `newArray[arr.length - i - 1]`, it is now `newArray[arr.length - i - 1]` taking values from `arr[i]`. At the end, I returned `newArray` rather than `arr` so that I can output a reversed array, not the same array. 

Bug for `reversedInPlace`, before on top and fix on bottom:
```java
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```
```java
static void reverseInPlace(int[] arr) {
  int a = 0;
  for(int i = 0; i < (arr.length)/2; i += 1) {
    a = arr[i];
    arr[i] = arr[arr.length - i - 1];
    arr[arr.length - i - 1] = a;
  }
}
```
Before, the array would get reversed for the first half of elements, but for the latter it would just mirror the first half, which is not considered as reversing an array but rather mirroring it. To fix this, I initialized a new variable `a`, stored the value at index i into `a`, replaced the value at index i with the value with the ith position from the end of the array, then replacing the ith position from the end of the array's value with the value stored in the variable `a`. To make sure we do not end up with the same exact array, I made sure to have this process stopped at the midpoint, which is `(arr.length)/2` rather than just `arr.length`. This way, the values can properly swap without having duplicate values where it is not needed, and this will reverse the array without needing to create a new array to return.

***

### Part 2
For this section, I will be focusing on the command `find`.


