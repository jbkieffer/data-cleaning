# Data Cleaning with MS Excel

## Character Encoding

When we open a data file in MS Excel, sometimes we will see that characters don't correctly display. Find the sample data file `doaj-article-sample.csv` in the `data` directory of your downloaded materials. Double click the file to open it with Excel. Scan through the Title and Authors columns to see some examples of this problem.

![Character display problems in an Excel spreadsheet](/img/encoding-errors.PNG "Example encoding errors")

To prevent this problem, we need to open the file differently. Close the data file and don't save any changes. Open a new blank Excel workbook.

Follow these steps to choose a specific character encoding when opening a data file using Excel:
1. From a new Excel workbook, click on Data in the menu bar
2. In the Ribbon, choose From Text
3. Navigate to the sample data file `doaj-article-sample.csv` and click Import

![MS Excel import data file screen](/img/choose-file.PNG "Import a file into Excel")

4. Follow the steps of the Text Import Wizard:
   - Step 1:
     - For original data type, choose Delimited
	 - Start import at row 1
	 - File origin: **Change from Windows (ANSI) to 65001 : Unicode (UTF-8)**
	 - **Check** the option, "My data has headers"
	 - ![Excel Text Import Wizard Step 1 screen](/img/text-import-1.PNG "Import data step 1")
	 - Click Next
   - Step 2:
     - Since this is a .csv (comma separated file), change the delimiter from Tab to Comma
	 - ![Excel Text Import Wizard Step 2 screen](/img/text-import-2.PNG "Import data step 2")
   - Step 3:
     - We don't want Excel to mess with the `Dates` column, so highlight that column and change the format of the column to Text
	 - ![Excel Text Import Wizard Step 3 screen](/img/text-import-3-date-text.PNG "Import data step 3")
   - Step 4:
     - Import the data into the existing blank worksheet starting at cell A1
	 - ![Excel Text Import Wizard Step 4 screen](/img/text-import-4.PNG "Import data step 4")
	 - Click OK

Most of the character encoding issues are now fixed.

![Character display corrected in an Excel spreadsheet](/img/encoding-fixed.PNG "Example encoding repairs")

**Don't overwrite your original raw data!** Save the data as a new file by clicking File > Save As. Change to the `outputs` directory and save your file with a new name. You can keep the file in .csv format or save it as an Excel (.xlsx) file.

![Save the imported data as a new file](/img/save-new-file.PNG "Save imported data to a new file")

---

## Trim whitespace

When we try to sort or match data we may encounter errors caused by additional whitespace at the beginning or end of a piece of data. The source of these problems can be hard to spot visually since the characters that create whitespace are not rendered in Excel's user interface. A common early step in any data cleaning process is to trim whitespace. We can do this in Excel using a formula. We are going to practice these steps using the data in the Title column.

Be sure you are working in your new saved file in the `/outputs` directory, e.g.: `/outputs/doaj-article-sample-clean.csv`

1. Add two empty columns to the right of the Title column.
   - One of these columns will be for the formula. Name this column `TrimTitleFormula`
   - The other column will be for the text output of the formula. Name this column `TrimmedTitle`
   - ![Excel Add a blank column](/img/add-column.png "Add a new column in Excel")
   - ![New Excel columns](/img/new-columns.PNG "Two new Excel columns")
2. In the first empty cell of the `TrimTitleFormula` column, type the formula `=TRIM(A2)`
   - ![Excel TRIM formula in a spreadsheet](/img/trim-formula.PNG "Enter the TRIM formula in cell B2")
3. Press Enter. The formula will disappear in the cell and be replaced by the formula results, the trimmed text from cell A2
   - The formula doesn't change the text if there is no additional whitespace to trim
4. Apply the formula to the rest of the data in the `Title` column:
   - Highlight cell B2, which contains the `TRIM` formula 
   - Drag the little green square at the bottom right of the cell all the way to the bottom of the column (row 1002). This will fill the empty cells with the formula and adjust the cell value that the formula is applied to.
   - ![Excel click and drag to copy a formula down a column](/img/drag-trim.png "Drag down cell B2 to copy the formula")
   - When you are finished, the column will fill with the trimmed text from the `Title` column
   - ![Excel filled column of trimmed Title data](/img/filled-title.PNG "Formula applied to all Title cells")
5. The column `TrimTitleFormula` appears to contain cleaned up Title data, but Excel is tricking you. The cells really contain formulas and can't be used for anything in their current state. We need to turn the formula results into actual text using the second empty column, `TrimmedTitle`:
   - Highlight all of the values in the `TrimTitleFormula` column, from B2 to B1002. A handy keyboard shortcut is to highlight cell B2 and then type Shift + Control (Command on a Mac) + the down arrow. Copy these values using your preferred method.
   - Now click into cell C2, the first empty cell in the column `TrimmedTitle`.
   - Right click (command click on a Mac) cell C2 and choose `Paste Values` - the icon looks like a clipboard with the numbers 123 on top.
   - ![Paste values into an Excel column](/img/paste-values.png "Paste values into an Excel column")
   - The text of the trimmed Titles will be inserted into the `TrimmedTitle` column
6. To keep your cleaned data file usable by other computer programs, it's important to remove dirty data and intermediate steps in the cleaning process. It's okay to delete columns in this version of your data, because you have saved it separately from your raw data.
   - Highlight the `TrimTitleFormula` column and delete it from the spreadsheet (the entire column, not just the cell contents).
   - Repeat this step for the original `Title` column
   - Change the name of the column `TrimmedTitle` to `Title`
   
Your `Title` data is now clean. If you want to practice these steps again, there are also extra whitespace characters in the `Publisher` column.

---

## Resources

Microsoft Office Support, "Top 10 ways to clean your data" https://support.microsoft.com/en-us/office/top-ten-ways-to-clean-your-data-2844b620-677c-47a7-ac3e-c2e157d1db19