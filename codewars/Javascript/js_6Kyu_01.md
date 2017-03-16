#6 kyu
##Counting Duplicates

```
Description:

Count the number of Duplicates

Write a function that will return the count of distinct case-insensitive alphabetic characters and numeric digits 
that occur more than once in the input string. 
The input string can be assumed to contain only alphanumeric characters, 
including digits, uppercase and lowercase alphabets.

Example

"abcde" -> 0 # no characters repeats more than once
"aabbcde" -> 2 # 'a' and 'b'
"aabbcdeB" -> 2 # 'a' and 'b'
"indivisibility" -> 1 # 'i'
"Indivisibilities" -> 2 # 'i' and 's'
"aa11" -> 2 # 'a' and '1'
```

###Solution
```{.javascript}
function duplicateCount(text){
    var splitText = [];
    var totalCount = 0;
    var duplicateCnt = 0;

    for (var i=0; i<text.length; i++) {
        var str = text[i].toLocaleLowerCase();
        var idx = splitText.indexOf(str);

        if (idx == -1) {
            splitText.push(str);
        }

    }

    for (var i=0; i<text.length; i++) {
        var str = splitText[i];

        for (var j=0; j<text.length; j++) {
            if (str == text[j].toLocaleLowerCase()) {
                duplicateCnt++;
            }
        }

        if (duplicateCnt >= 2) {
            totalCount++;
        }

        duplicateCnt = 0;
    }

    return totalCount;
}


function duplicateCount(text){
  return (text.toLowerCase().split('').sort().join('').match(/([^])\1+/g) || []).length;
}
```