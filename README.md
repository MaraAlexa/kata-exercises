### 1. Filter Array by Another Array
*using filter and indexOf*
```javascript
function gooseFilter (birds) {

  var geese = ["African", "Roman", "Toulouse", "Pilgrim"];

  return birds.filter( bird => geese.indexOf(bird) === -1 );
};

gooseFilter(["Mallard", "Hook Bill", "African", "Crested", "Pilgrim", "Toulouse"]);

// returns ['Mallard', 'Hook Bill', 'Crested']
```
*using filter and includes*

```javascript
function gooseFilter (birds) {

  var geese = ["African", "Roman", "Toulouse", "Pilgrim"];

  return birds.filter(bird => !geese.includes(bird));
};

gooseFilter(["Mallard", "Hook Bill", "African", "Crested", "Pilgrim", "Toulouse"]);

// returns ['Mallard', 'Hook Bill', 'Crested']

```
### 2. Sum the first nth term of Series
**Your task is to write a function which returns the sum of following series upto nth term(parameter).**
```
SeriesSum(1) => 1 = "1"
SeriesSum(2) => 1 + 1/4 = "1.25"
SeriesSum(5) => 1 + 1/4 + 1/7 + 1/10 + 1/13 = "1.57"
```
```javascript
function SeriesSum(n) {
  var sum = 0;

  for (i=0; i<n; i++){
    sum += 1/(3*i+1);
    // 0 + 1/3*0+1 = 0+1=1
    // 1+ 1/3*1+1 = 1+1/4= 1.25
  }
  // make the sum with only 2 decimals
   sum = sum.toFixed(2);
}
```

### 3. Printer Errors
**A function that takes in a string of letters from a to z  and outputs an error rate whose numerator is the number of errors and the denominator the length of the control string.**

```
s="aaabbbbhaijjjm"
error_printer(s) => "0/14"

s="aaaxbbbbyyhwawiwjjjwwm"
error_printer(s) => "8/22"
```
*using for loop*
```javascript
function printerError(s) {
  // need a var to count the number of unmatched letters
  var count = 0;
  for(var i = 0; i < s.length; i++) {
    if (s[i] > "m") {
      count++;
    }
  }
  return count+"/"+s.length;
}
```
*using **.match(regex)** returns that regex expression every time that expression is found; **.match(regex).length** returns the count of how many regex has found*
```javascript
function printerError(s) {
    return s.match(/[^a-m]/g).length + "/" + s.length;
}
```
### 4. The Difference between 2 arrays (similar with #1)
**It should remove all values from list a, which are present in list b.**

*using .includes*
```javascript
function array_diff(a, b) {
  //returns all the elements from a that does NOT include elements from b
  return a.filter(el => !b.includes(el));
}
```
*using for loop and indexOf*
```javascript
function array_diff(a, b) {

  var arr = new Array(); // make a new array
    // loop through the first array(a)
    for(var i = 0; i<a.length; i++) {
      // if in b you DONT find any el from a, push a in the arr (=>b.indexOf(a[i]) = false)
        if(b.indexOf(a[i]) < 0) {
            arr.push(a[i]);
        }
    }

  return arr;
}
array_diff([1,2,2], [2]); // gives [1]
```
### 5. Count duplicates in a string
*using for loop*
```javascript
function duplicateCount(text){

  var count = 0;
  var used = [];// to put the duplicates in
  // make it lowercase, split it into individual letters to be able to sort it alphabetically and then join them back together in a single string
  var sortedStr = text.toLowerCase().split('').sort().join('');

  // loop through the sorted string to compare the current with next iterator;
  // don't push the letter that is already in the used array
  for(var i = 0; i < sortedStr.length; i++) {
    if (sortedStr[i] == sortedStr[i+1]  && sortedStr[i] != used) {
      used.push(sortedStr[i]);
      count++;
    }
  }
  return count;// or return used to see the duplicated letters
}
duplicateCount("abbbbccww")); // used = ["b","c","w"]; count = 3;
```
*using forEach*
```javascript
function duplicateCount(text) {
  var dup = [];
  text.toLowerCase().split('').forEach(function(v, i, arr) {if(i != arr.lastIndexOf(v) && dup.indexOf(v) == -1) dup.push(v);});
  return dup.length;
}
```
### 6. Simple change machine
*using switch*
```javascript
function changeMe(moneyIn){
  // Write your function here
  switch(moneyIn) {
  case '£5':
  var charge = Array(25).fill('20p');
  return charge.join(' ')

  case '£2':
  var charge = Array(10).fill('20p');
  return charge.join(' ')

  case '£1':
  var charge = Array(5).fill('20p');
  return charge.join(' ')

  case '50p':
  return '20p 20p 10p'

  case '20p':
  var charge = Array(2).fill('10p');
  return charge.join(' ')

  default:
   return moneyIn}
}

```
## Basic Algorithms
### 1.Reverse a string
```javascript
function reverseString(str) {
  //["h", "e", 'l','o','o'].reverse().join('')
  return Array.from(str).reverse().join('');
}

reverseString("hello");
```
### 2.Check for Palindromes
*A palindrome is a word or sentence that's spelled the same way both forward and backward, ignoring punctuation, case, and spacing.*
```javascript
function palindrome(str) {
  // make a var for all unwanted characters like space, comas,etc (RegExp)
 var re = /[\W_]/g;

  // lowercase and get rid of unwanted characters: =>"a man, an apple" = "amanaapple"
 var lowRegStr = str.toLowerCase().replace(re, '');

  // reverse the string (need an array of string to be able to reverse it)
 var reverseStr = lowRegStr.split('').reverse().join('');
  // compare the reverse str with the original
 return reverseStr === lowRegStr; //return true if it is a palindrome

}
palindrome("eye");
```
### 3. Return the length of the longest word in the provided sentence.
```javascript
function findLongestWord(str) {
  var longestWord = str.split(' '); // split into an array of string

  longestWord.sort(function(a, b){

    if ( b.length > a.length){
      return 1; // goes first
    } else {
      return -1;// stays behind
    }
  });
  // var longestWord = ["javascript", "ruby", "love", ...]

  return longestWord[0].length; // return the first item from the array

}

findLongestWord("I love javascript and ruby");
// get 10 -> the length of "javascript"
```
### 4. Title Case a Sentence (capitalize the first letter of each word. )
```javascript
function titleCase(str) {
  // make all characters lower case
  str = str.toLowerCase() // i'm alittle tea pot
  // split the sentence into an array of words
           .split(' ')
  // turn first letter of each word into upper case
           .map(function(word){
              return (word.charAt(0).toUpperCase() + word.slice(1));
    /*
    1st word: "i'm"    =>  "i'm".charAt(0).toUpperCase() + "i'm".slice(1);
                                "I"                     +     "'m";
                                                  return "I'm";

    3rd word: "a"      => "little".charAt(0).toUpperCase()   + "".slice(1);
                                "L"                     +     "ittle";
                                              return "Little";
    */
            });
  // return the output of each word together
  return str.join(' '); // ["I'm", "A", "Little", "Tea", "Pot"].join(' ') => "I'm A Little Tea Pot"

}

titleCase("I'm a little tea pot"); // 'I'm A Little Tea Pot'

```
## Kata Exercises
### Make a class in ES6 with proprieties, methods and static methods
```javascript
class Person {
  constructor(firstName, lastName, age, gender){
    // || 'John' used to give default values; in case you don't give it your own name
    this.firstName = firstName || "John";
    this.lastName = lastName || "Doe";
    this.age = age || 0;
    this.gender = gender || "Male";
  }

  sayFullName(){
    return `${ this.firstName } ${ this.lastName }`;
  }
  // with static you create methods that are ONLY available to the class Person; cannot be called on instances of the class
  static greetExtraTerrestrials(raceName){
    return `Welcome to Planet Earth ${ raceName }`;
  }
}

const myperson = new Person('mara', 'alexa', 28, 'Female');
Person.greetExtraTerrestrials('Martians');
```
### Check if a coupon code is valid and not expired
```javascript
function checkCoupon(enteredCode, correctCode, currentDate, expirationDate){

  currentDate = Date.parse(currentDate);
  expirationDate = Date.parse(expirationDate);

  if(currentDate <= expirationDate && enteredCode === correctCode){
    return true;
  } else{
    return false;
  }
}
checkCoupon('123','123','September 5, 2014','October 1, 2014'); // true
checkCoupon('123a','123','September 5, 2014','October 1, 2014'); // false
```
### Mumbling function
```
accum("abcd");    // "A-Bb-Ccc-Dddd"
accum("RqaEzty"); // "R-Qq-Aaa-Eeee-Zzzzz-Tttttt-Yyyyyyy"
accum("cwAt");    // "C-Ww-Aaa-Tttt"
```
```javascript
function accum(s) {
  var letters = s.split(''); // ["a","b",...]
  var str =[];

  for( var i= 0; i< letters.length; i++){
  	str.push(letters[i].toUpperCase() + letters[i].toLowerCase().repeat(i));
    // letters[i] = a b c d;
    // i = index of i = 0 1 2 3
    // loop1: a + a.repeat(0) => a
    // loop2: b + b.repeat(1) => bb
    //loop 3: c + c.repeat(2) => ccc; etc...
  }
  return str.join('-');
}
accum("abcd"); //"A-Bb-Ccc-Dddd"
```
### List Filtering to return only integers
*ES6*
```javascript
function filter_list(l) {
  return l.filter(item => typeof(item) == "number");
}
//filter_list([1,2,'aasf','1','123',123]) => get [1,2,123]
```
*ES5 - by checking against strings*
```javascript
function filter_list(l) {
  return l.filter(function(elem){
    return typeof elem != "string"
  } )
}
```
### Sum the last 2 lowest numbers in an Array
*using .sort()*
```javascript
function sumTwoSmallestNumbers(numbers) {  
  //sort the numbers from lowest to highest
  numbers = numbers.sort(function(a, b){return a - b; }); // [5,8,12,19,22]

  // return the sum of last two
  return numbers[0] + numbers[1]; // 5 + 8
};
console.log(sumTwoSmallestNumbers([5, 12, 8, 22, 19])); // 13
```
### Regex password validation
*in one line*
```javascript
function validate(password) {
//Minimum 6 characters at least 1 Uppercase Alphabet, 1 Lowercase Alphabet and 1 Number
  return /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{6,}$/.test(password);
}
```
*check for each condition*
```javascript
function validate(password) {
  return  /^[A-Za-z0-9]{6,}$/.test(password) && // min 6 alphanumerical characters
          /[A-Z]+/           .test(password) && // min 1 Upper case letter
          /[a-z]+/           .test(password) && // min 1 Lower case letter
          /[0-9]+/           .test(password) ;  // min 1 Number
}
```

### Selling tickets to people that have bills of 25, 50 and 100 dollars. The seller has no initial change. Check if he can give change to everyone in the line
```
tickets([25, 25, 50]) // => YES
tickets([25, 100])    
        // => NO. Vasya will not have enough money to give change to 100 dollars
```
```javascript
function tickets(peopleInLine){
   var m25 = 0, m50 = 0;

    for (var i = 0; i < peopleInLine.length; i++) {
        switch(peopleInLine[i]){
            case 25:
                m25++;
                break;
            case 50:
                m25 > 0 ? m25-- : m25 = -1;
                m50++;
                break;
            case 100:
                m25 > 0 && m50 > 0 ? m50-- : (m25 > 2 ? m25 -= 2 : m25 = -1);
                m25--;
                break;
        }
    }
    return m25 < 0 ? "NO" : "YES";
}
```
### Greet a person; make sure the input its not an empty string or null
*basic solution*
```javascript
function greet(name) {
  if(name === '' || name === null){
    return null;
  } else {
    return `hello ${name}!`
  }
}
```
*clever solution*
```javascript
function greet(name) {
  return name ? `hello ${name}!` : null;
}
```
### Square each digid of a number
```
Test.assertEquals(squareDigits(9119), 811181);
```
*using for loop*
```javascript
function squareDigits(num){
    // convert num to a String of numbers
    var string = num.toString(); // "9119"
    // make an empty array to put the results
    var results = [];

    //loop through the string of numbers
    for (var i = 0; i < string.length; i++){
        // convert each digid to its square: 9*9;  1*1; etc
        results[i] = string[i] * string[i];
    }
    // join the results and convert them to NUmber
    return Number(results.join(''));
};
```
### Find the missing integer from a sequence of numbers in a string
```javascript
function findMissingNumber(sequence){

 // split the string into an array of strings: ["1", "2", "3", "5"]
 // than covert it into an array of numbers
 var arr = sequence.split(' ').map(Number);// [1, 2, 3, 5]
   // covers invalid sequences
  if(sequence.length == 0){
    return 0; // if an empty str is given
  }
  else if(/[a-z]/ig.test(sequence) === true){ // if letters are given
    return 1;
  }

  // the SOLUTION once you have a valid sequence :[1, 2, 3, 5]
  for(var i = 1; i <= arr.length; i++){// iterator = 1 2 3 4
    if(arr.indexOf(i) === -1){// if indexOf(4) does not exist
     return i;// return 4
    }
  }
  // for the already complete sequence(or empty)
  return 0
}
//findMissingNumber("1 2 3 5") =>gives 4
//findMissingNumber("2 6 4 5 3") => gives 1
```
### Write Number in Extended form
```javascript
function expandedForm(num) {
  num = num.toString().split('');
  console.log(num);//  ["1", "2", "0", "6", "6"]

  num = num.map((num, index, arr) => num + "0".repeat(arr.length - index -1 ));// 0*(5-0-1)=0*4; 0*(5-1-1)=0*3
  console.log(num); //["10000", "2000", "000", "60", "6"]

  num = num.filter(a => a > 0);// filter out the "0 strings"
  console.log(num);//["10000", "2000", "60", "6"]

  num = num.join(" + ");
  console.log(num); // 10000 + 2000 + 60 + 6

}

console.log(expandedForm(12066));// 10000 + 2000 + 60 + 6

```
### Sort ascending odd numbers and leave even numbers at their position
```
example:
sortArray([5, 3, 2, 8, 1, 4]) == [1, 3, 2, 8, 5, 4]
```
```javascript
function sortArray(array) {
  // filter for the odd numbers and sort it (ascending)

  const odd = array.filter((x) => x % 2)
                   .sort((a,b) => a - b);
  console.log(odd);// [1, 3, 5]

  // for each x in the array, if x is even return  [1, 3, 5].shift(); else return x
  return array.map((x) => x % 2 ? odd.shift() : x);
   // 1) for 5(odd) return [1, 3, 5].shift() ->[1]
	// 2) for 3(odd)  return   [3, 5].shift() ->[3]
    // 3) for 2(even) return                2 ->[2]
    // 4) for 8(even) return                8 ->[8]
    // 5) for 1(odd)  return      [5].shift() ->[5]
    // 6) for 4(even) return                4 ->[4]
}

console.log(sortArray([5, 3, 2, 8, 1, 4])); //[1, 3, 2, 8, 5, 4]

```
### Convert regular english to LeetSpeak dialect
```
toLeetSpeak("LEET") returns "1337"
```
*using for look*
```javascript
function toLeetSpeak(str) {
  var letSpeak = {
  A : '@',
  B : '8',
  C : '(',
  D : 'D',
  E : '3',
  F : 'F',
  G : '6',
  H : '#',
  I : '!',
  J : 'J',
  K : 'K',
  L : '1',
  M : 'M',
  N : 'N',
  O : '0',
  P : 'P',
  Q : 'Q',
  R : 'R',
  S : '$',
  T : '7',
  U : 'U',
  V : 'V',
  W : 'W',
  X : 'X',
  Y : 'Y',
  Z : '2'
  }
  var newstr = ''; // empty string to put new characters
  // loop through a string
  for(var i= 0; i< str.length; i++){
    //console.log(letSpeak[str[i]]); // 1 3 3 7
    newstr += letSpeak[str[i]];
  }
  return newstr;
}

console.log(toLeetSpeak('CODEWARS')); // "(0D3W@R$"
```
*using replace*
```javascript
function toLeetSpeak(str) {
  const alphabet = {
  A : '@',
  B : '8',
  C : '(',
  D : 'D',
  E : '3',
  F : 'F',
  G : '6',
  H : '#',
  I : '!',
  J : 'J',
  K : 'K',
  L : '1',
  M : 'M',
  N : 'N',
  O : '0',
  P : 'P',
  Q : 'Q',
  R : 'R',
  S : '$',
  T : '7',
  U : 'U',
  V : 'V',
  W : 'W',
  X : 'X',
  Y : 'Y',
  Z : '2'
}
  return str.replace(/[A-Z]/g, char => alphabet[char]);
}
```
