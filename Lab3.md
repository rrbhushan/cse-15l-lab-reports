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
For this section, I will be focusing on a few options for the command `grep`, showing a couple of examples of each. For each of these options, I referenced the following [link](https://man7.org/linux/man-pages/man1/grep.1.html), which details on many different options for `grep`.

#### Line number (-n):
```unix
[ronitbhushan@MacBook-Pro-24 docsearch %] grep "listened" ./technical/911report/preface.txt -n
91:            We have listened to scores of overwhelming personal tragedies and astounding acts of
```
```
[ronitbhushan@MacBook-Pro-24 docsearch %] grep "This" ./technical/911report/chapter-12.txt -n
9:                This shift has occurred with the full support of the Congress, both major political
19:            This pattern has occurred before in American history. The United States faces a
47:            This vagueness blurs the strategy. The catastrophic threat at this moment in history
111:                the Taliban and pursue al Qaeda. This work continues. But long-term success demands
145:                thus given the picture of an omnipotent, unslayable hydra of destruction. This image
169:                identify, disrupt, capture, or kill individual terrorists. This effort was going on
399:                This is an ambitious recommendation. It would mean a redoubled effort to
428:                they find in the field. This should include discretionary funds for expenditures by
456:                This ministry uses zakat and government funds to spread Wahhabi beliefs throughout
574:                to come. This American engagement is resented. Polls in 2002 found that among
627:                economic opportunity. This vision includes widespread political participation and
741:                    flexible contact group of leading coalition governments. This is a good place,
1065:                    questions and use their judgment. This is not an invitation to arbitrary
1220:                Transportation Security Act. This act created the Transportation Security
1302:                    continues. This screening function should be performed by the TSA, and it should
1349:                greater powers, and then the need for those powers recedes after the war ends. This
1351:                mindful of threats to vital personal and civil liberties. This balancing is no easy
1353:            This shift of power and authority to the government calls for an enhanced system of
1410:                of Homeland Security. This department now has the lead responsibility for problems
1500:                preparedness. This is entirely appropriate, for the private sector controls 85
```
Through this option, I see exactly which lines contain the word "This" and "listened" in the provided files, displaying all the lines containing the phrase provided. This can come handy later on if I am navigating through code to search for a particular variable being used without needing to manually check line by line for each usage.

#### Count (-c):
```
[ronitbhushan@MacBook-Pro-24 docsearch %] grep "listened" ./technical/911report/preface.txt -c
1
```
```
[ronitbhushan@MacBook-Pro-24 docsearch %] grep "This" ./technical/911report/chapter-12.txt -c 
20
```
With the count option, I found out how many entries of a specific phrase are there in the file provided, with the first example showing 1 match and the second showing 20 matches. This can be helpful in locating any redundancies within my programs, simplifying my code if it is too verbose/repetitive.

#### Ignore case (-i)
```
[ronitbhushan@MacBook-Pro-24 docsearch %] grep "This" ./technical/911report/chapter-12.txt -i
                our nation in this new era. The national debate continues. Countering terrorism has
                This shift has occurred with the full support of the Congress, both major political
            This pattern has occurred before in American history. The United States faces a
                destructive power in the largest cities of the United States. In this sense, 9/11
                regarded just as we regard terrorism against America "over here." In this same
            This vagueness blurs the strategy. The catastrophic threat at this moment in history
                themselves. The United States must support such developments. But this process is
                efforts should be directed at those individuals and organizations. Calling this
                the Taliban and pursue al Qaeda. This work continues. But long-term success demands
                thus given the picture of an omnipotent, unslayable hydra of destruction. This image
                identify, disrupt, capture, or kill individual terrorists. This effort was going on
            Every policy decision we make needs to be seen through this lens. If, for example,
                This is an ambitious recommendation. It would mean a redoubled effort to
                    this region-wisely, as the 9/11 story shows-and failed half-measures could be
                    adapt to current security challenges of the future. NATO must pass this test.
                    rampant crime and narcotics trafficking in this crossroads of Central Asia.
                they find in the field. This should include discretionary funds for expenditures by
                This ministry uses zakat and government funds to spread Wahhabi beliefs throughout
                Arabia. The Saudi government has difficulty acknowledging this. American military
                declared, "[i]f we do not declare a general mobilization-we will lose this war on
                to come. This American engagement is resented. Polls in 2002 found that among
                ascendancy. Only Muslims can do this.
                economic opportunity. This vision includes widespread political participation and
                    flexible contact group of leading coalition governments. This is a good place,
                in this area.
                this area, the CooperativeThreat Reduction Program (usually referred to as
                redoubled its international commitments to support this program, and we recommend
                part. The government should weigh the value of this investment against the
                Qaeda-perhaps drastically-but it is too soon to know if this reduction will last.
                    understand this phenomenon well. Other evidence we obtained confirmed the
                    questions and use their judgment. This is not an invitation to arbitrary
                "visa waiver" countries will be added to the program, beginning this year, covered
                this timetable may be too slow, given the possible security dangers.
                To balance this measure, programs to speed known travelers should be a higher
                Transportation Security Act. This act created the Transportation Security
                planned to take over this function when it deploys a new screening system to take
                the place of CAPPS. The deployment of this system has been delayed because of claims
                    continues. This screening function should be performed by the TSA, and it should
                    implement this new system.
                industry will derive substantial benefits from this deployment, it should pay a fair
                greater powers, and then the need for those powers recedes after the war ends. This
                mindful of threats to vital personal and civil liberties. This balancing is no easy
            This shift of power and authority to the government calls for an enhanced system of
                this determination.
                Recommendation: At this time of increased and consolidated
                of Homeland Security. This department now has the lead responsibility for problems
                    merit additional support. Congress should not use this money as a pork
                protect the interests of their home states or districts. But this issue is too
                occurrence of this problem at three very different sites is strong evidence that
                preparedness. This is entirely appropriate, for the private sector controls 85
                was a principal contributing factor to this lack of preparedness.
```
```
[ronitbhushan@MacBook-Pro-24 docsearch %] grep -i "and" ./technical/government/Media/agency_expands.txt
Legal services agency expands
legal services to the poor, has expanded into the San Gabriel and
cultural isolation and service providers' lack of cultural
And with 13 percent to 15 percent of the Asian population in the
services and programs available to the poor," he said.
immigration, housing, public benefits and labor legal services to
"I remember the days when there were only a handful of people in
and English are interchangeable. Our goal is to have that for the
2002 to design and head the project.
"Now we have people speaking Cantonese, Mandarin, Thai, Khmer
(from Cambodia), Korean, Vietnamese, Japanese and Tagalog," Yee
Mak, a family law attorney who speaks Cantonese, Mandarin and
up in Hong Kong and Thailand before coming to the United States. "I
could use my language skills and wanted to give back to the Asian
NLS expanded when Legal Services Corp., the federal agency that
base from 16,000 to around 25,000, and NLS opened an office in El
```
This option makes it so I can find any key phrase in the provided file without bothering with case correctness, like in these examples where especially with chapter-12.txt, I was able to find a lot more matches. Through this, I don't have to worry about missing a particular method or variable mention by just including -i, making this option extremely useful for locating particular variables/method calls.

#### Invert match (-v):
```
[ronitbhushan@MacBook-Pro-24 docsearch %] grep -v "and" ./technical/government/Media/agency_expands.txt





By Matt Myerhoff
Published: Friday, July 19, 2002
PASADENA -- Neighborhood Legal Services, which provides free
Pomona valleys, areas with large Asian populations, many of whom
speak limited or no English.
Language is their biggest obstacle, but the Asian communities'
expertise also play a part, said NLS executive director Neal
Dubovitz.
And with 13 percent to 15 percent of the Asian population in the
U.S. living below the poverty line, NLS services are badly needed,
Dubovitz said.
"Although it is a significant part of the poverty population,
Asians historically have not been able to participate in the
From simple telephone advice to complete legal representation in
court, the agency provides free consumer, health, family,
people who earn under $1,380 per month.
Legal service providers have long served large Latino
populations, who have cultural diversity but share a common
language.
the legal offices who spoke Spanish," Dudovitz said. "Now Spanish
major Asian languages as well."
Before the expansion, only a few NLS lawyers spoke Asian
languages, said attorney Rebecca Yee, who was hired by NLS in April
said.
One of the 13 attorneys hired to work with the program is Irene
Thai.
Mak was a partner at a private law firm before she went to work
for NLS two years ago, earning up to $20,000 less a year working on
domestic violence cases.
"The job is more satisfying than the money," said Mak, who grew
community."
funds providers of free legal services nationwide, reduced the
number of grantees in the Los Angeles area from five to three,
Dudovitz said.
NLS won the competitive grant over the Legal Services Program
for Pasadena, San Gabriel-Pomona valleys. That boosted its client
Monte.




```
```
[ronitbhushan@MacBook-Pro-24 docsearch %] grep -v "the" ./technical/government/Media/5_Legal_Groups.txt 




Vulnerable
Salt Lake City Tribune

BY EDWARD MCDONOUGH
Five independent Salt Lake organizations that provide legal
Legal Center at 205 N. 400 West is a project of "And Justice for
All," which, until this venture, has been a joint fund-raising
services. "And Justice for All," which solicits donations primarily
service law groups.
parking, something that's hard to find downtown and which has been
agencies about $375,000 each year. My assistant, Charity
efficient for those needing legal services. No longer will a woman
desperate for a protective order, for example, have to run all over
brick and stone interior walls were all hidden behind coverings and
Sweet Candy Company building for Tomax. The Olafsons are delighted
cost received so far. There still needed to be furnishings and




```
In this case, the inverse selection is outputted (including new lines which is why there's a lot of spacing in between), which ignores lines that include the phrase specified in the given file (in short, none of the outputted lines include the given phrase). This can be useful for debugging in picking up on any non-method call lines, which gets outputted and can be cross checked to make sure the logic is correct if we already know the specified methods are correct.
