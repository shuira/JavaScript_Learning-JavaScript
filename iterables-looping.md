# Iterables and looping

### The for loop

Original syntax is not good enough

  ```javascript
  const cuts = ['Chuck', 'Brisket', 'Shank', 'Short Rib'];
  for (let i = 0; i < cuts.length; i++) {
    console.log(cuts[i]); // => Chuck, Brisket, Shank, Short Rib
  }
  ```

array.forEach() can't abort or skip the loop -> break or continue dosen't work

  ```javascript
  cuts.forEach((cut) => {
    console.log(cut);
    if(cut === 'Brisket') {
      continue; // doesn't work
    }
  })
  ```

for...in loop iterates all enumerable properties of an object, including methods or properties added to the prototype

```javascript
Array.prototype.shuffle = function(){
  //...
}
cuts.shop = 'MM MEats';
for (const index in cuts) {
  console.log(cuts[index]); // => Chuck, Brisket, Shank, Short Rib, MM MEats, function(){...}
}
```

:fire: for...of syntax is specific to *collections*

```javascript
for (const cut of cuts) {
  if(const cut === 'Brisket') {
    continue;
  }
  console.log(cut);
}
```

### More about for-of

Want to get the index in for...of? We can destructuring every returning **cuts.entries()**

```javascript
for (const [index, cut] of cuts.entries()) {
    console.log(`${index + 1}: ${cut}`);
}
```

Using Object.entries() to destructure every key-value pair
  
```javascript
const apple = {
  color: 'Red',
  size: 'Medium',
  weight: 50,
  sugar: 10
};

for (const [key, value] of Object.entries(apple)) {
  console.log(key + ': ' + value); // "color: Red", "size: Medium"...
}
```

:fire: You can use for-of with any data even though that isn't an array, **as long as it is iterable**, like **DOM collection(Nodelist)**, **arguments**, **string**, **array**, **generator**, **map**, **set**, etc. However you can turn those arrayish data into a true array using Array.from() and then applied those built-in methods

```javascript
//for-of arguments
function addUpNumbers() {
  let total = 0;
  for (const num of arguments) {
    total += num;
  }
  return total;
}
addUpNumbers(1,2,3); // -> 6

//for-of string
const name = 'Wes Bos';
for (const char of name) {
  console.log(char); // 'W' 'e' 's' ' ' 'B' 'o' 's'
}

//for-of DOM collection
const ps = document.querySelectorAll('p');
for (const paragraph of ps) {
  paragraph.addEventListener('click', function() {
    console.log(this.textContent);
  });
}
```
