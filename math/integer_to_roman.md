#Integer to Roman

[原題網址](http://www.lintcode.com/en/problem/integer-to-roman/)

題意：把整數轉換為羅馬數字


```java
public String intToRoman(int n) {
        
    int[] number = new int[]{1000, 500, 100, 50, 10, 9, 5, 4, 1};
    String[] roman = new String[]{"M", "D", "C", "L", "X", "IX", "V", "IV", "I"};
    
    StringBuilder str = new StringBuilder();
    for (int i = 0; i < number.length; i++) {

        while (n >= number[i]) {
            str.append(roman[i]) ;
            n -= number[i];
        }
    }
    
    return new String(str);
    
}
```