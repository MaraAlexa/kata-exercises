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
** Your task is to write a function which returns the sum of following series upto nth term(parameter).**
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
**
A function that takes in a string of letters from a to z  and outputs an error rate whose numerator is the number of errors and the denominator the length of the control string.**

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
