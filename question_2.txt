const begin = process.argv[2] || 1;
const end = process.argv[3] || 10000;
const targetValues = [1, 89];
let totalFound = 0;

/**
 * Square the array of numbers created by splitting the input number and determine if they sum the value we're looking for
 * @param {number[]} strNumArr Array of numbers to be combined and run recursively
 */
function squareParts(strNumArr) {
  const squareResult = strNumArr
    .map(i => i * i)
    .reduce((prev, next) => {
      return prev + next;
    }, 0);
  // Found target value
  if (targetValues.includes(squareResult)) {
    if (squareResult == 89) {
      totalFound = totalFound + 1;
    }
  } else {
    squareParts(splitNumber(squareResult));
  }
}

/**
 * Split the number into the component pieces
 * @param {number} beginInt Beginning integer
 */
function splitNumber(beginInt) {
  return beginInt
    .toString()
    .split("")
    .map(i => parseInt(i, 10));
}

/**
 * Examine a range of numbers and see if they match the values we're looking for
 * @param {number} beginInt Beginning integer
 * @param {number} endInt End integer
 */
function findTargetInRange(beginInt = begin, endInt = end) {
  for (let i = beginInt; i < endInt; i++) {
    // Split the number into component pieces and combine squares recursively
    squareParts(splitNumber(i));
  }
}

findTargetInRange(begin);
console.log("****************TOTAL****************");
console.log(totalFound);
