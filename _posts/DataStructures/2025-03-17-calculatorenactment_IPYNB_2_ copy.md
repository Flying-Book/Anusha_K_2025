---
layout: post
title: Calculator Enactment
categories: ['AP CSA']
description: Continue with Classes, Queues, performing Sorts and BigO analysis on your algorithm(s).
permalink: /data_structures/calculator
toc: False
comments: True
---

## Reverse Polish Notation (RPN) & Postfix Evaluation  

### **Understanding Stacks and Queues**  
- **Stack (LIFO - Last In, First Out)**: Think of stacking cards. The last one placed is the first one removed.  
- **Queue (FIFO - First In, First Out)**: Think of a line at a store. The first one in is the first one out.  

---

### **What is Reverse Polish Notation (RPN)?**  
- **Infix Notation**: Standard mathematical notation where operators are between operands. (e.g., `3 + 5 * 8`)  
- **Postfix Notation (RPN)**: Operators come after the operands. (e.g., `35+8*` instead of `(3+5)*8`)  

**Example Conversions:**  
1. `3 * 5` → `35*`  
2. `(3 + 5) * 8` → `35+8*`  

---

### **Postfix Expression Evaluation**  
**Example:** Solve `8 9 + 10 3 * 8 *`  
#### **Step-by-Step Calculation:**
1. `8 9 +` → `17`
2. `10 3 *` → `30`
3. `30 8 *` → `240`
4. Final result: `17 240` (Not combined yet, needs more context)  

**Try this:** Solve `8 2 ^ 8 8 * +`  
#### **Step-by-Step Calculation:**
1. `8 2 ^` → `64` (Exponentiation: `8^2 = 64`)
2. `8 8 *` → `64`
3. `64 64 +` → `128` (Final result)  

---

### **Why Use Postfix Notation?**  
- **Follows PEMDAS naturally** (Parentheses, Exponents, Multiplication/Division, Addition/Subtraction).  
- **Operators go into a stack**, while **numerals go into a queue**.  
- **Easier to evaluate expressions using stacks**, reducing complexity in parsing.  

---

### **Popcorn Hack - Convert to Infix!**  
Convert the following **postfix expressions** into **infix notation**:

1. `6 3 * 4 +`
2. `10 2 8 * + 3 -`
3. `15 3 / 4 2 * +`
4. `7 3 2 * + 5 -`
5. `9 3 + 2 ^`



### Answers Here for Popcorn Hack

### Infix to RPN
- For every “token” in infix
[![824-E9-D4-F-D60-A-4941-B42-F-32-C730-BD9-DA5.png](https://i.postimg.cc/bJz03hkP/824-E9-D4-F-D60-A-4941-B42-F-32-C730-BD9-DA5.png)](https://postimg.cc/3ycDxztf)
[![85-DC050-E-F993-400-D-8608-179-A68144-DC4.png](https://i.postimg.cc/VL3j2MnD/85-DC050-E-F993-400-D-8608-179-A68144-DC4.png)](https://postimg.cc/YhzGWvXW)
  - If token is number: push into queue
  - Else if token is operator 
    - While the stack isn't empty, and the operator at the top of the stack has greater or equal “precedence” to the current token, pop values from stack into the queue. 
    - Then push the “token” into the stack.
  - Else if token is “(“
    - Push token into stack
  - Else if token is “)”
    - Pop elements from stack to queue until you reach the “(“
    - Remove “(“ from the stack
[![99638-DD9-D95-C-48-B4-A8-E5-A406-EBA93-F44.png](https://i.postimg.cc/pTThmXKm/99638-DD9-D95-C-48-B4-A8-E5-A406-EBA93-F44.png)](https://postimg.cc/5HhNGJ7J)

### Evaluate the RPN
- Make new stack
- For every token in queue
  - If token is number: push into stack
  - If token is operator:
    - Take 2 nums from top of the stack
    - Use the operator: [num1] (operator) [num2]
    - Put result into stack
- When stack only has 1 element, you have your answer!


[![A117-BCA3-60-D8-41-F6-BFFD-FD10-C7453-D5-D.png](https://i.postimg.cc/Ls4BVSzp/A117-BCA3-60-D8-41-F6-BFFD-FD10-C7453-D5-D.png)](https://postimg.cc/bZMtzKCC)

## Homework:
* Instead of making a calculator using postfix, make a calculator that uses prefix (the operation goes before the numerals)
* Prefix: 3*5 becomes *35, (7-5)*2 becomes *2-75


```python
import java.util.Stack;

public class PrefixEvaluator {

    public static int calculatePrefix(String prefixExpression) {
        Stack<Integer> operandStack = new Stack<>();
        String validOperators = "+-*/";

        // Traverse the expression from right to left
        for (int index = prefixExpression.length() - 1; index >= 0; index--) {
            char currentChar = prefixExpression.charAt(index);

            // If the character is a digit, push it onto the stack
            if (Character.isDigit(currentChar)) {
                operandStack.push(Character.getNumericValue(currentChar));
            }
            // If the character is an operator
            else if (validOperators.indexOf(currentChar) != -1) {
                // Pop two operands from the stack
                int firstOperand = operandStack.pop();
                int secondOperand = operandStack.pop();

                // Perform the operation and push the result back onto the stack
                switch (currentChar) {
                    case '+':
                        operandStack.push(firstOperand + secondOperand);
                        break;
                    case '-':
                        operandStack.push(firstOperand - secondOperand);
                        break;
                    case '*':
                        operandStack.push(firstOperand * secondOperand);
                        break;
                    case '/':
                        operandStack.push(firstOperand / secondOperand);
                        break;
                }
            }
        }

        // The final result will be the only element left in the stack
        return operandStack.pop();
    }

    public static void main(String[] args) {
        String prefixExpression = "*2-75"; 
        int finalResult = calculatePrefix(prefixExpression);
        System.out.println(finalResult);
    }
}
```
