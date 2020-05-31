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