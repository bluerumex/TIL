#7Kyu
##Simple Fun #176: Reverse Letter

```
Description:

Task

Given a string str, reverse it omitting all non-alphabetic characters.
Example

For str = "krishan", the output should be "nahsirk".

For str = "ultr53o?n", the output should be "nortlu".
Input/Output

[input] string str

A string consists of lowercase latin letters, digits and symbols.
[output] a string

```

###Solution
```{.javascript}
function reverseLetter(str) {
    var strArr = str.split(""),
        i, ret = [], match = /[A-Za-z]/;

    for (i = strArr.length - 1; i >= 0; i--) {
        if (match.test(strArr[i])) {
            ret.push(strArr[i]);
        }
    }
    return ret.join('');
}


function reverseLetter(str) {
  return [...str].reduce((s, c) => /[A-Z]/i.test(c) ? c + s : s, "")
}


function reverseLetter(str) {
  return str
        .split("")
        .filter(char => /[a-z]/i.test(char))
        .reverse()
        .join("");
}
```