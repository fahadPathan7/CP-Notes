# Sum of the differences of all pairs in an array

### Procedures
- To calculate we need to sort the array first (ascending order)
- then we will traverse in a loop and add to the sum. <br><br>

> **The equation: sumOfTheArray - sumFromStartToThatNumber - remainingNumbersCnt * valueOfCurrentNumber**

<br>

### Example
If there is an array 4, 5, 2, 1, 3 then, after sorting we will get 1, 2, 3, 4, 5
<br>The sum of the array is 15.
<br>Now we will traverse from the first to the last index.

Let, the sum of the array is arrSum and the sum of the differences is difSum<br>
Now, arrSum = 15 and difSum = 0

for the value 1,<br>
difSum += 15 - 1 - 4 * 1

difSum becomes 10 after first operation

for the value 2, <br>
difSum += 15 - 3 - 3 * 2

difSum becomes 16 after second operation.

after all 5 operations the sum will be 20 (10 + 6 + 3 + 1 + 0) <br><br>

### Code segment
```c++
    int ar[5] = {1, 2, 3, 4, 5};
    int sumArr = 15, difSum = 0;
    int prevSum = 0;
    for (int i = 0; i < 5; i++) {
        prevSum += ar[i];
        difSum += sumArr - prevSum - (5 - i - 1) * ar[i];
    }
    cout << difSum << endl;
```
<br>

### Problems to practice
- [1648A](https://codeforces.com/contest/1648/problem/A)

### Solution of the problmes
- [1648A](https://codeforces.com/contest/1648/submission/196965918)


