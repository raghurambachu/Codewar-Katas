The Hashtag Generator
26th May 2020
```js
// " Hello there thanks for trying my Kata"  =>  "#HelloThereThanksForTryingMyKata"
// "    Hello     World   "                  =>  "#HelloWorld"
// ""                                        =>  false

// It must start with a hashtag (#).
// All words must have their first letter capitalized.
// If the final result is longer than 140 chars it must return false.
// If the input or the result is an empty string it must return false.
function generateHashtag(str) {
  if (!str.length) return false;
  let arrOfWords = [];
  str = str.trim().split(" ");

  let listOfWords = str.reduce(
    (listOfWords, sentenceItem) =>
      sentenceItem !== "" ? listOfWords.concat(sentenceItem) : listOfWords,
    []
  );
  let capitalisedListOfWords = listOfWords.map(
    (word) => word[0].toUpperCase() + word.slice(1)
  );
  let hashedStr = `#${capitalisedListOfWords.join("")}`;
  return hashedStr.length > 140 ? false : hashedStr;
}

//generateHashtag("    Hello     World   ")
console.log(generateHashtag(" Hello there thanks for trying my Kata"));
```



Convert PascalCase string into snake_case
```js
// Complete the function/method so that it takes CamelCase string and returns the string in snake_case notation. Lowercase characters can be numbers. If method gets number, it should return string.

// Examples:

// //  returns test_controller
// toUnderscore('TestController');

// // returns movies_and_books
// toUnderscore('MoviesAndBooks');

// // returns app7_test
// toUnderscore('App7Test');

// // returns "1"
// toUnderscore(1);

function toUnderscore(string) {
  if (!isNaN(string)) return `${string}`;
  let wordsArray = [];
  let posOfCapitals = string
    .split("")
    .reduce(
      (posOfCapitals, letter, index) =>
        letter.charCodeAt() < 97 && letter.charCodeAt() > 64
          ? posOfCapitals.concat(index)
          : posOfCapitals,
      []
    );
  let i = 0;
  for (; i <= posOfCapitals.length - 2; i++) {
    wordsArray.push(string.slice(posOfCapitals[i], posOfCapitals[i + 1]));
  }
  wordsArray.push(string.slice(posOfCapitals[i]));
  return wordsArray.map((word) => word.toLowerCase()).join("_");
}

//console.log(toUnderscore("TestController"))
//console.log(toUnderscore('MoviesAndBooks'))
console.log(toUnderscore("App7Test"));
```


29th May 2020
Strings, Numbers and Calculation
```js
function calculateString(st) {
  let operations = ["*", "+", "-", "/"];
  let storeOperator,result;
  let getOperation = operations.forEach((operator, index) => {
    if (st.includes(operator)) storeOperator = operator;
  });
  st = st.split(storeOperator);
  let numbers = st.map((part,index) => part.split("").reduce((num,char) => !isNaN(char) || char === "."? num + char : num,"")).map(num => +num);
  switch(storeOperator){
    case "+":
      result = numbers[0] + numbers[1];
      break;
    case "-":
      result = numbers[0] - numbers[1];
      break;
    case "*":
      result = numbers[0] * numbers[1];
      break;
    case "/":
      result = numbers[0] / numbers[1];
      break;
  }
  return `${Math.round(result)}`;
}
//console.log(calculateString("gdfgdf234dg54gf*23oP42"));
console.log(calculateString(";$%§fsdfsd235??df/sdfgf5gh.000kk0000"));

// Input: "gdfgdf234dg54gf*23oP42"
// Output: "54929268" (because 23454*2342=54929268)
```


30th May 2020
Pair of Gloves
```js
let myGloves = [
  "Fuchsia",
  "Maroon",
  "Navy",
  "Purple",
  "Fuchsia",
  "Gray",
  "Teal",
  "White",
  "White",
];
function numberOfPairs(gloves) {
  return (
    Object.entries(
      gloves.reduce((obj, glove) => {
        if (glove in obj) obj[glove] = ++obj[glove];
        else obj[glove] = 1;
        return obj;
      }, {})
    ).reduce(
      (total, [color, count]) =>
        count % 2 === 0 ? total + count : total + count - 1,
      0
    ) / 2
  );
}

console.log(numberOfPairs(myGloves));
```


31st May 2020
Search For Letters
```js
// Create a function which accepts one arbitrary string as an argument, and return a string of length 26.

// The objective is to set each of the 26 characters of the output string to either '1' or '0' based on the fact whether the Nth letter of the alphabet is present in the input (independent of its case).

// So if an 'a' or an 'A' appears anywhere in the input string (any number of times), set the first character of the output string to '1', otherwise to '0'. if 'b' or 'B' appears in the string, set the second character to '1', and so on for the rest of the alphabet.

// For instance:

// "a   **&  cZ"  =>  "10100000000000000000000001"
function change(string) {
  let alphabet = "abcdefghijklmnopqrstuvwxyz";
  let bits = Array.from({ length: 26 }, () => 0);
  string = string
    .toLowerCase()
    .match(/[a-z]*/g)
    .join("");
  string.split("").forEach((char) => {
    if (alphabet.includes(char)) bits[alphabet.indexOf(char)] = 1;
  });
  return bits.join("");
}

console.log(change("Abc e  $$  z!!a$%&RgTT"));

```

4th June 2020
Meeting
```js
// John has invited some friends. His list is:
// Could you make a program that

// makes this string uppercase
// gives it sorted in alphabetical order by last name.
// When the last names are the same, sort them by first name. Last name and first name of a guest come in the result between parentheses separated by a comma.
// "(CORWILL, ALFRED)(CORWILL, FRED)(CORWILL, RAPHAEL)(CORWILL, WILFRED)(TORNBULL, BARNEY)(TORNBULL, BETTY)(TORNBULL, BJON)"

function meeting(str) {
  str = str
    .split(";")
    .map((name) => name.split(":"))
    .map(([first, last]) =>
      [last.toUpperCase(), first.toUpperCase()].join(", ")
    )
    .sort()
    .map((name) => `(${name})`)
    .join("");
  return str;
}

str =
  "Fred:Corwill;Wilfred:Corwill;Barney:Tornbull;Betty:Tornbull;Bjon:Tornbull;Raphael:Corwill;Alfred:Corwill";

console.log(meeting(str));
```

5th June 2020
Divisible Ints
```js
// You are given an integer N. Your job is to figure out how many substrings inside of N divide evenly with N.

function getCount(n) {
  strN = `${n}`;
  let count = 0;
  let possibleDivisors = [];
  for (let i = 0; i < strN.length; i++) {
    for (let j = 1; j <= strN.length; j++) {
      possibleDivisors.push(strN.slice(i, j));
    }
  }
  possibleDivisors = possibleDivisors
    .filter((digits) => digits != "")
    .map((digit) => +digit)
    .sort((a, b) => a - b);
  possibleDivisors = possibleDivisors.slice(0, possibleDivisors.length - 1);
  for (let i = 0; i < possibleDivisors.length; i++) {
    if (n % possibleDivisors[i] === 0) count++;
  }
  return count;
}

console.log(getCount(1230));
```


6th June 2020
Permute Palindrome
```js
// Write a function that will check whether the permutation of an input string is a palindrome. Bonus points for a solution that is efficient and/or that uses only built-in language functions. Deem yourself brilliant if you can come up with a version that does not use any function whatsoever.

function permutePalindrome(str) {
  const list = str
    .split("")
    .sort()
    .reduce((list, char) => {
      if (char in list) {
        list[char] = ++list[char];
      } else {
        list[char] = 1;
      }
      return list;
    }, {});
  let counter = 0;
  for (let [key, value] of Object.entries(list)) {
    if (value % 2 === 0) delete list[key];
    else {
      counter++;
      if (counter > 1) break;
      delete list[key];
    }
  }
  return Object.keys(list).length === 0 ? true : false;
}


console.log(permutePalindrome("racecar"));
console.log(permutePalindrome("kayak"));
console.log(permutePalindrome("something"));

// Example
// madam -> True
// adamm -> True
// junk -> False

// Hint
// The brute force approach would be to generate all the permutations of the string and check each one of them whether it is a palindrome. However, an optimized approach will not require this at all.

```

11th June 2020
Happy Numbers
```js
// Math geeks and computer nerds love to anthropomorphize numbers and assign emotions and personalities to them. Thus there is defined the concept of a "happy" number. A happy number is defined as an integer in which the following sequence ends with the number 1.

// Start with the number itself.
// Calculate the sum of the square of each individual digit.
// If the sum is equal to 1, then the number is happy. If the sum is not equal to 1, then repeat steps 1 and 2. A number is considered unhappy once the same number occurs multiple times in a sequence because this means there is a loop and it will never reach 1.
// For example, the number 7 is a "happy" number:

// 72 = 49 --> 42 + 92 = 97 --> 92 + 72 = 130 --> 12 + 32 + 02 = 10 --> 12 + 02 = 1

// Once the sequence reaches the number 1, it will stay there forever since 12 = 1

// On the other hand, the number 6 is not a happy number as the sequence that is generated is the following: 6, 36, 45, 41, 17, 50, 25, 29, 85, 89, 145, 42, 20, 4, 16, 37, 58, 89

// Once the same number occurs twice in the sequence, the sequence is guaranteed to go on infinitely, never hitting the number 1, since it repeat this cycle.

// Your task is to write a program which will print a list of all happy numbers between 1 and x (both inclusive), where:

function happyNumbers(x) {
  let happyNums = [];
  for (let i = 2; i <= x; i++) {
    if (checkHappyNumber(i)) happyNums.push(i);
  }
  return happyNums;
}

function checkHappyNumber(i) {
  let arrSum = [];
  let num = `${i}`;
  let isHappyNumber = true;
  while (+num !== 1) {
    num = `${num
      .split("")
      .reduce((sum, digit) => sum + Math.pow(+digit, 2), 0)}`;
    if (!arrSum.includes(num)) {
      arrSum.push(num);
    } else {
      isHappyNumber = false;
      break;
    }
  }
  return isHappyNumber;
}

console.log(happyNumbers(74));
```