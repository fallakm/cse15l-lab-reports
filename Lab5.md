# Putting it all together# Putting it all together

## Step 1: Debugging Scenario
**Design a debugging scenario**

### post from a student 

Hello to all tutors and the professor,

I am currently trying to complete the practice skill demo 4 and I am confused with why the `ListExamples.java` file isn't passing all of the `test.sh` test cases. My best guess is that for the first test case, there is an operation that isn't completing because the JUnit test timed out. For the second test case, I am guessing that there is some logic error with how I add the values to the final list but I don't know how to fix it. Can you please provide me with some direction on how to complete this step? 

```
student@6bb576b4edf5:~/buggy$ bash test.sh
JUnit version 4.13.2
.E.E
Time: 0.247
There were 2 failures:
1) testMerge(TestListExamples)
org.junit.runners.model.TestTimedOutException: test timed out after 100 milliseconds
        at java.base@11.0.21/java.util.Arrays.copyOf(Arrays.java:3720)
        at java.base@11.0.21/java.util.Arrays.copyOf(Arrays.java:3689)
        at java.base@11.0.21/java.util.ArrayList.grow(ArrayList.java:238)
        at java.base@11.0.21/java.util.ArrayList.grow(ArrayList.java:243)
        at java.base@11.0.21/java.util.ArrayList.add(ArrayList.java:486)
        at java.base@11.0.21/java.util.ArrayList.add(ArrayList.java:499)
        at app//ListExamples.merge(ListExamples.java:42)
        at app//TestListExamples.testMerge(TestListExamples.java:24)
2) testFilter(TestListExamples)
java.lang.AssertionError: expected:<[apple, a]> but was:<[a, apple]>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at TestListExamples.testFilter(TestListExamples.java:15)

FAILURES!!!
Tests run: 2,  Failures: 2
```

### A Response from a TA

Sure! 

When it comes to the symptoms you are experiencing in `testMerge`, I would suggest thinking about what would cause a program to time out. Generally, infinite loops are the most common cause of `TimeoutException`. So I would suggest looking at all of loop conditions and making sure that they have the appropriate terminate condition. Looking at the line number listed in the failure message can help (Should be visible in the line `at app//ListExamples.merge(ListExamples.java:42)`). 

For the symptoms in `testFilter`, I would reccomend drawing out what exactly is happening in the code. It appears that the data is getting entered in the wrong order so I would reccomend double checking the `add` method. 

### Student Reply to TA

Thanks for the help! 

For `testMerge`, I found the problem loop by looking at the line number in the JUnit failure message and noticed that the loop had was changing the incorrect variable after each iteration, resulting in the termination condition never being met. 

For `testFilter`, I noticed that the method was adding the desired elements to the wrong position. So, I just rewrote it so that it added the elements to the end instead of the beginning of the returned `ArrayList`. 

![Image](Image.png)

### The setup

#### Directory Structure

- `buggy/`
  - `ListExamples.class`
  - `ListExamples.java`
  - `StringChecker.class`
  - `TestListExamples.class`
  - `TestListExamples.java`
  - `test.sh`

#### Contents of each file before the fixes

##### Contents of `ListExamples.java`
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s); 
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index1 += 1;
    }
    return result;
  }


}
```

##### Contents of `TestListExamples.java`
```
import java.util.ArrayList;
import java.util.List;
import java.util.Arrays;
import static org.junit.Assert.*;
import org.junit.*;

public class TestListExamples {
  @Test
  public void testFilter() {
    List<String> strs = new ArrayList<>();
    strs.add("a");
    strs.add("b");
    strs.add("apple");
    List<String> filtered = ListExamples.filter(strs, s -> s.charAt(0) == 'a');
    assertEquals(filtered, Arrays.asList("a", "apple"));
  }

  @Test(timeout=100)
  public void testMerge() {
    List<String> strs1 = new ArrayList<>();
    List<String> strs2 = new ArrayList<>();
    strs1.add("a"); strs1.add("b"); strs1.add("cranberry");
    strs2.add("dragon");
    List<String> merged = ListExamples.merge(strs1, strs2);
    assertEquals(merged, Arrays.asList("a", "b", "cranberry", "dragon"));
  }
}
```

##### Contents of `test.sh`
```
set -e

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java

java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore TestListExamples
```

##### Don't have anything relevant to access in `ListExamples.class` and `TestListExamples.class`


#### Command line that triggered the bug

`bash test.sh`

![Image](Image1.png)

#### What to edit to fix the bug

The bug that was causing the error was located in the `ListExamples.java` file. So, upon examination, I had changed the line `result.add(0, s);` to `result.add(result.size(), s);` so that the `filter()` method produced the correct output. Also, I changed the line `index1 += 1;` in the third while loop in the `merge()` method to `index2 += 1;` to allow the loop to change something relevant to the termination condition. 

The fixed `ListExamples.java` is below with the exact lines having comments explaining what I changed. 

##### Contents of `ListExamples.java` after the fixes
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(result.size(), s); // Changed it to add at end of result rather than beginning 
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1; // Changed the incremented variable to index2 rather than index1
    }
    return result;
  }


}
```


## Step 2: Reflection
I learned how useful bash scripts can be. I can preset everything I want into the terminal with a single bash. I also realised how useful knowing all of this information is while doing different PA's for other course. The Labs were really helpful and I wish I could still have them for other courses. It was also useful to have someone with me while I would run into different compile errors. I also learned how to use vim so I could access everything from the terminal and also how to locate files.

