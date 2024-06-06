# Putting it all together# Putting it all together

## Step 1: Debugging Scenario
**Design a debugging scenario**

*(Image of post from a student with a screenshot showing a symptom)*


![Image](Untitled.png)
![Image](9331C307-2C6F-4FEE-882C-4EAE50926219.jpeg)

TA Response:
> From the information that I can see, I noticed that your code is producing some runtime errors. This is the reason why you're getting the an IndexOutOfBounds Exception error. This issue might me caused because of the line 10 code. Please try to checkline 10 and see if thats whats causing the error. 

After Fixing line 10 code: 
> I was able to successfully compile and run the code. I notice that the bug was in the header of the for loop. It would keep iterating over indices up and equal the length of some string. This caused the IndexOutOfBounds error because the index of the string started at 0 and iterating to an index up to the length would be out of bounds for the last index of the string.

I used 2 files and a java single java program along side the bash script. I put everything in the same folder in order to organise and run.
![Image](BF10A817-B38A-4E75-8614-1569071B7F16.jpeg)

*(Image of the buggy code)*
![Image](3DDEC9E4-49A9-46B9-8A61-9AB831A30C6F.jpeg)

*(Image of the fixed code)*
![Image](283E2EC1-791C-4B97-A35B-D815A69FB015.jpeg)

*(Image of the bash script I used)*


![Image](3772E204-A103-49C4-97E7-C7AD72F09BEA.jpeg)

I made the edittes to the line 10 from the java program, I changed the header from '<=' to only '<' which removed the error message and printed out the desired output:
- ```for(int i = 0; i <= messages.length(); i++){```
* ```for(int i = 0; i < messages.length(); i++){```


## Step 2: Reflection
I learned how useful bash scripts can be. I can preset everything I want into the terminal with a single bash. I also realised how useful knowing all of this information is while doing different PA's for other course. The Labs were really helpful and I wish I could still have them for other courses. It was also useful to have someone with me while I would run into different compile errors. I also learned how to use vim so I could access everything from the terminal and also how to locate files.

