#7 kyu
##Count the Characters

Description:

The goal of this kata is to write a function that takes two inputs:
a string and a character. 
The function will count the number of times that character appears in the string. 
The count is case insensitive.

For example:

The character can be any alphanumeric character.

###Solutions

```{.java}
public static int charCount(String str, char c) {
    String[] arrStr = str.split("");
    int count = 0;
    for (String compare : arrStr) {
        if (!compare.equals("")) {
            if (compare.toLowerCase().equals(
                    String.valueOf(c).toLowerCase())) {
                count++;
            }
        }
    }
    return count;
}


public class CC {
  public static int charCount(String str, char c) {
    int counter = 0;
    for (int i = 0; i < str.length(); i++) {
      if (str.substring(i, i + 1).equalsIgnoreCase("" + c)) counter++;
    }
    return counter;
  }
}
```
