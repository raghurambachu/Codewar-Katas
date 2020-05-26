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