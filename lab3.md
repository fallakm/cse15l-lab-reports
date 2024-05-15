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


### Option 1: -i (ignore-case)

Source: [Geeks for Geeks](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)
<https://www.geeksforgeeks.org/grep-command-in-unixlinux/>

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
> it with a word that doesnt exist and see what happens. I will search for the term `tree` from the same directory. I will
> use the command `grep -i tree 1468-6708-3-1.txt` while being in the working directory `/Users/fallakmakhija/cse/docsearch/technical/biomed`.
> This outputs:

```
User biomed $ grep -i tree 1468-6708-3-1.txt

```

> This does not print anything which makes sense given it is never mentioned in the file.


### Option 2: -r (Recursive search)

Source: [DigitalOcean](https://www.digitalocean.com/community/tutorials/grep-command-in-linux-unix)
<https://www.digitalocean.com/community/tutorials/grep-command-in-linux-unix>

```
grep -r "string-name" files/directories
```

> The -r option is useful to search for a string recursively in your current directory and all other subdirectories
> If file/directory is not provided, the `grep -r` command will search for pattern in the current directory
> If we write `grep -r "string" * ` then it will search for the specified string across all files and directories.
> We will test this command by using `grep -r "chapter" ` in the working directory `911report` which is our
> current directory.
> COMMAND will be `grep -r "chapter"`
> The result outputs:


```
fallakmakhija@Fallaks-MacBook-Pro 911report % grep -r "chapter" 
chapter-1.txt:    Others in the agency were aware of it, as we explained earlier in this chapter.
chapter-10.txt:                chapter 3). Ashcroft told us he was determined to take every conceivable action,
chapter-10.txt:                Iraqi intelligence officer (discussed in chapter 7) and a Polish report that
chapter-11.txt:                (reprinted in chapter 4), brought the focus back to more traditional hostage taking;
chapter-11.txt:                the main focus (war in Korea), and as too unrealistic. As we pointed out in chapter
chapter-11.txt:                the embassy bombings of August 1998. We described those decisions in chapter 4. It
chapter-11.txt:            Earlier chapters describe in detail the actions decided on by the Clinton and Bush
chapter-11.txt:                capabilities were in the domestic arena. In chapter 3 we discussed these
chapter-11.txt:                Kuala Lumpur, detailed in chapter 6. In late 1999, the National Security Agency
chapter-12.txt:            As we mentioned in chapter 2, Usama Bin Ladin and other Islamist terrorist leaders
chapter-12.txt:            Many details in chapters 2, 5, and 7 illustrate the direct and indirect value of the
chapter-12.txt:                dangerous weapons. As we note in chapter 2, al Qaeda has tried to acquire or make
chapter-12.txt:                nuclear weapons for at least ten years. In chapter 4, we mentioned officials
chapter-12.txt:            First, as we will discuss in chapter 13, to open up the sharing of information across
chapter-13.1.txt:                opportunities,"some of which we reviewed in chapter 11. These are often
chapter-13.1.txt:                "connecting the dots." In chapter 11 we explained that these labels are too narrow.
chapter-13.1.txt:                    described in chapter 12.
chapter-13.1.txt:                still not sized or funded to be an executive agency. In chapter 3 we described some
chapter-13.1.txt:                regions, countries, and issues that we discuss in chapter 12. Much of the job of
chapter-13.1.txt:            We summarized the resulting organization of the intelligence community in chapter 3.
chapter-13.1.txt:                    civil-military misunderstandings we described in chapter 4. It is a problem to
chapter-13.1.txt:                describe in chapter 8, the information is distributed, but in a compartmented
chapter-13.1.txt:            In chapter 6, we described the transition of 2000-2001. Beyond the policy issues we
chapter-13.1.txt:                all-out effort to institutionalize change-can do the job. As we mentioned in chapter
chapter-13.3.txt:                summarized in chapter 2.
chapter-13.4.txt:                in chapter 2, we do not agree with this assessment. On Bin Ladin's reactions to
chapter-13.4.txt:                for the record, July 13, 2004. As discussed in chapter 7, we have examined three
chapter-13.4.txt:                chapter 8. That was not known at the time. Mihdhar was met at the Kuala Lumpur
chapter-13.4.txt:            234. In chapter 3, we discuss how this problem arose. By 2001, it had become worse.
chapter-13.4.txt:            5. Notably, as discussed in chapter 5, precisely such arrangements-in the form of
chapter-13.4.txt:                chapter
chapter-13.4.txt:                is referred to as the "Phoenix memo," discussed in chapter 8.) For Hanjour obtaining
chapter-13.4.txt:                later in this chapter, may have had a role in recruiting one or more of the muscle
chapter-13.5.txt:                the number of hijackers. As discussed later in this chapter, he was refused entry.
chapter-13.5.txt:                operation. See chapter 5.2. He has also stated that Atta included a nuclear plant in
chapter-13.5.txt:                1998, hijacking article (in chapter 4) and the August 6, 2001, article discussing
chapter-13.5.txt:                Bin Ladin's plans to attack in the United States (in this chapter)-were eventually
chapter-13.5.txt:                CIA cable, follow-up source on KSM, July 11, 2001. As noted in chapter 7, KSM has
chapter-13.5.txt:                discussed in chapter 3, and specifically from a March 1995 memorandum of then Deputy
chapter-13.5.txt:                through the OIPR screen. What had happened, as we discussed in chapter 3, was a
chapter-13.5.txt:                regulations, "Regulations" chapter of "Operational Procedures and Policies," July
chapter-13.5.txt:                Company Operations" chapters of "Operational Procedures and Policies," July 1999.
chapter-13.5.txt:            23. FDNY regulations, "Communications" chapter of "Operational Procedures and
chapter-13.5.txt:                review contacts between Iraq and al Qaeda in chapter 2. We have found no credible
chapter-13.5.txt:            15. For Murad's idea, see chapter 5, note 33.
chapter-13.5.txt:                National Intelligence Director we recommend later in this chapter.
chapter-2.txt:                airliners over the Pacific. Details on these plots appear in chapter 3.
chapter-2.txt:                in chapter 7, al Qaeda contacts with Iran continued in ensuing years.
chapter-3.txt:            In chapter 2, we described the growth of a new kind of terrorism, and a new terrorist
chapter-3.txt:                organized the bombing of two U.S. embassies. In this chapter, we trace the parallel
chapter-3.txt:                institutional beliefs and practices in chapter 8.
chapter-3.txt:                chapter 6, questioning by an especially alert Customs inspector led to the arrest of
chapter-3.txt:            Subsequent chapters will raise the issue of whether, despite tremendous talent,
chapter-3.txt:                (Timothy Mc Veigh in Oklahoma City). As we pointed out in chapter 3, the White House
chapter-5.txt:                Karachi; Mihdhar traveled from Yemen. As discussed in chapter 6, U.S. intelligence
chapter-5.txt:                plot, even as late as the summer of 2001, as discussed in chapter 7.
chapter-5.txt:            As we explained in chapter 2, Bin Ladin did not fund al Qaeda through a personal
chapter-5.txt:                discussed in more detail in chapter 7.
chapter-6.txt:            In chapters 3 and 4 we described how the U.S. government adjusted its existing
chapter-6.txt:                mind for the millennium period. In chapter 5 we introduced an al Qaeda operative
chapter-6.txt:            In chapter 5, we discussed the dispatch of two operatives to the United States for
chapter-6.txt:                reignited interest in Khallad. We will return to that story in chapter 8.
chapter-6.txt:                government since 1999 and, as we mentioned in chapter 4, the U.S. government as a
chapter-6.txt:            As discussed in chapter 4, plans of this kind were never carried out before 9/11.
chapter-6.txt:            Early in chapter 5 we introduced, along with Khalid Sheikh Mohammed, two other men
chapter-6.txt:                terrorism surged dramatically. In chapter 8, we will explore this reporting and the
chapter-7.txt:            In chapter 5 we described the Southeast Asia travels of Nawaf al Hazmi, Khalid al
chapter-7.txt:                that chapter we also described how Mihdhar was spotted in Kuala Lumpur early in
chapter-7.txt:                asked Khallad (whom we introduced in chapter 5) to maintain email contact with Hazmi
chapter-7.txt:            As we mentioned in chapter 2, while in Sudan, senior managers in al Qaeda maintained
chapter-8.txt:                to locate him. As pointed out in chapter 6, Abu Zubaydah had been a major figure in
chapter-8.txt:                the plot. As seen in chapter 7, al Qaeda's operatives made mistakes. At least two
chapter-8.txt:            In chapter 6 we discussed how intelligence agencies successfully detected some of the
chapter-8.txt:                bombing (we introduced Khallad in chapter 5, and returned to his role in the Cole
chapter-8.txt:                bombing in chapter 6).55 One of the members of the FBI's investigative team in Yemen
chapter-8.txt:                investigation on Zacarias Moussaoui. As mentioned in chapter 7, he had entered the
chapter-8.txt:                chapter 7, Moussaoui had been in contact with and received money from Ramzi
chapter-8.txt:                Surveillance Act to conduct the search (we introduced FISA in chapter 3).
chapter-8.txt:                Moussaoui, as discussed in chapter 7. As in the Moussaoui situation already
chapter-9.txt:            Like the national defense effort described in chapter 1, the emergency response to
```



> Example 2 : We use the command `grep -r "health" ./biomed/1471-2458-3-20.txt` to search for the term
> `health` in file `1471-2458-3-20.tx` of the `biomed` directory.
> This gives us the output:


```
fallakmakhija@Fallaks-MacBook-Pro technical % grep -r "health" ./biomed/1471-2458-3-20.txt
./biomed/1471-2458-3-20.txt:        immunize half a million hospital-based healthcare workers
./biomed/1471-2458-3-20.txt:        healthcare workers in emergency departments, intensive care
./biomed/1471-2458-3-20.txt:        members are declining. In Israel, almost half of healthcare
./biomed/1471-2458-3-20.txt:        U.S. healthcare workers' opinions about smallpox
./biomed/1471-2458-3-20.txt:        influence the ongoing decision-making of healthcare workers
./biomed/1471-2458-3-20.txt:          We surveyed a convenience sample of healthcare workers
./biomed/1471-2458-3-20.txt:          and self-assessed health history relative to smallpox
./biomed/1471-2458-3-20.txt:          the answers chosen), (2) the risks and health problems of
./biomed/1471-2458-3-20.txt:          Self-assessed health history relative to smallpox
./biomed/1471-2458-3-20.txt:          of healthcare workers answered "yes" (32%) or "probably"
./biomed/1471-2458-3-20.txt:        target group of 500,000 health care workers had accepted
./biomed/1471-2458-3-20.txt:        health-related risks of vaccination are paramount
./biomed/1471-2458-3-20.txt:        large unions of healthcare workers in early 2003 not to
./biomed/1471-2458-3-20.txt:        for healthcare workers are similar to those of
./biomed/1471-2458-3-20.txt:        rumor mill) are important in healthcare workers'
./biomed/1471-2458-3-20.txt:        healthcare workers about this vaccine.
```

### Option 3: -o (only-matching)

Source: [Geeks for Geeks](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)
<https://www.geeksforgeeks.org/grep-command-in-unixlinux/>

```
grep -o pattern filename

```
> Useful as it prints only the matched parts of a matching line, with each such part on a separate output line.
> Let's search for the term `threat` in the file `chapter-11.txt` of the directory `911report` with `-i` as well to
> remove case sensitivity
> We write the command `grep -oi threat chapter-11.txt`
> This is the follwing output:


```
fallakmakhija@Fallaks-MacBook-Pro 911report % grep -oi threat chapter-11.txt
threat
threat
threat
threat
threat
threat
threat
threat
threat
Threat
Threat
threat
threat
threat
threat
threat
threat
threat
threat
Threat
threat
threat
threat
threat
threat
threat
threat
threat
threat
threat
threat
threat

```

> We can also use this command but with `wc` to count the number of words
> This time we will count the number of times the word `health` appears in file `1468-6708-3-1.txt` of
> the `biomed` directory.

Example 2 : `grep -oi health 1468-6708-3-1.txt | wc`

```
fallakmakhija@Fallaks-MacBook-Pro biomed % grep -o health 1468-6708-3-1.txt | wc
      50      50     350
```

### Option 4: -v (invert-match)

Source: [Geeks for Geeks](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)
<https://www.geeksforgeeks.org/grep-command-in-unixlinux/>

```
grep -v "pattern" file.txt
```


> Used to display the lines that are not matched with the specified search string pattern using the `-v` option
> It's useful for filtering out unwanted lines from the output.
> These options provide enhanced functionality to the grep command,
> allowing for more efficient and flexible text searches in files and directories.
 **Example1** : We display the lines not containing `The` in the file `chapter-13.1.txt` of the directory `911report`
 **Command**: `grep -v "The" chapter-13.1.txt`
   

```
fallakmakhija@Fallaks-MacBook-Pro 911report % grep -v "The" chapter-13.1.txt
            HOW TO DO IT? A DIFFERENT WAY OF ORGANIZING THE GOVERNMENT
            As presently configured, the national security institutions of the U.S. government
                confronts a very different world today. Instead of facing a few very dangerous
                adversaries, the United States confronts a number of less visible challenges that
                surpass the boundaries of traditional nation-states and call for quick, imaginative,
                and agile responses.
                That is now the job of the generation that experienced 9/11. Those attacks showed,
                emphatically, that ways of doing business rooted in a different era are just not
                good enough. Americans should not settle for incremental, ad hoc adjustments to a
                system designed generations ago for a world that no longer exists.
            We recommend significant changes in the organization of the government. We know that
                the quality of the people is more important than the quality of the wiring diagrams.
                Some of the saddest aspects of the 9/11 story are the outstanding efforts of so many
                individual officials straining, often without success, against the boundaries of the
                them more effectively, achieving unity of effort. We offer five major
                recommendations to do that:
            
                unifying strategic intelligence and operational planning against Islamist
                    terrorists across the foreign-domestic divide with a National Counterterrorism
                    Center;
                unifying the intelligence community with a new National Intelligence Director;
                unifying the many participants in the counterterrorism effort and their
                    knowledge in a network-based information-sharing system that transcends
                    traditional governmental boundaries;
                unifying and strengthening congressional oversight to improve quality and
            
```



**Example 2** 

>  We can combine the `-v` option with `-i` and `wc` to count the number of
> lines, words, and characters in `chapter-1.txt` present in the directory `911report`
> that do not contain the letter `I`.
> Command used : `grep -vi "I" chapter-1.txt|wc`
> Following is the output:


```
fallakmakhija@Fallaks-MacBook-Pro 911report % grep -vi "I" chapter-1.txt|wc
     384      67     801
```
