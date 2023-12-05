# Part1  Debugging Scenario
## The file & directory structure
![Image](structure.png)

## The contents of each file before fixing the bug

#### FileProcessor.java:

![Image](original_FileProcessor.png)

Markdown:
```
import java.nio.file.*;
import java.io.*;

public class DataProcessor {
    public static void main(String[] args) {
        if (args.length != 1) {
            System.out.println("Usage: java DataProcessor <filename>");
            return;
        }

        String filename = args[0];
        Path file = Paths.get(filename);

        try {
            String content = Files.readString(file);
            int wordCount = countWords(content);
            System.out.println("Word Count: " + wordCount);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    private static int countWords(String content) {
        return content.split(" ").length;
    }
}

```

#### analysis.sh:
![Image](original_analysis.png)

Markdown:
```
#!/bin/bash

javac DataProcessor.java
java DataProcessor wrongfile.txt

```
#### data.txt:

![Image](original_data.png)

Markdown:
```
Hello, this is a sample text file. 
It contains multiple lines and various word counts.

Some lines have more words than others.
This line, for example, has exactly eight words.

Punctuation! Shouldn't affect; the: word, count.

```

## Conversation:

#### StudentA:
I'm working on a project where I have a Java program that processes data from a file and then outputs results. There's also a Bash script that sets up the environment, compiles the Java code, and runs it with specific parameters. However, I'm encountering some odd behavior:

The Java program doesn't seem to process the file data correctly.

I'm attaching a screenshot of the terminal output after running the Bash script.
Any suggestions on what might be going wrong?

![Image](bash_output1.png)

command executed on terminal:
```
$ bash analysis.sh
```

Markdown for output:
```
Error reading file: wrongfile.tt
```
#### TA:
To address the first issue, could you insert a print statement in your Java code to show the file's contents that it's reading? This will help us verify if the file reading part is working correctly.

### StudentA:
After adding a print statement in my Java program, I noticed it's reading an empty file or incorrect content. It seems the issue might be with the file path or how the file is passed to the Java program.

Modified FileProcessor.java:

![Image](modifiedFile_First.png)

Markdown for how I added in FileProcessor.java:
```
if (!Files.exists (file) || Files.isDirectory (file)) (
System.out.printin("File not found or is a directory: " + filename);
return:
) else if (Files.size(file) == 0) (
System.out.printin("file is empty: " + filename);
return;
}

```

command executed on terminal:
```
$ bash analysis.sh
```
Output:
![Image](First_student.png)

Markdown for Output
```
File not found or is a directory: wrongfile.txt
```
#### TA:
Thanks for the update. Please check the file path in your Bash script and make sure the file exists and is not empty.

### StudentA:
I checked and corrected the file path in the Bash script. Now the Java program reads the correct file, but the processing logic still seems off. The word count is incorrect.

Markdown for how I fixed in the bash script:
```
java FileProcessor data.txt
```

Corrected analysis.sh:
![Image](second_analysis.png)

command executed on terminal:
```
$ bash analysis.sh

```

Output:
![Image](wordcount_output.png)


#### TA
It looks like the issue is with the word counting logic in your Java program. Can you share the relevant part of your Java code where you are counting words? We need to ensure it handles cases like multiple spaces, punctuation, etc.

### StudentA:
Here's the Java code snippet for word counting. I can't find what's wrong here. Probably, it has an issue with splitting words?
```
 private static int countWords(String content) {
        return content.split(" ").length;
    }
}
```
#### TA
Yes, The word counting logic doesn't handle multiple spaces or punctuation properly. Update it to split words more accurately, considering these cases.

### StudentA:
I fixed the code like the following for countWords method in FileProcessor.java:
```
// Updated to correctly count words, considering multiple spaces and punctuation
        return content.trim().split("\\s+").length;
```
![Image](fixedwordcount.png)

Thank you, I got the correct output.

Output:
![Image](wordcount_fixedoutput.png)

#### Final Modified FileProcessor.java:


![Image](finalmodifiedFile.png)

Markdown:
```
import java.nio.file.*;
import java.io.*;

public class FileProcessor {
    public static void main(String[] args) {
        if (args.length != 1) {
            System.out.println("Usage: java FileProcessor <filename>");
            return;
        }
        
        String filename = args[0];
        Path file = Paths.get(filename);


        try{

            if (!Files.exists(file) || Files.isDirectory(file)) {
                System.out.println("File not found or is a directory: " + filename);
                return;
            } else if (Files.size(file) == 0) {
                System.out.println("File is empty: " + filename);
                return;
            }

            String content = Files.readString(file);
            int wordCount = countWords(content);
            System.out.println("Word Count: " + wordCount);
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
    }

    private static int countWords(String content) {
       // Updated to correctly count words, considering multiple spaces and punctuation
        return content.trim().split("\\s+").length;
    }
}
```

#### Final Modified analysis.sh:

![Image](finalmodifiedbash.png)

Markdown:
```
#!/bin/bash

javac FileProcessor.java
java FileProcessor data.txt
```

# Part2 Reflection

I learned how to transfer data from a local to a remote server. I am also glad to know how to use Debbagger with jdb command. I didn't know how I could set breakpoints and run to debug my code before. These skills would help me solve any error I face in the future program. I also enjoyed how to use Vim editor, which is different from a normal code editor. It was hard to memorize every command to move cursor around until I get used to it, but I felt it quite convinient now since I can jump to specific line in my code with a specific command, for example : the line number.
