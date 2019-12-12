const inputDateString = 'March 21, 2018 08:02:00';
const formatErrorMessage = 'Input date must fit this format: March 21, 2018 7:02:00';

/*
 * function: formatNoteDate
 * arguments: dateStr - string like "March 21, 2018 12:02:00"
 * returns: string of date like "3/21/2018 12:02PM"
 */

// Brackets should be on the same line
// Need docblock for function signatures
function formatNoteDate(dateStr) {
  // Use es6 let/const
  // These variable names are not descriptive
  // There's no input validation
  // There's no error handling, so if the input isn't the right format, it'll just be an uncaught exception
  var notedt = new Date(dateStr);
  // This doesn't describe what it's trying to accomplish, which is to convert to 12 hour format
  var notehour = notedt.getHours() % 12;
  var notemins = notedt.getMinutes();

  // Use identity operator, not equality operator - or just !notehour
  if (notehour == 0) {
    // Lack of parentheses makes this confusing and a potential bug
    // No need to call the same function and do the same math twice
    if (notedt.getHours() / 12 == 1 || notedt.getHours() / 12 == 2) {
      notehour = 12;
    }
  }

  // Implicit type casting is not a good idea
  if (notemins < 10) {
    notemins = "0" + notemins;
  }

  // This string concatenation here is much too long
  // The same output could be achieved using ticks and interpolation
  // There's no reason to call the functions within the final value, they could be calculated before for readability
  // Again, implicit type conversion is going to lead to issues
  return (
    notedt.getMonth() +
    1 +
    "/" +
    notedt.getDate() +
    "/" +
    notedt.getFullYear() +
    " " +
    notehour +
    ":" +
    notemins +
    (notedt.getHours() >= 12 ? "PM" : "AM")
  );
  // Missing closing bracket which is going to throw a syntax error
}

/*
 * function: formatNoteDate
 * arguments: dateStr - string like "March 21, 2018 12:02:00"
 * returns: string of date like "3/21/2018 12:02PM"
 */

/**
 * Ensure that we have a string in the right format and a valid datetime
 * @param {String} inputDate
 */
function checkValidDate(inputDate) {
  // Make sure we have the right format
  if (!/\w+\s\d{1,2},\s\d{4}\s(\d{2}\:?){3}/) {
    throw new Error("");
  }
  // ...and a valid date
  if (isNaN(Date.parse(inputDate))) {
    throw new Error("Input date must be a valid datetime");
  }
}

/**
 * Format date
 * @param {String} dateInput Input date string
 */
function refactorNoLibrary(dateInput = null) {
  checkValidDate(dateInput);
  const inputDate = new Date(dateInput);
  let isPm = inputDate.getHours() > 12;
  // Get modulo remainder if PM
  let hour = inputDate.getHours() % 12;
  let minute = inputDate.getMinutes();
  // Differentiate noon and midnight
  if (!hour && [1, 2].includes(inputDate.getHours() / 12)) {
    hour = 12;
  }

  // If note minutes are less than ten, append a 0
  minute = minute < 10 ? `0${minute}` : minute;

  // Display AM or PM
  const amPm = isPm ? "PM" : "AM";

  const monthPlusOne = inputDate.getMonth() + 1;
  const notedDate = inputDate.getDate();
  const notedYear = inputDate.getFullYear();
  return `${monthPlusOne}/${notedDate}/${notedYear} ${hour}:${minute}${amPm}`;
}

/**
 * Just use a library and let that do the heavy lifting
 * @param {String} inputDateString 
 */
function refactorWithLibrary(inputDateString = "") {
  try {
    return require('date-fns/format')(new Date(inputDateString), 'M/d/yyyy hh:mmaaa');
  } catch (e) {
    console.log('****************INPUT DATETIME MUST BE VALID****************')
    console.log(formatErrorMessage);
    console.log(`Input value: ${inputDateString}`);
  }
}

const secondFormat = formatNoteDateRefactored(inputDateString);
console.log(`Second Format: ${secondFormat}`);
const thirdFormat = bestFormatDate(inputDateString);
console.log(`Third Format: ${thirdFormat}`);
