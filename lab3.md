# Lab Report 3 - Bugs and Commands

## Part 1 - Bugs 

I have chosen a bug from ArrayTests.

1. A failure-inducing input for the buggy program, as a JUnit test and any associated code (write it as a code block in Markdown)

    ```
    @Test 
    public void testReversedInPlaceFail() {
      int[] input1 = {1, 2, 3};
      ArrayExamples.reverseInPlace(input1);
      assertArrayEquals(new int[]{3, 2, 1}, input1);
    }
    ```


2. An input that doesn’t induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)


    ```
    @Test 
    public void testReverseInPlacePass() {
      int[] input1 = { 2 };
      ArrayExamples.reverseInPlace(input1);
      assertArrayEquals(new int[]{ 2 }, input1);
    }
    ```
3. The symptom, as the output of running the tests (a screenshot of running JUnit with at least the two inputs above)
   
   ![Symptom](symptom.png)





4. a) Code before fixing bug:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
}
```

4. b)  Code after fixing bug:
```
static void reverseInPlace(int[] arr) {
    int temp;
    for(int i = 0; i < arr.length/2; i += 1) {
      temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
}
```

5. **Briefly describe why the fix addresses the issue**
   
For the reverseInPlace() method, it was returning the original inputted array, not the new array that should be used for the reversed version of the input. The values are lost on changing the current array so a temporary array `temp` has to be created to hold the values of the current array and then assign it back to the original array and also change the parameters for the `for` loop to stop once i is less than half of array’s length.It changes the last elements before they are reversed.


## Part 2 - Researching Commands 
### Command: `grep`

I will explore the `grep` command and what it does.
As we learnt in class, `grep` is used for searching and manipulating text patterns within files.


### Option 1: -i (case-insensitive search)

Source: [Geeks for Geeks](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)

```
grep -i "pattern" file.txt
```

> The -i option enables to search for a string case insensitively in the given file (ignore-case). It ignores the case of letters, making the search more flexible.
> I will search for the term `Disease` in the `biomed` directory from `./techincal`
> using the command `grep -i "Disease" ./biomed/1477-7525-1-12.txt` while being in `/Users/fallakmakhija/cse/docsearch/technical`.
> This should make grep case insensitive
> This results in the output:

```
fallakmakhija@Fallaks-MacBook-Pro technical % grep -i "Disease" ./biomed/1477-7525-1-12.txt
        model of chronic disease management, with patients taking a
        persons treated for chronic diseases [ 6 7 8 9 10 11 ] ,
        between disease progression and HRQOL.
        Since 1990, the Centers for Disease Control and
        relevant to HIV disease. Wu et al found that their modified
        disease. New developments in the treatment of HIV have
        advanced disease. A majority of the SHAS participants had
        Critical indicators of disease progression, such as CD4
        disease; indeed, 83.6% were reported to the national
        relationship of disease progression, therapy, and HRQOL
        The evolution toward treatment of HIV disease as a
```
> As we can see this prints all the lines that contain the word `Disease` regardless of case sensitivity. This is an important 
> feature because it gives us the ability to search with a term being case insensitive.
> Now we will use this command to check for the term `TRADE` from the directory `911report` from `./technical`
> use the command `grep -i "TRADE" chapter-9.txt` while being in the working directory `/Users/fallakmakhija/cse/docsearch/technical/911report`.
> This results in output:

```
fallakmakhija@Fallaks-MacBook-Pro 911report % grep -i "TRADE" chapter-9.txt
                World Trade Center rested not with national policymakers but with private firms and
            The World Trade Center.
            The World Trade Center (WTC) complex was built for the Port Authority of New York and
                of America, New York City and specifically the World Trade Center had been the
                and exposed vulnerabilities in the World Trade Center's and the city's emergency
                Port Authority World Trade Department employees-including those not on the
                Authority's nine facilities, including the World Trade Center.
                overall response to an The World Trade Center Radio Repeater System Rendering by
                    1 World Trade Center (the North Tower) at 8:46 until the South Tower was hit
                    2 World Trade Center (the South Tower) at 9:03 until the collapse of the South
                airplane crash at the World Trade Center. The air traffic controllers had been
                vicinity of the World Trade Center and evacuating civilians from those
                civilians in the World Trade Center complex, because of the magnitude of the
                World Trade Center that same morning included catastrophic damage 1,000 feet above
                experience of the civilians at the World Trade Center on 9/11.
                disaster strike. Clearly, many building occupants in the World Trade Center did not
                World Trade Center attacks, the FDNY as an institution proved incapable of

```
> Now lets try to use
> it with a word that doesnt exit and see what happens. I will search for the term `tree` from the same directory. I will
> use the command `grep -i tree 1468-6708-3-1.txt` while being in the working directory `/Users/fallakmakhija/cse/docsearch/technical/biomed`.
> This outputs:

```
User biomed $ grep -i tree 1468-6708-3-1.txt

```

> This does not print anything which makes sense given it is never mentioned in the file.


### Option 2: -r (Recursive search)
