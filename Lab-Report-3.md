## **PART 1 - BUGS**
The bug of question is within ArrayExamples, with the reverseInPlace method

1) A failure Inducing input:

```
int[] input2 = {3,2,1};
ArrayExamples.reverseInPlace(input2);
assertArrayEquals(new int[] {1,2,3}, input2 );

```

2) A non failure inducing input:

```
int[] input3 = {1,1,1};
ArrayExamples.reverseInPlace(input1);
assertArrayEquals(new int[] {1,1,1}, input3);

```  

3) Symptom from running tests:

```
1) testReverseInPlace(ArrayTests)
arrays first differed at element [2]; expected:<3> but was:<1>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReverseInPlace(ArrayTests.java:12)
        ... 32 trimmed
Caused by: java.lang.AssertionError: expected:<3> but was:<1>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 38 more
```

4) The Bug:
Before:

```
static void reverseInPlace(int[] arr) {
   for(int i = 0; i < arr.length; i += 1) {
     arr[i] = arr[arr.length - i - 1];
   }
 }

```

Explanation of Bug:
> The entierty of the bug is that while the for loop is running, it is updating the orginal array. For example,
> when the array {3, 2, 1} gets passed into this code, at index 0, arr[0] = arr[3-0-1], we set the 0 index of the
> array to the 2nd index of the array so now the array looks like {1,2,1}. Continuing on to index 1, arr[1] =
> arr[3-1-1], we set arr[1] to arr [1] so the array stays {1,2,1}, at the final index of the array is where the issue
> occurs since arr[2] = arr[3-2-1] so we set the last index of the array to the first index thus we have a final array
> of {1,2,1} instead of the desired {1,2,3}. Since the array {1,1,1} and {3} have either the same values or one value,
> this error wouldn't have been detected by them
After:

```
static void reverseInPlace(int[] arr) {
   int[] tempArr = new int[arr.length];
   for(int i = 0; i < arr.length; i += 1) {
     tempArr[i] = arr[arr.length - i - 1];
   }
   for (int i = 0; i <arr.length;i++){
     arr[i] = tempArr[i];
   }
 }

```

Explanation of Fix:
> Since the bug was caused by the array updating itself, the key to fixing it is to generate a temporary array and we loop
> through updating the temporary array instead. After, the orginal array gets set to the temporary array so that the orginal
> array gets updated without worry.
## **PART 2 - RESEARCHING COMMANDS**
The command being researched is the Grep command
[link](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)
1) The first command line option is: -h
"-h" Displays matched lines, but does not display the filenames

```
EXAMPLE 1:
[zroland@ieng6-202]:docsearch:279$ grep -h "crime" technical/911report/chapter-2.txt 
                the Americans to liberate the holy places "is considered a crime,"he said,"let
```

> grep -h "crime" returns the line(s) where the word crime appears in the given text file which in
> this case is only 1 line so one line is printed.

```
EXAMPLE 2:
[zroland@ieng6-202]:docsearch:280$ grep -h "holy" technical/911report/chapter-2.txt 
                the holy Qur'an and some of its interpreters. He appeals to people disoriented by
                what was seen as a "holy war"-jihad-against an invader. The largest numbers came
                world markets to buy arms and supplies for the mujahideen, or "holy warriors."
                conveyed the same message-the duty of Muslims to carry out holy war against the
                the Americans to liberate the holy places "is considered a crime,"he said,"let
```

> grep -h "holy" returns the lines(s) where the word holy appears in the given text file, which in
> this case is 5 lines. Notice that holy was in the line where we found crime in so that line was
> also returned subsequently

```
EXAMPLE 3:
zroland@ieng6-202]:docsearch:287$ grep -rh "holy" technical/911report/
                faith itself. Lives guided by religious faith, including literal beliefs in holy
                cyclical fund-raising process (with more money coming during the holy month of
                religion is denigrated. Our holy places desecrated. Our countries are occupied. Our
                the holy Qur'an and some of its interpreters. He appeals to people disoriented by
                what was seen as a "holy war"-jihad-against an invader. The largest numbers came
                world markets to buy arms and supplies for the mujahideen, or "holy warriors."
                conveyed the same message-the duty of Muslims to carry out holy war against the
                the Americans to liberate the holy places "is considered a crime,"he said,"let
                brochures in Arabic about jihad, held forth to friends on the subject of holy war,
                Jordan into Israel, and two Christian holy sites, at a time when all these locations
```

> grep -rh "holy" searches recursively in the technical/911report/ directory and lists all the lines
> in which "holy" appears within the textfiles that reside in that directory.

2) The second command line option is: -l
"-l" Displays list of a file names only

```
EXAMPLE 1:
[zroland@ieng6-202]:docsearch:284$ grep -l "holy" technical/911report/chapter-2.txt
technical/911report/chapter-2.txt
```

> grep -l text plus a file path returns the relative path to the file if the text exists within
> the file. In this case, holy does exist within chapter-2 as verified earlier so we see its
> relative path returned

```
EXAMPLE 2:
[zroland@ieng6-202]:docsearch:285$ grep -l "holy" technical/911report/chapter-1.txt 
```

> grep -l text plus a filereturns the relative path to the file if the text exists within
> the file. In this case the string "holy" not occur within chapter-1 so nothing is returned

```
EXAMPLE 3:
[zroland@ieng6-202]:docsearch:286$ grep -rl "holy" technical/911report/
technical/911report/chapter-12.txt
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-2.txt
technical/911report/chapter-5.txt
technical/911report/chapter-6.txt
```

> grep -rl text searches recursively in a given directory to return the names of all the files that contain
> the specified text.

3) The third command line option is: -n
"-n" Displays matched lines and their line numbers

```
EXAMPLE 1:
[zroland@ieng6-202]:docsearch:292$ grep -n "holy" technical/911report/chapter-2.txt 
70:                the holy Qur'an and some of its interpreters. He appeals to people disoriented by
308:                what was seen as a "holy war"-jihad-against an invader. The largest numbers came
328:                world markets to buy arms and supplies for the mujahideen, or "holy warriors."
911:                conveyed the same message-the duty of Muslims to carry out holy war against the
944:                the Americans to liberate the holy places "is considered a crime,"he said,"let
```

> grep -n "holy" displays all the lines and their subsequent numbers that holy appears in chapter-2

```
EXAMPLE 2:
[zroland@ieng6-202]:docsearch:293$ grep -n "tower" technical/911report/chapter-1.txt 
96:    All on board, along with an unknown number of people in the tower, were killed instantly.
122:    All on board, along with an unknown number of people in the tower, were killed instantly.
408:    Reagan National controllers then vectored an unarmed National Guard C- 130H cargo aircraft, which had just taken off en route to Minnesota, to identify and follow the suspicious aircraft. The C-130H pilot spotted it, identified it as a Boeing 757, attempted to follow its path, and at 9:38, seconds after impact, reported to the control tower:"looks like that aircraft crashed into the Pentagon sir."
418:    FAA: That was another-it was evidently another aircraft that hit the tower. That's the latest report we have.
610:    The President and the Vice President The President was seated in a classroom when, at 9:05, Andrew Card whispered to him: "A second plane hit the second tower. America is under attack." The President told us his instinct was to project calm, not to have the country see an excited reaction at a moment of crisis. The press was standing behind the children; he saw their phones and pagers start to ring. The President felt he should project strength and calm until he could better understand what was happening.
622:    At 9:33, the tower supervisor at Reagan National Airport picked up a hotline to the Secret Service and told the Service's operations center that "an aircraft [is] coming at you and not talking with us." This was the first specific report to the Secret Service of a direct threat to the White House. No move was made to evacuate the Vice President at this time. As the officer who took the call explained, "[I was] about to push the alert button when the tower advised that the aircraft was turning south and approaching Reagan National Airport."
```

> grep -n "tower" dispalys all the lines and the subsequent numbers that tower appears in chapter-1

```
EXAMPLE 3:
[zroland@ieng6-202]:docsearch:290$ grep -rn "holy" technical/
technical/911report/chapter-12.txt:91:                faith itself. Lives guided by religious faith, including literal beliefs in holy
technical/911report/chapter-13.4.txt:849:                cyclical fund-raising process (with more money coming during the holy month of
technical/911report/chapter-13.5.txt:2858:                religion is denigrated. Our holy places desecrated. Our countries are occupied. Our
technical/911report/chapter-2.txt:70:                the holy Qur'an and some of its interpreters. He appeals to people disoriented by
technical/911report/chapter-2.txt:308:                what was seen as a "holy war"-jihad-against an invader. The largest numbers came
technical/911report/chapter-2.txt:328:                world markets to buy arms and supplies for the mujahideen, or "holy warriors."
technical/911report/chapter-2.txt:911:                conveyed the same message-the duty of Muslims to carry out holy war against the
technical/911report/chapter-2.txt:944:                the Americans to liberate the holy places "is considered a crime,"he said,"let
technical/911report/chapter-5.txt:755:                brochures in Arabic about jihad, held forth to friends on the subject of holy war,
technical/911report/chapter-6.txt:51:                Jordan into Israel, and two Christian holy sites, at a time when all these locations
technical/biomed/1472-6793-3-3.txt:313:          on one-dimensional isoelectric focusing gels (ampholytes
technical/plos/journal.pbio.0020263.txt:45:        to “cultivate what Einstein referred to as ‘holy curiosity.’” She makes plain that science,
technical/plos/journal.pbio.0030105.txt:30:        melted into melancholy, sadness into ennui. “It's not about moving,” he observed, “it's
```
> grep -rn "holy" technical/ recursively lists the filenames,line numbers and lines themselves that have holy within them.

4) the fourth command line option is:
"-o" Prints only the matched parts of a macthing line

```
EXAMPLE 1:
[zroland@ieng6-202]:docsearch:300$ grep -o "holy" technical/911report/chapter-2.txt 
holy
holy
holy
holy
holy
```
> grep -o "holy" prints only the parts matching the line holy within chapter-2.txt so we get
> 5 lines returned of just holy

```
EXAMPLE 2:
[zroland@ieng6-202]:docsearch:297$ grep -ro "one piece" technical/
technical/plos/journal.pbio.0020028.txt:one piece
technical/plos/journal.pbio.0020401.txt:one piece
technical/plos/pmed.0020209.txt:one piece
```

> grep -ro "one piece" recursively goes through the technical directory and prints out the
> relative paths of all the files that contain the string "one piece" and only that string too.

```
EXAMPLE 3:
[zroland@ieng6-202]:docsearch:306$ grep -rno "one piece" technical/
technical/plos/journal.pbio.0020028.txt:158:one piece
technical/plos/journal.pbio.0020401.txt:13:one piece
technical/plos/pmed.0020209.txt:14:one piece

```

> grep -rno "one piece"recursively goes through the technical directory and prints out the relative path, the
> line number, and the string "one piece" that is found

```
EXAMPLE 4:
[zroland@ieng6-202]:docsearch:307$ grep -rino "one piece" technical/
technical/biomed/1476-069X-2-4.txt:816:One piece
technical/plos/journal.pbio.0020028.txt:158:one piece
technical/plos/journal.pbio.0020401.txt:13:one piece
technical/plos/pmed.0020209.txt:14:one piece
```

> grep -rino "one piece" recursively goes through the technical directory, this time ignoring the case finds all
> the files and lines that contain one piece and prints out the relatively path,line number, and the string
> one piece ignoring the case so this time we have 1 additional entry of One piece which was not previously
> found since case mattered.
   

