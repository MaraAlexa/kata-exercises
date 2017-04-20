### Filter Array by Another Array
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

  return birds.filter(b => !geese.includes(b));
};

  gooseFilter(["Mallard", "Hook Bill", "African", "Crested", "Pilgrim", "Toulouse"]);

// returns ['Mallard', 'Hook Bill', 'Crested']

```
