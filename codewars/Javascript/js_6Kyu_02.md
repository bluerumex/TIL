#6 kyu
##Counting Duplicates

```
Description:

Given an array (arr) as an argument complete the function 
countSmileys that should return the total number of smiling faces.

Rules for a smiling face:
-Each smiley face must contain a valid pair of eyes. Eyes can be marked as : or ;
-A smiley face can have a nose but it does not have to. Valid characters for a nose are - or ~
-Every smiling face must have a smiling mouth that should be marked with either ) or D.
Valid smiley face examples:
:) :D ;-D :~)
Invalid smiley faces:
;( :> :} :] 

Example cases:

countSmileys([':)', ';(', ';}', ':-D']);       // should return 2;
countSmileys([';D', ':-(', ':-)', ';~)']);     // should return 3;
countSmileys([';]', ':[', ';*', ':$', ';-D']); // should return 1;

```

###Solution
```{.javascript}
function countSmileys(arr) {
    var count = 0;
    for (var i in arr) {
        arr[i].match(/[:;][~-][)D]|[:;][)D]/)!=null?count++:[];
    }
    return count;
}


const countSmileys = ss => ss.reduce((a, s) => a + /^[:;][-~]?[D)]$/.test(s), 0);


function countSmileys(arr) {
  return arr.filter(x => /^[:;][-~]?[)D]$/.test(x)).length;
}


function countSmileys(arr) {
  return arr.reduce((n, s) => /^[:;][-~]?[)D]$/.test(s) ? n + 1 : n, 0)
}

```