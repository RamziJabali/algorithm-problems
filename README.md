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

## 5) Lonely Integer
```
Given an array of integers, where all elements but one occur twice, find the unique element.

Example
a=(1,2,3,4,2,1)

The unique element is 4.

Function Description

Complete the lonelyinteger function in the editor below.

lonelyinteger has the following parameter(s):

© int afny: an array of integers

Returns

* int the element that occurs only once

Input Format

The first line contains a single integer, n, the number of integers in the array.

The second line contains n space-separated integers that describe the values in a.
Constraints

* 1 <= n < 100

* It is guaranteed that m is an odd number and that there is one unique element.

* 0 <= a[i] <= 100, where O <= i < n.

```

## Solution
100%
```
fun lonelyinteger(a: Array<Int>): Int {
    val maxSize = 100
    val repetitionsArray = Array<Int>(maxSize){0}
    for (index in a.indices) {
        val newIndex = a[index] % maxSize
        repetitionsArray[newIndex] += 1
    }
    for (index in repetitionsArray.indices) {
        if(repetitionsArray[index] == 1){
            return index
        }
    }
    return 0
}
```

## 6) Flipping Bits
```
You will be given a list of 32 bit unsigned integers. Flip all the bits (1 + 0 and 0 —+ 1) and return the result as
an unsigned integer.

Example

n=%

910 = 10012. We're working with 32 bits, so:

000000000000000000000000000010012 = 919
11111111111111111111111111110110) = 429496728619

Return 4294967286
Function Description
Complete the flippingBits function in the editor below.

flippingBits has the following parameter(s):

* intn:an integer
Returns

* int: the unsigned decimal integer result
Input Format

The first line of the input contains g, the number of queries

Each of the next q lines contain an integer, n, to process.
Constraints

1<q <100
O<n<2”

3 
2147483647 
1 
0
Sample Output

2147483648 
4294967294 
4294967295
Explanation

Take 1 for example, as unsigned 32-bits is 00000000000000000000000000000001 and doing the flipping we get 11111111111111111111111111111110 which in turn is 4294967294.


```

## Solution
Incomplete
```

```

## random: Palindrome
```
// given a string check if it's a palindrome
fun palindromeChecker(word: String): Boolean {
    // case 1 empty string return false:
    if (word.isEmpty()) return false
    //  case 2 checking if the word is a palindrome
    var bIndex = word.length - 1
    var fIndex = 0
    while (fIndex != word.length - 1) {
        if (word[fIndex] != word[bIndex]) {
            return false
        }
        if (word.length % 2 == 0 && fIndex == word.length / 2) {
            return true
        } else if (fIndex == bIndex) {
            return true
        }
        fIndex++
        bIndex--
    }
    return false

}// given a string check if it's a palindrome
fun palindromeChecker2(word: String): Boolean {
    // case 1 empty string return false:
    if (word.isEmpty()) return false
    //  case 2 reverse the string and compare the 2
    var reversedString = ""
    for (index in word.length-1 downTo 0){
        reversedString += word[index]
    }
    println(reversedString)
    return word == reversedString
}
```

## random: Anagram
## O(2N)
```
// 2 strings, anagram words you can rearrange that makes it into another word
fun anagram(word1: String, word2: String): Boolean {
    if (word1.length != word2.length) return false
    val letterHashMap = HashMap<Char, Int>()
    // O(1)
    for (character in 'a'..'z') {
        letterHashMap[character] = 0
    }
    // O(n)
    for (index in word1.indices) {
        letterHashMap[word1[index].lowercaseChar()] = letterHashMap[word1[index].lowercaseChar()]!! + 1
    }
    // O(n)
    for (index in word2.indices) {
        letterHashMap[word2[index].lowercaseChar()] = letterHashMap[word2[index].lowercaseChar()]!! - 1
    }
    // O(1)
    for (character in 'a'..'z') {
        if (letterHashMap[character] != 0) {
            return false
        }
    }
    return true
}
```

## random: PhoneNumberPad
```
/ Given the phone dial pad attached below. Write a function that takes in a string of entered numbers
// and returns all possible corresponding text possibly meaning to enter as a list of strings.

// Example: Input “123”
// Output:  	[“ad”, “ae”, “af”, “bd”, “be”, “bf”, “cd”, “ce”, “cf”]
```
```
fun phoneNumberDial(numbers: String): List<String> {
    val phonePad = getPhonePadHashMap()
    var listOfCombinations = mutableListOf<String>()
    var lastCombinations = mutableListOf<String>()
    var currentPrimaryCombinationLetter = ""
    //base case length is 1
    if (numbers.length == 1) {
        return phonePad[numbers[0].toString()]!!
    }
    // length > 1
    for (character in phonePad[numbers[0].toString()]!!) { // check the character list of number 2 -> ["23"]
        currentPrimaryCombinationLetter += character // Add the first character in the list of number 2 -> A
        lastCombinations = phoneNumberDial(
            numbers.substring(
                1, numbers.length
            )
        ).toMutableList() // get the next number in the string
        for (character in lastCombinations) {
            listOfCombinations.add(currentPrimaryCombinationLetter + character)
        }
        lastCombinations.clear()
        currentPrimaryCombinationLetter = ""
    }
    return listOfCombinations
}

private fun getPhonePadHashMap(): HashMap<String, List<String>> = HashMap<String, List<String>>().apply {
    this.mapKeys {
        "0" to listOf("")
        "1" to listOf("")
        "2" to listOf("A", "B", "C")
        "3" to listOf("D", "E", "F")
        "4" to listOf("G", "H", "I")
        "5" to listOf("J", "K", "L")
        "6" to listOf("M", "N", "O")
        "7" to listOf("P", "Q", "R", "S")
        "8" to listOf("T", "U", "V")
        "9" to listOf("W", "Y", "X", "Z")
    }
}
```
