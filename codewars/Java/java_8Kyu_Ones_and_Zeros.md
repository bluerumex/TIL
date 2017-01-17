#8 kyu
##Ones and Zeros

Description:

Given an array of one's and zero's convert the equivalent binary value to an integer.
Eg: [0, 0, 0, 1] is treated as 0001 which is the binary representation of 1

Examples:

Testing: [0, 0, 0, 1] => 1
Testing: [0, 0, 1, 0] => 2
Testing: [0, 1, 0, 1] => 5
Testing: [1, 0, 0, 1] => 9
Testing: [0, 0, 1, 0] => 2
Testing: [0, 1, 1, 0] => 6
Testing: [1, 1, 1, 1] => 15
Testing: [1, 0, 1, 1] => 11

###Solutions

```{.java}
public class BinaryArrayToNumber {

    public static void main(String arsg[]) {
        List<Integer> list = new ArrayList<Integer>(Arrays.asList(1, 0, 0, 1));
        System.out.println(convertBinaryArrayToInt(list));
    }

    public static int convertBinaryArrayToInt(List<Integer> binary) {
        int arr[] = new int[]{8, 4, 2, 1};
        int sum = 0;

        for(int i=0; i<binary.size(); i++) {
            if (binary.get(i) == 1) {
                sum += arr[i];
            }
        }
        return sum;
    }
}
```

###Best Practices
case. 1
```{.java}
public class BinaryArrayToNumber {

    public static int ConvertBinaryArrayToInt(List<Integer> binary) {
        
        int number = 0;
        for (int bit : binary)
            number = number << 1 | bit;
        return number;
    }
}
```

case. 2
```{.java}
public class BinaryArrayToNumber {

    public static int ConvertBinaryArrayToInt(List<Integer> binary) {
    
    String res = "";
    
    for (int i : binary)
            res += i; 
        
    return Integer.parseInt(res, 2);
    }
}
```

case. 3
```{.java}
public class BinaryArrayToNumber {

    public static int ConvertBinaryArrayToInt(List<Integer> binary) {
      int ans = 0;
      for (int i = 0; i < binary.size(); i++) {
        if (binary.get(i) == 1) ans += Math.pow(2,binary.size() - i - 1);
      }
      return ans;
    }
}
```