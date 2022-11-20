题目链接：[1106. 解析布尔表达式 - 力扣（LeetCode）](https://leetcode.cn/problems/parsing-a-boolean-expression/)

解题思路：

> 采用stack（栈）结构处理，将元素以此入栈，直至遇到")"符号进行出栈操作，出栈遇到"("结束出栈，对符号"("到")"内的表达式进行判断

解题代码：

```java
class Solution {
    public boolean parseBoolExpr(String expression) {
        char[] chars = expression.toCharArray();
        ArrayDeque<Character> stack = new ArrayDeque<>();
        for (int i = 0; i < chars.length; i++) {
            // 如果是)符号，则处理当前的表达式，到遇到的第一个(符号的下一个符号
            if (chars[i] == ')') {
                StringBuilder strb = new StringBuilder();
                while (stack.peekLast() != '(') {
                    strb.append(stack.pollLast());
                }
                stack.pollLast();
                Character contr = stack.pollLast();
                if (contr == '&') {
                    if (strb.toString().contains("f")) {
                        stack.add('f');
                        continue;
                    }
                    stack.add('t');
                }
                if (contr == '|') {
                    if (strb.toString().contains("t")) {
                        stack.add('t');
                        continue;
                    }
                    stack.add('f');
                }
                if (contr == '!') {
                    if (strb.toString().equals("t")) {
                        stack.add('f');
                    } else {
                        stack.add('t');
                    }
                }
                continue;
            }
            stack.add(chars[i]);
        }
        return stack.pollLast() == 't';
    }
}
```



![image-20221120212045701](resources/leetcode1106%E8%A7%A3%E6%9E%90%E5%B8%83%E5%B0%94%E8%A1%A8%E8%BE%BE%E5%BC%8F.assets/image-20221120212045701.png)