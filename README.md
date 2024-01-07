# interview-problems
Interview Algorithm Questions that are completed.


## 2) Mini-Max Sum

```
Given five positive integers, find the minimum and maximum values that can be calculated by summing exactly four of the five integers. Then print the respective minimum and maximum values as a single line of two space-separated long integers.

Example
arr = [1,3,5,7,9]
The minimum sum is 1 + 3 + 5 + 7 = 16 and the maximum sum is 3 + 5 + 7 + 9 = 24. The function prints


16 24
Function Description

Complete the miniMaxSum function in the editor below.

miniMaxSum has the following parameter(s):
arr: an array of 5 integers
Print

Print two space-separated integers on one line: the minimum sum and the maximum sum of  of  elements.

Input Format

A single line of five space-separated integers.

Constraints


Output Format

Print two space-separated long integers denoting the respective minimum and maximum values that can be calculated by summing exactly four of the five integers. (The output can be greater than a 32 bit integer.)

Sample Input

1 2 3 4 5
Sample Output

10 14
Explanation

The numbers are 1, ,2, 3, 4, and 5. Calculate the following sums using four of the five integers:
 1. Sum everything except 1, the sum is 2 + 3 + 4 + 5 = 14.
 2. Sum everything except 2, the sum is 1 + 3 + 4 + 5 = 13.
 3. Sum everything except 3, the sum is 1 + 2 + 4 + 5 = 12.
 4. Sum everything except 4, the sum is 1 + 2 + 3 + 5 = 11.
 5. Sum everything except 5, the sum is 1 + 2 + 3 + 4 = 10.

Hints: Beware of integer overflow! Use 64-bit Integer.
```

## Solution:
100%
```
fun miniMaxSum(arr: Array<Int>): Unit {
    var smallest: Int = arr[0] 
    var largest: Int = arr[0]
    var total: Long = 0

    for(number in arr){
        smallest = if (smallest < number) smallest else number
        largest = if (largest > number) largest else number        
        total = total + number
    }
    var smallestTotal = total - largest
    var largestTotal = total - smallest
    print("$smallestTotal $largestTotal")
}

fun main(args: Array<String>) {

    val arr = readLine()!!.trimEnd().split(" ").map{ it.toInt() }.toTypedArray()

    miniMaxSum(arr)
}
```

## 3) Time Conversion
```
Given a time in 12-hour AM/PM format, convert it to military (24-hour) time.
Note: - 12:00:00AM on a 12-hour clock is 00:00:00 on a 24-hour clock.
- 12:00:00PM on a 12-hour clock is 12:00:00 on a 24-hour clock.
Example
S = '12:01:00PM'
    Return '12:01:00'

S = '12:01:00AM'
    Return '00:01:00'

Function Description

Complete the timeConversion function in the editor below. It should return a new string representing the input time in 24 hour format.

timeConversion has the following parameter(s):

string s: a time in 12 hour format
Returns

string: the time in 24 hour format
Input Format

A single string 8 that represents a time in 12-hour clock format (i.e.: hh:mm:ssAM or hh:mm:ssPM).
Constraints:

All input times are valid

Sample Input
07:05:45PM
Sample Output
19:05:45
```

## Solution
100%
```
fun timeConversion(s: String): String {
    val hours: String = s.subSequence(0, 2).toString()
    val time: String = ""
    if (s.takeLast(2) == "AM") {
        if (hours == "12"){
            return "00"+s.subSequence(2, s.length-2)
        }       
        return hours+ s.subSequence(2, s.length-2)

    } else {
         if (hours == "12") {
            return "12" + s.subSequence(2, s.length-2)
        }
        return (hours.toInt() + 12).toString() + s.subSequence(2, s.length -2)
    }
}
```


## 4) Sparse Arrays
```
There is a collection of input strings and a collection of query strings. For each query string, determine how
many times it occurs in the list of input strings. Return an array of the results.
Example
strings ab' ,abc']
queries
There are 2 instances of 'ab', 1 of 'abc' and 0 of 'bc'. For each query, add an element to the return array,
results = [2,1,0].
Function Description
Complete the function matching Strings in the editor below. The function must return an array of integers
representing the frequency of occurrence of each query string in strings.
matching Strings has the following parameters:
string strings[n] - an array of strings to search
string queries[q] - an array of query strings
Returns

int[q]: an array of results for each query
Input Format
Input Format
The first line contains and integer n the size of strings
 Each of the next n lines contains a string strings[i].
The next line contains q. the size of queries1.
 Each of the next q lines contains a string queries[i].
Constraints
              1000
1 595 1000
 1 <= |strings[i], queries[i]| <= 20.

Sample Input 1

4
aba
baba
aba
xzxb
3
aba
xzxb
ab
Sample Output 1

2
1
0

Sample Input 2

3
def
de
fgh
3
de
lmn
fgh
Sample Output 2

1
0
1

Sample Input 3

13
abcde
sdaklfj
asdjf
na
basdn
sdaklfj
asdjf
na
asdjf
na
basdn
sdaklfj
asdjf
5
abcde
sdaklfj
asdjf
na
basdn
Sample Output 3

1
3
4
3
2

```

## Solution
100%
```
fun matchingStrings(strings: Array<String>, queries: Array<String>): Array<Int> {
    val repetitions = Array<Int>(queries.size){0}
    var index = 0
    for (query in queries){
        for (string in strings){
            if(query.compareTo(string) == 0){
               repetitions[index]++ 
            }
        }
        index++
    }
    return repetitions
}
```


