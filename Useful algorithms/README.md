# Generate array of days in month with 35 positions filling the days before first and last days of month passing year and month as a params
`````
const getArrayOfDaysInMonth = (year, month) => {
  var numDaysInMonth, daysInWeek, daysIndex, index, day, daysArray;

  numDaysInMonth = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
  daysInWeek = ["Dom", "Seg", "Ter", "Qua", "Qui", "Sex", "Sáb"];
  daysIndex = { Sun: 0, Mon: 1, Tue: 2, Wed: 3, Thu: 4, Fri: 5, Sat: 6 };
  index = daysIndex[new Date(year, month - 1, 1).toString().split(" ")[0]];
  daysArray = [];

  for (day = 1; day <= numDaysInMonth[month - 1]; day++) {

    if (day === 1) {
      const end = daysInWeek.findIndex(d => d === daysInWeek[index]);
      
      for (let weekIndex = end - 1; weekIndex >= 0; weekIndex--) {
        const beforeMonthDaysCount = numDaysInMonth[month - 2];
        daysArray.push(beforeMonthDaysCount - weekIndex);
      }

      daysArray.push(day);
    } else if (day === numDaysInMonth[month - 1]) {
      daysArray.push(day);
      
      const start = daysInWeek.findIndex(d => d === daysInWeek[index]);
      
      for (let weekIndex = 1; weekIndex <= 7 - start; weekIndex++) {
        daysArray.push(weekIndex);
      }
    } else {
      daysArray.push(day);
    }

    index++;
    if (index == 7) index = 0;
  }
  
  return daysArray;
};

console.log(getArrayOfDaysInMonth(2021,4));
`````
