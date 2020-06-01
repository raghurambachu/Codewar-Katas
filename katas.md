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