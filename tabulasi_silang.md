#### Dharu Aulia Rahman_2100016086
# Tabulasi Silang Data Penyebab Kematian di Indonesia

## Instruksi A
1. Buka data berikut: [Data Kematian di Indonesia](https://www.kaggle.com/datasets/hendratno/cause-of-death-in-indonesia) menggunakan Google Spreadsheet
2. Pada Menu Bar pilih Ekstensi kemudian pilih App Script
3. Masukkan Kode Script berikut kedalam App Script:

```
function onOpen() {
  SpreadsheetApp.getUi()
    .createMenu('Custom Menu')
    .addItem('Generate Crosstab', 'generateCrosstab')
    .addToUi();
}

function generateCrosstab() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var dataRange = sheet.getDataRange();
  var data = dataRange.getValues();

  var crosstabData = {}; // Object to store the crosstab data
  var years = []; // Array to store unique years
  var types = []; // Array to store unique types

  // Loop through the data and calculate total deaths for each cause, type, and year
  for (var i = 1; i < data.length; i++) {
    var cause = data[i][0];
    var type = data[i][1];
    var year = data[i][2];
    var totalDeaths = data[i][4];

    if (!crosstabData[cause]) {
      crosstabData[cause] = {};
    }

    if (!crosstabData[cause][type]) {
      crosstabData[cause][type] = {};
    }

    if (!crosstabData[cause][type][year]) {
      crosstabData[cause][type][year] = 0;
    }

    crosstabData[cause][type][year] += totalDeaths;

    // Add the year and type to the respective arrays if they're not already there
    if (!years.includes(year)) {
      years.push(year);
    }

    if (!types.includes(type)) {
      types.push(type);
    }
  }

  // Sort the years and types in ascending order
  years.sort();
  types.sort();

  // Create a new sheet for crosstab data
  var newSheet = SpreadsheetApp.getActiveSpreadsheet().insertSheet();
  newSheet.setName('Crosstab Data');

  // Write column headers in the new sheet
  var headerRow = ['Cause', 'Type'].concat(years);
  newSheet.getRange(1, 1, 1, headerRow.length).setValues([headerRow]);

  // Write crosstab data in the new sheet
  var outputData = [];
  for (var cause in crosstabData) {
    for (var type in crosstabData[cause]) {
      var rowData = [cause, type];
      for (var i = 0; i < years.length; i++) {
        var year = years[i];
        var totalDeaths = crosstabData[cause][type][year] || 0;
        rowData.push(totalDeaths);
      }
      outputData.push(rowData);
    }
  }
  newSheet.getRange(2, 1, outputData.length, headerRow.length).setValues(outputData);

  // Auto-resize columns to fit the content
  newSheet.autoResizeColumns(1, headerRow.length);
}
```

4. Klik Jalankan kemudian tunggu hingga Proses selesai
5. Lakukan pengecekan hasil Tabulasi Silang pada Google Spreadsheet
6. Hasil Tabulasi Silang akan Berada di Sheet baru

### Table A

| Cause                                                                                                                         | Type                          | 2000 | 2001 | 2002 | 2003 | 2004   | 2005  | 2006  | 2007  | 2008  | 2009  | 2010  | 2011 | 2012 | 2013 | 2014 | 2015 | 2016 | 2017 | 2018 | 2019  | 2020  | 2021   | 2022  |
| ----------------------------------------------------------------------------------------------------------------------------- | ----------------------------- | ---- | ---- | ---- | ---- | ------ | ----- | ----- | ----- | ----- | ----- | ----- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ----- | ----- | ------ | ----- |
| Abrasi Air Laut                                                                                                               | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| AIDS                                                                                                                          | Bencana Non Alam dan Penyakit | 47   | 99   | 100  | 1305 | 1805   | 3469  | 3330  | 2780  | 3690  | 1299  | 1672  | 597  | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 614   | 665   | 688    | 0     |
| Aksi Teror dan Sabotase                                                                                                       | Bencana Sosial                | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 13   | 0    | 18   | 3     | 4     | 4      | 0     |
| Angin kencang                                                                                                                 | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 3     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Angin Puting Beliung                                                                                                          | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 13    | 0     | 0     | 0    | 0    | 0    | 0    | 37   | 20   | 0    | 10   | 4     | 12    | 4      | 0     |
| Angin Siklon Tropis                                                                                                           | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 10    | 4    | 23   | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Angin siklon tropis (angin kencang dan angin puting beliung)                                                                  | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 4     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Angin Topan                                                                                                                   | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Angin Topan / Angin Puting Beliung / Angin Puyuh                                                                              | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 9     | 10    | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Antraks                                                                                                                       | Bencana Non Alam dan Penyakit | 0    | 2    | 16   | 4    | 16     | 2     | 3     | 15    | 0     | 14    | 7     | 3    | 0    | 7    | 12   | 0    | 0    | 2    | 0    | 0     | 0     | 0      | 0     |
| Avian Influenza (Flu Burung)                                                                                                  | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 156   | 540   | 407   | 200   | 159   | 59    | 69   | 57   | 18   | 10   | 8    | 0    | 2    | 0    | 0     | 0     | 0      | 0     |
| Banjir                                                                                                                        | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 2     | 108   | 140   | 58    | 30    | 33    | 14   | 9    | 0    | 0    | 35   | 42   | 6    | 26   | 43    | 88    | 124    | 0     |
| Banjir Bandang                                                                                                                | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 251   | 0     | 42    | 127   | 215   | 55   | 38   | 0    | 0    | 20   | 81   | 23   | 18   | 109   | 49    | 120    | 0     |
| Banjir Bandang dan Angin Siklon Tropis                                                                                        | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Banjir Bandang dan Tanah Longsor                                                                                              | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 2     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Banjir dan Tanah Longsor                                                                                                      | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 265   | 0     | 0     | 0     | 3    | 20   | 0    | 0    | 2    | 11   | 49   | 43   | 98    | 67    | 106    | 0     |
| Banjir disertai Tanah Longsor                                                                                                 | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 17    | 4     | 19    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Banjir Lahar Dingin                                                                                                           | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 6    | 6    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Batuk Rejan                                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 4      | 0     | 1     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Bencana kelaparan                                                                                                             | Bencana Sosial                | 0    | 0    | 0    | 0    | 0      | 0     | 1     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Campak                                                                                                                        | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 9     | 0     | 1     | 0     | 7     | 9    | 4    | 2    | 8    | 1    | 0    | 1    | 0    | 0     | 0     | 0      | 0     |
| Cedera intrakranial                                                                                                           | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 2554   | 3021  | 5038  | 0     | 0     | 0     | 2050  | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Cedera lahir                                                                                                                  | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 23     | 51    | 57    | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Cedera YDT lainnya YTT dan daerah badan Multipel                                                                              | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 1210  | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Cedera, Keracunan, dan Akibat Sebab Luar Tertentu Lainnya                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 5331  | 9540  | 5945  | 11534 | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Cikungunya                                                                                                                    | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| COVID-19                                                                                                                      | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 22138 | 121956 | 12876 |
| Demam Berdarah Dengue (DBD)                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 5710  | 4797  | 2374  | 3738  | 2008  | 597  | 816  | 871  | 907  | 1071 | 1598 | 493  | 467  | 919   | 747   | 1410   | 0     |
| Demam Tifoid dan Paratifoid                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 2619   | 0     | 0     | 0     | 0     | 1013  | 548   | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Demam yang Sebabnya Tidak Diketahui                                                                                           | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 462   | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Diabetes melitus YTT                                                                                                          | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 2086  | 4768  | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Diare                                                                                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 94   | 128  | 53     | 0     | 326   | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Diare & gastroenteritis Oleh penyebab infeksi tertentu (kolitis infeksi)                                                      | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 3941   | 0     | 5432  | 0     | 0     | 1747  | 2578  | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Difteri                                                                                                                       | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 1     | 1     | 11    | 0     | 0     | 24    | 38   | 76   | 39   | 16   | 5    | 24   | 44   | 29   | 23    | 13    | 50     | 0     |
| Dispepsia                                                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 520   | 332   | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Eklamsia dan preeklamsia                                                                                                      | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 145    | 197   | 166   | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Erupsi Gunung Api                                                                                                             | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Faktor yg Mempengaruhi Keadaan Kesehatan & yg Berhubungan dengan Pelayanan Kesehatan                                          | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 796   | 1850  | 0     | 1627  | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Gagal ginjal lainnya                                                                                                          | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 3047  | 5042  | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Gagal Teknologi                                                                                                               | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 23   | 20   | 0    | 5    | 1     | 1     | 7      | 0     |
| Gangguan Mental & Perilaku                                                                                                    | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 164   | 454   | 0     | 204   | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Gangguan saluran napas lainnya yang berhubungan dengan masa perinatal                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 548    | 724   | 662   | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Gastritis dan Duodenitis                                                                                                      | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 235   | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Gejala, Tanda & Penemuan Laboratorium, Klinik Abnormal YTK                                                                    | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 3264  | 6592  | 3967  | 8476  | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Gelombang Besar                                                                                                               | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 3    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Gelombang Besar dan Angin Siklon Tropis                                                                                       | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 1    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Gelombang Pasang                                                                                                              | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 5     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Gelombang Pasang/Badai                                                                                                        | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 4    | 0    | 0    | 0     | 0     | 7      | 0     |
| Gempa & Tsunami                                                                                                               | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 509   | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Gempa Bumi                                                                                                                    | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 1801  | 6469  | 99    | 14    | 1209  | 7     | 1    | 13   | 0    | 0    | 2    | 107  | 4    | 573  | 64    | 0     | 121    | 0     |
| Gempa Bumi dan Tsunami                                                                                                        | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 2615 | 0     | 0     | 0      | 0     |
| Gizi Buruk                                                                                                                    | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 293   | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Hepatitis A                                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Hepatitis B                                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 5     | 7     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Hepatitis Klinis                                                                                                              | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 7      | 8     | 5     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Hipertensi Esensial (Primer)                                                                                                  | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 935   | 1910  | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Hipoksia intrauterus dan asfiksia lahir                                                                                       | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 1297   | 1876  | 1792  | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Infeksi khusus lainnya pada masa perinatal                                                                                    | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 137    | 138   | 117   | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Infeksi Saluran Napas Bagian Atas Akut Lainnya                                                                                | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 5532   | 0     | 0     | 0     | 0     | 162   | 1178  | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Janin dan bayi baru lahir yang dipengaruhi oleh faktor dan penyulit kehamilan persalinan dan kelahiran                        | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 362    | 461   | 548   | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kebakaran                                                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 2     | 29    | 0    | 88   | 0    | 0    | 62   | 42   | 1    | 15   | 3     | 6     | 42     | 0     |
| Kebakaran (Pemukiman)                                                                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 6    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kebakaran Hutan dan Lahan                                                                                                     | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 22   | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kebakaran Hutan dan Lahan                                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kecelakaan Industri                                                                                                           | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 11    | 33    | 8     | 0    | 0    | 0    | 0    | 0    | 1    | 0    | 22   | 0     | 0     | 1      | 0     |
| Kecelakaan kerja                                                                                                              | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 1784  | 1883  | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kecelakaan Lalu Lintas                                                                                                        | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 11204  | 0     | 0     | 0     | 0     | 18448 | 29952 | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kecelakaan Transportasi                                                                                                       | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 129   | 65    | 0     | 0     | 0     | 324  | 314  | 0    | 0    | 475  | 252  | 14   | 246  | 0     | 0     | 0      | 0     |
| Kecelakaan Transportasi Darat                                                                                                 | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 69    | 8     | 35     | 0     |
| Kecelakaan Transportasi Laut-Udara                                                                                            | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 34    | 0     | 134    | 0     |
| Kegagalan Teknologi                                                                                                           | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 3     | 6     | 0     | 25   | 4    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kegagalan Teknologi (termasuk ledakan kompor gas)                                                                             | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 5     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kehamilan yang berakhir abortus                                                                                               | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 499    | 95    | 205   | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kehamilan, Persalinan & Masa Nifas                                                                                            | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 857   | 2636  | 0     | 1807  | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kejadian Luar Biasa (KLB) - Keracunan                                                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 7    | 34   | 12   | 45   | 10    | 2     | 6      | 0     |
| Kejadian Luar Biasa (KLB) - Penyakit                                                                                          | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 66   | 0    | 2    | 82   | 8     | 30    | 0      | 0     |
| Kekeringan                                                                                                                    | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Keracunan                                                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 4     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Keracunan Makanan                                                                                                             | Bencana Non Alam dan Penyakit | 0    | 23   | 27   | 6    | 22     | 0     | 21    | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Keracunan/KLB                                                                                                                 | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 22   | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB                                                                                                                           | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 10    | 58    | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Antraks                                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 1     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Cacat Air                                                                                                                 | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Campak                                                                                                                    | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 44     | 7     | 0     | 0     | 0     | 42    | 6     | 10   | 4    | 1    | 21   | 0    | 4    | 14   | 0    | 0     | 0     | 0      | 0     |
| KLB Cikungunya                                                                                                                | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Demam Berdarah                                                                                                            | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Demam Berdarah Dengue (DBD)                                                                                               | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 91    | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 144  | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Dengue High Fever                                                                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 87     | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Dengue Shock Syndrome                                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 7      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Diare                                                                                                                     | Bencana Non Alam dan Penyakit | 218  | 200  | 188  | 256  | 158    | 694   | 1293  | 233   | 1135  | 300   | 438   | 60   | 107  | 21   | 87   | 90   | 12   | 68   | 36   | 0     | 0     | 0      | 0     |
| KLB Diare Berdarah                                                                                                            | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Difteri                                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 10     | 9     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Disentri                                                                                                                  | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Frambusia                                                                                                                 | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Gizi Buruk                                                                                                                | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 3     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Hand, Foot, Mouth Diseases                                                                                                | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Hepatitis                                                                                                                 | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 2      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Hepatitis Klinis                                                                                                          | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Keracunan                                                                                                                 | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 5      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Keracunan Makanan                                                                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 23     | 0     | 0     | 0     | 0     | 0     | 0     | 4    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Leptospirosis                                                                                                             | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 1      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Malaria                                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 15     | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Malaria Falsiparum                                                                                                        | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 44    | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Malaria Klinis                                                                                                            | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Marasmus                                                                                                                  | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Meningitis                                                                                                                | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Parotitis                                                                                                                 | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Pertusis                                                                                                                  | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Polio                                                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 8     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Rabies                                                                                                                    | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 13     | 18    | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Rubella                                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Tetanus                                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Tetanus Neonatal                                                                                                          | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 39     | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Thypoid                                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Tifus Perut                                                                                                               | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| KLB Typus Perut                                                                                                               | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kolera                                                                                                                        | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kondisi lain yang bermula pada masa perinatal                                                                                 | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 170    | 255   | 342   | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Kondisi Tertentu yang bermula pada masa Perinatal                                                                             | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 9873  | 19134 | 9822  | 27324 | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Konflik                                                                                                                       | Bencana Sosial                | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 16    | 33    | 34   | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Konflik Sosial                                                                                                                | Bencana Sosial                | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 1     | 0     | 0     | 0    | 65   | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Konflik Sosial atau Kerusuhan Sosial                                                                                          | Bencana Sosial                | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 45   | 13   | 0    | 7    | 4     | 0     | 0      | 0     |
| Kronis Filariasis                                                                                                             | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 425   | 891   | 617    | 0     |
| Ledakan (bom, tabung gas, dll)                                                                                                | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 9     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Ledakan Akibat Gas                                                                                                            | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 8    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Ledakan Bom                                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 2     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Ledakan Granat/Bom                                                                                                            | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 45    | 14    | 4     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Leptospirosis                                                                                                                 | Bencana Non Alam dan Penyakit | 0    | 0    | 21   | 20   | 75     | 62    | 47    | 146   | 76    | 138   | 258   | 492  | 174  | 300  | 307  | 256  | 185  | 352  | 446  | 366   | 212   | 168    | 0     |
| Letusan Gunung Api                                                                                                            | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 1    | 9    | 71   | 0    | 0     | 0     | 51     | 0     |
| Letusan Gunung Berapi                                                                                                         | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 382   | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Letusan/Peningkatan Aktivitas Gunung Api                                                                                      | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 2    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Longsor Sampah                                                                                                                | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 1    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Malaria (termasuk semua malaria)                                                                                              | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 3578   | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Klinik Malaria                                                                                                                | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 30    | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Malformasi, Deformasi Kongenital & Perbedaan Kromosom                                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 599   | 1082  | 0     | 605   | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Neoplasma                                                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 4822  | 6756  | 4585  | 8664  | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Apendiks                                                                                                             | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 234   | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Darah & Organ Pembuat Darah & Gangguan tertentu yang Melibatkan Mekanisme Imun                                       | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 225   | 258   | 0     | 1223  | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Endokrin, Nutrisi, dan Metabolik                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 4511  | 10484 | 5277  | 11170 | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit hemolitik pada janin dan bayi baru lahir                                                                             | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 17     | 26    | 20    | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Infeksi & Parasit Tertentu                                                                                           | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 12624 | 31968 | 14323 | 50307 | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit infeksi dan parasit kongenital                                                                                       | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 466    | 516   | 467   | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit jantung lainnya                                                                                                      | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 2577  | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Kulit & Jaringan Subkutan                                                                                            | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 201   | 378   | 0     | 324   | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Mata dan Adneksa                                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 14    | 574   | 0     | 123   | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Sistem Cerna                                                                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 5787  | 11478 | 6590  | 13650 | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Sistem Kemih Kelamin                                                                                                 | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 4390  | 7500  | 4557  | 9084  | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Sistem Muskuloskeletal dan Jaringan Ikat                                                                             | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 235   | 470   | 0     | 605   | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Sistem Napas                                                                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 6075  | 12312 | 7214  | 24570 | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Sistem Sirkulasi Darah                                                                                               | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 19944 | 38722 | 21830 | 69489 | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Susunan Syaraf                                                                                                       | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 3089  | 5788  | 0     | 3218  | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyakit Telinga dan Kelebihan. Mastoideus                                                                                    | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 21    | 70    | 0     | 109   | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyulit kehamilan dan persalinan lainnya                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 552   | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Penyulit kehamilan, persalinan dan masa nifas lainnya                                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 1508   | 214   | 250   | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Perdarahan antepartum                                                                                                         | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 11     | 16    | 8     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Perdarahan intrakranial                                                                                                       | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 2868   | 3572  | 7354  | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Perdarahan pasca persalinan                                                                                                   | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 43     | 71    | 43    | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Persalinan dengan penyulit gawat janin                                                                                        | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 11     | 8     | 11    | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Persalinan prematur                                                                                                           | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 23     | 31    | 34    | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Pertumbuhan janin lamban, malnutrisi janin dan gangguan yang berhubungan dengan kehamilan pendek dan berat badan lahir rendah | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 2100   | 2606  | 5156  | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Petir                                                                                                                         | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 7     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Plasenta previa                                                                                                               | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 30     | 40    | 36    | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Radang paru-paru                                                                                                              | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 3103   | 2765  | 4918  | 0     | 0     | 2365  | 2630  | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Rabies                                                                                                                        | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 19    | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Rabies - Lyssa                                                                                                                | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 585   | 824   | 1100 | 822  | 595  | 456  | 925  | 568  | 435  | 333  | 115   | 40    | 124    | 0     |
| Rubella                                                                                                                       | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Sebab Luar Morbiditas & Mortalitas                                                                                            | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 2745  | 2020  | 0     | 2046  | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Septisemia                                                                                                                    | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 2369   | 3065  | 5078  | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Stroke tidak menyebut pendarahan atau infark                                                                                  | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 4215   | 4692  | 8754  | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Tanah Longsor                                                                                                                 | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 170   | 123   | 46    | 103   | 73    | 131   | 84   | 54   | 0    | 0    | 96   | 168  | 16   | 23   | 34    | 20    | 50     | 0     |
| TB Paru                                                                                                                       | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 3271  | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| TB Paru BTA Positif                                                                                                           | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 3282  | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Tersambar Petir                                                                                                               | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 1    | 6    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Tetanus                                                                                                                       | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 43    | 20    | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Neonatorium Tetanus                                                                                                           | Bencana Non Alam dan Penyakit | 183  | 100  | 91   | 98   | 42     | 136   | 83    | 74    | 100   | 76    | 84    | 69   | 59   | 42   | 54   | 27   | 14   | 14   | 4    | 2     | 2     | 18     | 0     |
| Tsunami                                                                                                                       | Bencana Alam                  | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 2    | 0    | 0    | 0    | 0    | 0    | 0    | 431  | 0     | 0     | 0      | 0     |
| Tsunami Aceh (Hilang)                                                                                                         | Bencana Alam                  | 0    | 0    | 0    | 0    | 37527  | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Tsunami Aceh (Meninggal)                                                                                                      | Bencana Alam                  | 0    | 0    | 0    | 0    | 129171 | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Tuberkulosis                                                                                                                  | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 11993 | 13174 | 14148  | 0     |
| Tuberkulosis Paru                                                                                                             | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 3852   | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Tuberkulosis paru lainnya                                                                                                     | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 2024  | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |
| Wabah Penyakit (Epidemi)                                                                                                      | Bencana Non Alam dan Penyakit | 0    | 0    | 0    | 0    | 0      | 0     | 0     | 0     | 0     | 0     | 0     | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0     | 0     | 0      | 0     |

## Instruksi B

1. Buka data berikut: [Data Kematian di Indonesia](https://www.kaggle.com/datasets/hendratno/cause-of-death-in-indonesia) menggunakan Google Spreadsheet
2. Pada Menu Bar pilih Ekstensi kemudian pilih App Script
3. Masukkan Kode Script berikut kedalam App Script:

```
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
```

4. Klik Jalankan kemudian tunggu hingga Proses selesai
5. Lakukan pengecekan hasil Tabulasi Silang pada Google Spreadsheet
6. Hasil Tabulasi Silang akan Berada di Sheet baru

### Table B

| Type                          | Year | Total Deaths |
| ----------------------------- | ---- | ------------ |
| Bencana Alam                  | 2015 | 215          |
| Bencana Alam                  | 2016 | 442          |
| Bencana Alam                  | 2017 | 169          |
| Bencana Alam                  | 2018 | 3739         |
| Bencana Alam                  | 2019 | 352          |
| Bencana Alam                  | 2020 | 236          |
| Bencana Alam                  | 2021 | 583          |
| Bencana Non Alam dan Penyakit | 2015 | 3160         |
| Bencana Non Alam dan Penyakit | 2016 | 2754         |
| Bencana Non Alam dan Penyakit | 2017 | 1454         |
| Bencana Non Alam dan Penyakit | 2018 | 1730         |
| Bencana Non Alam dan Penyakit | 2019 | 14582        |
| Bencana Non Alam dan Penyakit | 2020 | 37929        |
| Bencana Non Alam dan Penyakit | 2021 | 139404       |
| Bencana Sosial                | 2015 | 45           |
| Bencana Sosial                | 2016 | 26           |
| Bencana Sosial                | 2017 | 0            |
| Bencana Sosial                | 2018 | 25           |
| Bencana Sosial                | 2019 | 7            |
| Bencana Sosial                | 2020 | 4            |
| Bencana Sosial                | 2021 | 4            |

Table diatas sudah mengalami penyesuaian karena jika menggunakan semua data, terdapat data yang hilang
