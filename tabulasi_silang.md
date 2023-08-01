# Tabulasi Silang Data Penyebab Kematian di Indonesia

### Instruksi

−Item1

function myFunction() {
var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
var dataRange = sheet.getDataRange();
var data = dataRange.getValues();

var headers = data.shift(); // Remove the header row

var typeIndex = headers.indexOf('Type');
var yearIndex = headers.indexOf('Year');
var deathsIndex = headers.indexOf('Total Deaths');

var crossTabData = {};
for (var i = 0; i < data.length; i++) {
var row = data[i];
var type = row[typeIndex];
var year = row[yearIndex];
var deaths = row[deathsIndex];

    if (!crossTabData[type]) {
      crossTabData[type] = {};
    }

    if (!crossTabData[type][year]) {
      crossTabData[type][year] = 0;
    }

    crossTabData[type][year] += deaths;

}

// Output the cross-tabulation to a new sheet
var outputSheet = SpreadsheetApp.getActiveSpreadsheet().insertSheet();
var outputData = [['Type', 'Year', 'Total Deaths']];
for (var type in crossTabData) {
for (var year in crossTabData[type]) {
outputData.push([type, parseInt(year), crossTabData[type][year]]);
}
}

outputSheet.getRange(1, 1, outputData.length, outputData[0].length).setValues(outputData);
outputSheet.activate();
}
