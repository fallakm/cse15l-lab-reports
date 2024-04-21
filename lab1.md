# *CSE15L LAB REPORTS*
***
## **Lab Report 1** 
***

1. For `cd` command:
   
   * *With no arguments*
     
     ![Image](image1.png)
     
     cd with no arguments does not do anything
      
     Absolute path before : `/Users/fallakmakhija`
     



   * *With directory as argument*

     ![Image](image2.png)
     
     no error produced, changes the current directory to `lecture1`
     
     Absolute path before : `/Users/fallakmakhija`
     
     Absolute path after command :  `/Users/fallakmakhija/lecture1`


   * *With file as argument*

     ![Image](image3.png)

     error produced since cd works only to change directories and not to file
     So, `cd Hello.java` produces error
     
     Absolute path before : `/Users/fallakmakhija/lecture1`
     
     Absolute path after command : `/Users/fallakmakhija/lecture1`


     

3. For `ls` command:
   
   * *With no arguments*

     ![Image](image4.png)
     
     Running ls with no arguments lists the contents of the current directory
     which is `lecture1`
     
     No error is produced
     
     Absolute path before: `/Users/fallakmakhija/lecture1`



   * *With directory `messages` as argument*

     ![Image](image5.png)

     Returns list of files and directories in the specified directory
     which is `messsages`
     
     No error produced
     
     Absolute path before: `/Users/fallakmakhija/lecture1`



   * *With file `Hello.java` as argument*

     ![Image](image6.png)

     Running this command lists the name of the itself
     In this case, it is `Hello.java`
     
     Absolute path before: `/Users/fallakmakhija/lecture1`

     
     
4. For `cat` command:

   * *With no arguments*
     
     ![Image](image7.png)
     
     no error produced,does not do anything
     
     there is no output , it waits for input from standard input
     
     Absolute path before: `/Users/fallakmakhija/lecture1`
     


   * *With directory `messages` as argument*
  
     ![Image](image8.png)
  
     Absolute path before: `/Users/fallakmakhija/lecture1`
     
     Error produced
     
     attempts to concatenate the contents of a directory `messages`, which is not possible.
     


   * *With file `Hello.java` as argument*

     ![Image](image9.png)
     
     Absolute path before: `/Users/fallakmakhija/lecture1`
  
     No error produced
     
     displays/prints the contents of the specified file `Hello.java` 
     
     
   

     
     
     
