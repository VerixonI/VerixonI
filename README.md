SQL Basics: Simple NULL handling

DESCRIPTION:

For this challenge you need to create a SELECT statement, this statement must have NULL handling, using COALESCE and NULLIF.

If name is an empty string, you must replace with '[product name not found]'.

If card_name is an empty string, you must replace with '[card name not found]'.

If no price is specified (i.e. price is NULL), or if the price is 50 or less, you must discard the row.

eusales table schema
id
name
price
card_name
card_number
transaction_date
resultant table schema
id
name
price (greater than 50.00)
card_name
card_number
transaction_date
NOTE: Your solution should use pure SQL. Ruby is used within the test cases to do the actual testing.

SQL:

SELECT 
    id,
    COALESCE(NULLIF(name, ''), '[product name not found]') AS name,
    price,
    COALESCE(NULLIF(card_name, ''), '[card name not found]') AS card_name,
    card_number,
    transaction_date
FROM 
    eusales
WHERE 
    price IS NOT NULL 
    AND price > 50.00;
______________________________________________________________________________________________________________________________________________________________________

Simple Fun #74: Growing Plant

DESCRIPTION:
Task
Each day a plant is growing by upSpeed meters. Each night that plant's height decreases by downSpeed meters due to the lack of sun heat. Initially, plant is 0 meters tall. We plant the seed at the beginning of a day. We want to know when the height of the plant will reach a certain level.

SQL:

SELECT 
    growing_plant.id,
    CAST(
        CASE 
            WHEN up_speed >= desired_height THEN 1
            ELSE CEIL((desired_height - up_speed) * 1.0 / (up_speed - down_speed)) + 1
        END AS INT
    ) AS num_days
FROM 
    growing_plant
ORDER BY 
    growing_plant.id;

______________________________________________________________________________________________________________________________________________________________________

Sum of Digits / Digital Root

DESCRIPTION:
Digital root is the recursive sum of all the digits in a number.

Given n, take the sum of the digits of n. If that value has more than one digit, continue reducing in this way until a single-digit number is produced. The input will be a non-negative integer.

JavaScript:

function digitalRoot(n) {
    let numStr = n.toString();
    if (numStr.length === 1) {
        return parseInt(numStr);
    }
    let sum = 0;
    for (let digit of numStr) {
        sum += parseInt(digit);
    }
    return digitalRoot(sum);
}
console.log(digitalRoot(16));    
console.log(digitalRoot(942));   
console.log(digitalRoot(132189));  
console.log(digitalRoot(493193));  



______________________________________________________________________________________________________________________________________________________________________

Your order, please

DESCRIPTION:
Your task is to sort a given string. Each word in the string will contain a single number. This number is the position the word should have in the result.

Note: Numbers can be from 1 to 9. So 1 will be the first word (not 0).

If the input string is empty, return an empty string. The words in the input String will only contain valid consecutive numbers.

JavaScript:

function order(words) {
  if (words === "") return "";
  const wordArray = words.split(' ');
  const sortedWords = [];
  for (let i = 1; i <= 9; i++) {
    for (let j = 0; j < wordArray.length; j++) {
      if (wordArray[j].includes(i)) {
        sortedWords.push(wordArray[j]);
      }
    }
  }

  return sortedWords.join(' ');
}
console.log(order("is2 Thi1s T4est 3a"));
console.log(order("4of Fo1r pe6ople g3ood th5e the2"));
console.log(order(""));



______________________________________________________________________________________________________________________________________________________________________

Exes and Ohs

DESCRIPTION:
Check to see if a string has the same amount of 'x's and 'o's. The method must return a boolean and be case insensitive. The string can contain any char.

JavaScript:

function XO(str) {
  const lowerStr = str.toLowerCase();
  let countX = 0;
  let countO = 0;
  for (let char of lowerStr) {
    if (char === 'x') {
      countX++;
    } else if (char === 'o') {
      countO++;
    }
  }
  return countX === countO;
}
console.log(XO("ooxx"));
console.log(XO("xooxx"));
console.log(XO("ooxXm"));
console.log(XO("zpzpzpp"));
console.log(XO("zzoo"));


______________________________________________________________________________________________________________________________________________________________________

Two to One

DESCRIPTION:
Take 2 strings s1 and s2 including only letters from a to z. Return a new sorted string, the longest possible, containing distinct letters - each taken only once - coming from s1 or s2.

JavaScript:

function longest(s1, s2) {
  const combinedArray = Array.from(new Set(s1 + s2));
  const sortedArray = combinedArray.sort();
  return sortedArray.join('');
}
const a = "xyaabbbccccdefww";
const b = "xxxxyyyyabklmopq";
console.log(longest(a, b));
const c = "abcdefghijklmnopqrstuvwxyz";
console.log(longest(c, c));



_____________________________________________________________________________________________________________________________________________________________________

Stop gninnipS My sdroW!

DESCRIPTION:
Write a function that takes in a string of one or more words, and returns the same string, but with all words that have five or more letters reversed (Just like the name of this Kata). Strings passed in will consist of only letters and spaces. Spaces will be included only when more than one word is present.

C++:

#include <string>
#include <sstream>

using namespace std;

string spinWords(const string &sentence) {
    stringstream resultStream(sentence);
    stringstream finalResult;
    string word;
    bool first = true;
    while (resultStream >> word) {
        if (word.length() >= 5) {
            reverse(word.begin(), word.end());
        }
        if (!first) {
            finalResult << " ";
        }
        first = false;
        finalResult << word;
    }
    return finalResult.str();
}


_____________________________________________________________________________________________________________________________________________________________________

Persistent Bugger.

DESCRIPTION:
Write a function, persistence, that takes in a positive parameter num and returns its multiplicative persistence, which is the number of times you must multiply the digits in num until you reach a single digit.

JavaScript:

function persistence(num) {
    let count = 0;
    while (num >= 10) {
        const digits = num.toString().split('');
        num = digits.reduce((accumulator, currentValue) => accumulator * currentValue, 1);
        count++;
    }
    return count;
}
console.log(persistence(39));
console.log(persistence(999)); 
console.log(persistence(4));


_____________________________________________________________________________________________________________________________________________________________________

Scramblies

DESCRIPTION:
Complete the function scramble(str1, str2) that returns true if a portion of str1 characters can be rearranged to match str2, otherwise returns false.

JavaScript:

function scramble(str1, str2) {
    const charCount1 = {};
    const charCount2 = {};
    for (let char of str1) {
        charCount1[char] = (charCount1[char] || 0) + 1;
    }
    for (let char of str2) {
        charCount2[char] = (charCount2[char] || 0) + 1;
    }
    for (let char in charCount2) {
        if (!charCount1[char] || charCount1[char] < charCount2[char]) {
            return false;
        }
    }
    
    return true;
}
console.log(scramble('rkqodlw', 'world'));
console.log(scramble('cedewaraaossoqqyt', 'codewars'));
console.log(scramble('katas', 'steak')); 


_____________________________________________________________________________________________________________________________________________________________________

Write Number in Expanded Form

DESCRIPTION:
Write Number in Expanded Form
You will be given a number and you will need to return it as a string in Expanded Form.

JavaScript:

function expandedForm(num) {
    const numStr = num.toString();
    const expanded = [];
    for (let i = 0; i < numStr.length; i++) {
        if (numStr[i] !== '0') {
            const zeros = '0'.repeat(numStr.length - i - 1);
            expanded.push(numStr[i] + zeros);
        }
    }
    return expanded.join(' + ');
}
console.log(expandedForm(12));
console.log(expandedForm(42));
console.log(expandedForm(70304));













