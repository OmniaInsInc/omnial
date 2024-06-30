// Handle POST requests to add data
function doPost(e) {
  const sheet = SpreadsheetApp.openById('1cjuafyKl4YoxkFAxcrBF968tY5L9x60zwUMzqv10nts').getActiveSheet();
  const jsonData = JSON.parse(e.postData.contents);
  const fields = ['timestamp', 'firstName', 'lastName', 'email', 'phone', 'state', 'gender'];
  const newRow = fields.map(field => jsonData[field] || '');
  sheet.appendRow(newRow);
  return ContentService.createTextOutput(JSON.stringify({ result: 'success' }))
    .setMimeType(ContentService.MimeType.JSON);
}

// Handle GET requests to retrieve data
function doGet(e) {
  const sheet = SpreadsheetApp.openById('1cjuafyKl4YoxkFAxcrBF968tY5L9x60zwUMzqv10nts').getActiveSheet();
  const rows = sheet.getDataRange().getValues();
  const data = rows.slice(1).map(row => {
    return {
      timestamp: row[0],
      firstName: row[1],
      lastName: row[2],
      email: row[3],
      phone: row[4],
      state: row[5],
      gender: row[6]
    };
  });
  return ContentService.createTextOutput(JSON.stringify(data))
    .setMimeType(ContentService.MimeType.JSON);
}

// Handle DELETE requests to remove data
function doDelete(e) {
  const sheet = SpreadsheetApp.openById('1cjuafyKl4YoxkFAxcrBF968tY5L9x60zwUMzqv10nts').getActiveSheet();
  const jsonData = JSON.parse(e.postData.contents);
  const emailToDelete = jsonData.email;
  const dataRange = sheet.getDataRange();
  const values = dataRange.getValues();

  for (let i = values.length - 1; i >= 0; i--) {
    if (values[i][3] === emailToDelete) { // Assuming email is in the 4th column
      sheet.deleteRow(i + 1); // Adjust for 0-based index
      return ContentService.createTextOutput(JSON.stringify({ result: 'success', message: 'Row deleted' }))
        .setMimeType(ContentService.MimeType.JSON);
    }
  }
  return ContentService.createTextOutput(JSON.stringify({ result: 'error', message: 'Email not found' }))
    .setMimeType(ContentService.MimeType.JSON);
}

// Handle OPTIONS requests for preflight
function doOptions(e) {
  return ContentService.createTextOutput('')
    .setMimeType(ContentService.MimeType.JSON);
}
