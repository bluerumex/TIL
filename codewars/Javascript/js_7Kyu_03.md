#7Kyu
##Don't give me five!

In this kata you get the start number and the end number of a region and should return the count of all numbers except numbers with a 5 in it. The start and the end number are both inclusive!
```
Examples:

1,9 -> 1,2,3,4,6,7,8,9 -> Result 8
4,17 -> 4,6,7,8,9,10,11,12,13,14,16,17 -> Result 12
The result may contain fives. ;-)

The start number will always be smaller than the end number. Both numbers can be also negative!
```
###Solutions
```{.javascript}
function dontGiveMeFive(start, end) {
    var arr = [];

    for (var i=start; i<=end; i++) {
        if ((i).toString().match(5) == null) {
            arr.push(i);
        };
    }
    return arr.length;
}
```

###Best Practices

case. 1
```{.javascript}
function dontGiveMeFive(start, end) {
  let count = 0
  for (let i = start; i <= end; i++) {
    if (!/5/.test(i)) {
      count++
    }
  }
  return count
}
```

case. 2
```{.javascript}
const dontGiveMeFive4=(s,e)=>[...Array(e-s+1)].reduce((r,_,n)=>r+!/5/.test(n+s),0);
```