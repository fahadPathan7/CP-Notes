# Skip some digits and print the nth number


### Index
- [Basic discussion](#basic-discussion)
- [Code segment](#code-segment)
- [Problems to practice](#problems-to-practice)
- [Solution of the problems](#solution-of-the-problems)

<br>

### Basic discussion

The problem can be described as someone hates digit 4. So you have to answer his queries without using that digit. <br>
If he wants to know the 4th natural number, you should say it is 5 (1, 2, 3, 5).<br>If he wants 13th natural number, it would be 15. And so on...
<br>

**We can solve this problem by using base of a new number system.**

As we are skipping digit 4, we have a number system of base 9. And the digits are 0, 1, 2, 3, 5, 6, 7, 8, 9. <br>
Here 5, 6, 7, 8, 9 are compared to 4, 5, 6, 7, 8.

So, to get a desired number in this base form, we have to mod and divide the given number until the number becomes zero.<br>
And the mod values in reverse order will be the desired number.

<br>

### Simulation
The operations we need to get the 13th number in the new base (base 9) system are,
<br>First operation,<br>
We will get the mod, num % 9 = 5 (we are getting 4 here. but we are representing 4 as 5 in the base system)<br>
and after integer division, num = num / 9 = 1 <br><br>
Second operation,<br>
We will again get the mod, num % 9 = 1 (we are getting 1 here and not changing. because the digits 0, 1, 2, 3 are representing themselves in the base system)<br>
and after integer division, num = num / 9 = 0<br>
As we got 0, we do not need to perform further operations.<br><br>
The mod values we got are the 5 and 1. the leftmost mod value is the LSB(Least Significant Bit) and the rightmost mod value is the MSB(Most Significant Bit).<br>So, when we will write the number we will write it in the reverse order. And the number will be 15.<br>
So, the number 13 in 10 base system is exactly same as 15 in 9 base system.<br>

<br>

### Code segment
```c++
void convert(int n) {
    stack<int> st; // stack will be used to store the mod values. beause the MSB will be the top most element of the stack.
    while (n > 0) {
        int temp = n % 9; // temporary storing mod value
        n /= 9; // dividing the number
        if (temp >= 4) temp++; // checking if the mod value is grater than or same as 4. As we are skipping digit 4 in the base system
            // the digit 4 will be represented by 5. 5 will be represented by 6. and so on. so we need to increase the digit by one in this case.
        st.push(temp); // storing into the stack
    }
    while (!st.empty()) {
        // printing the value
        cout << st.top();
        st.pop();
    }
    cout << endl;
}
```

<br>

### Similar Questions
- skip 3 & 7 and print nth natural number
- skip 1, 4 & 5 and print nth natural number

<br>

### Problems to practice
- [Living Sequence](https://codeforces.com/contest/1811/problem/E)

<br>

### Solution of the problems
- [Living Sequence](https://codeforces.com/contest/1811/submission/200962724)