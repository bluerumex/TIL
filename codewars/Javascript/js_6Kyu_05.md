#6 kyu
##Length of missing array

```
Description:

You get an array of arrays.
If you sort the arrays by their length, you will see, that their length-values are consecutive.
But one array is missing!


You have to write a method, that return the length of the missing array.

Example:
[[1, 2], [4, 5, 1, 1], [1], [5, 6, 7, 8, 9]] --> 3


If the array of arrays is null/nil or empty, the method should return 0.

When an array in the array is null or empty, the method should return 0 too!
There will always be a missing element and its length will be always between the given arrays. 
```

###Solution
```{.javascript}
function getLengthOfMissingArray(arrayOfArrays) {
    var missingArrLength = 0;
    var arrayOfArraysLength = [];
    for (var i in arrayOfArrays) {
        arrayOfArraysLength.push(arrayOfArrays[i]!=null?arrayOfArrays[i].length:0);
    }
        arrayOfArraysLength.sort(function(a, b) {
        return a - b;
    });
    var val = arrayOfArraysLength[0];
    if (val == 0) {
        return 0;
    }
    for (var i in arrayOfArraysLength) {
        var arrVal = arrayOfArraysLength[i];
        if (val != arrVal) {
            missingArrLength = val;
            break;
        } else {
            val++;
        }
    }
    return missingArrLength;
}


function getLengthOfMissingArray(arr) {
  return !arr||(ar=arr.map((x,i)=>x?x.length:0).sort((a,b)=>a-b)).indexOf(0)>-1
         ?0:ar.filter((x,i)=>x!=i+ar[0]).concat([1])[0]-1
}


function getLengthOfMissingArray(arrayOfArrays) {
  const lengths = (arrayOfArrays || [])
    .map(a => a ? a.length : 0)
    .sort((a, b) => a - b)
  
  if (lengths.includes(0)) {
    return 0
  }

  for (let i = 0; i < lengths.length - 1; i++) {
    if (lengths[i] + 1 !== lengths[i + 1]) {
      return lengths[i] + 1
    }
  }

  return 0
}

```