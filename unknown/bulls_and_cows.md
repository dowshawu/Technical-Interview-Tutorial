# Bulls and Cows

[Leetcode](https://leetcode.com/problems/bulls-and-cows/)

題意：

其實就是小時候玩的猜數字。

You are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is.

Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). 

Your friend will use successive guesses and hints to eventually derive the secret number.

For example:
```
Secret number:  "1807"
Friend's guess: "7810"
```
Hint: 1 bull and 3 cows. (The bull is 8, the cows are 0, 1 and 7.)

Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. In the above example, your function should return "1A3B".

Please note that both secret number and friend's guess may contain duplicate digits, for example:
```
Secret number:  "1123"
Friend's guess: "0111"
```
In this case, the 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow, and your function should return "1A1B".

You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.

解題思路：

update 2015.12.6

用兩個bucket即可，只要值與位置相同，則bulls++，否則在對應的位置++，最後再掃一次找0-9中個數較小的來計算cows，程式碼如下：


```java
public class Solution {
    public String getHint(String secret, String guess) {
        if (secret == null || guess == null || secret.length() == 0 || guess.length() == 0) {
            return "";
        }
        
        int[] sArray = new int[10];
        int[] gArray = new int[10];
        int bulls = 0;
        for (int i = 0; i < secret.length(); i++) {
            if (secret.charAt(i) != guess.charAt(i)) {
                sArray[secret.charAt(i) - '0']++;
                gArray[guess.charAt(i) - '0']++;
            } else {
                bulls++;
            }
        }
        
        int cows = 0;
        for (int i = 0; i < 10; i++) {
            cows += Math.min(sArray[i], gArray[i]);
        }
        
        return bulls + "A" + cows + "B";
    }
}
```

使用hashmap，以及一個matched的array來判斷。

```java
public class Solution {
    public String getHint(String secret, String guess) {
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        boolean[] matched = new boolean[secret.length()];
        int a = 0;
        int b = 0;
        for (int i = 0; i < secret.length(); i++) {
            char s = secret.charAt(i);
            char g = guess.charAt(i);
            if (s == g) {
                matched[i] = true;
                a++;
            } else {
                if (!map.containsKey(s)) {
                    map.put(s, 1);
                } else {
                    map.put(s, map.get(s) + 1);
                }
            }
        }
        
        for (int i = 0; i < guess.length(); i++) {
            if (matched[i]) {
                continue;
            }
            char g = guess.charAt(i);
            if (map.containsKey(g)) {
                b++;
                if (map.get(g) == 1) {
                    map.remove(g);
                } else {
                    map.put(g, map.get(g) - 1);
                }
            }
        }
        
        String res = a + "A" + b + "B";
        return res;
    }
}
```