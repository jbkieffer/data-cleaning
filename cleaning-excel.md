# Data Cleaning with MS Excel

## Software Installation

This tutorial assumes that you have a recent version of MS Excel installed on your computer, or that you have access to Excel through Office365. If you are using Office365, open Excel in the desktop version of the software to follow along completely.

---

## Character Encoding

When we open a data file in MS Excel, sometimes we will see that characters don't correctly display. Find the sample data file `doaj-article-sample.csv` in the `data` directory of your downloaded materials. Double click the file to open it with Excel. Scan through the `Title` and `Authors` columns to see some examples of this problem.

![Character display problems in an Excel spreadsheet](/img/encoding-errors.PNG "Example encoding errors")

To prevent this problem, we need to open the file differently. Close the data file and don't save any changes. Open a new blank Excel workbook.

Follow these steps to choose a specific character encoding when opening a data file using Excel:
1. From a new Excel workbook, click on `Data` in the menu bar
2. In the `Data` ribbon, choose `From Text`
3. Navigate to the sample data file `doaj-article-sample.csv` and click `Import`

![MS Excel import data file screen](/img/choose-file.PNG "Import a file into Excel")

4. Follow the steps of the `Text Import Wizard`:
   - Step 1:
     - For original data type, choose `Delimited`
	 - Start import at row 1
	 - File origin: Change from `Windows (ANSI)` to `65001 : Unicode (UTF-8)`
	 - Check the option `My data has headers`
	 - ![Excel Text Import Wizard Step 1 screen](/img/text-import-1.PNG "Import data step 1")
	 - Click `Next`
   - Step 2:
     - Since this is a .csv (comma separated file), change the delimiter from `Tab` to `Comma`
	 - ![Excel Text Import Wizard Step 2 screen](/img/text-import-2.PNG "Import data step 2")
   - Step 3:
     - We don't want Excel to mess with the `Dates` column, so highlight that column and change the format of the column to `Text`
	 - ![Excel Text Import Wizard Step 3 screen](/img/text-import-3-date-text.PNG "Import data step 3")
   - Step 4:
     - Import the data into the existing blank worksheet starting at cell A1
	 - ![Excel Text Import Wizard Step 4 screen](/img/text-import-4.PNG "Import data step 4")
	 - Click `OK`

Many of the character encoding issues are now fixed.

![Character display corrected in an Excel spreadsheet](/img/encoding-fixed.PNG "Example encoding repairs")

**Don't overwrite your original raw data!** Save the data as a new file by clicking `File` > `Save As`. Change to the `outputs` directory and save your file with a new name. You can keep the file in .csv format or save it as an Excel (.xlsx) file.

![Save the imported data as a new file](/img/save-new-file.PNG "Save imported data to a new file")

---

## Trim Whitespace

When we try to sort or match data we may encounter errors caused by additional whitespace at the beginning or end of a piece of data. The source of these problems can be hard to spot visually since the characters that create whitespace are not rendered in Excel's user interface. A common early step in any data cleaning process is to trim whitespace. We can do this in Excel using a formula. We are going to practice these steps using the data in the `Title` column.

Be sure you are working in your new saved file in the `/outputs` directory, e.g.: `/outputs/doaj-article-sample-clean.csv`

1. Add two empty columns to the right of the `Title` column.
   - ![Excel Add a blank column](/img/add-column.png "Add a new column in Excel")
   - One of these columns will be for the formula. Name this column `TrimTitleFormula`
   - The other column will be for the text output of the formula. Name this column `TrimmedTitle`
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
   - Highlight all of the values in the `TrimTitleFormula` column, from B2 to B1002. A handy keyboard shortcut is to highlight cell B2 and then type `Shift + Control + down arrow` (`Shift + Command + down arrow` on a Mac). Copy these values using your preferred method.
   - Now click into cell C2, the first empty cell in the column `TrimmedTitle`.
   - Right click (command click on a Mac) cell C2 and choose `Paste Values` - the icon looks like a clipboard with the numbers 123 on top.
   - ![Paste values into an Excel column](/img/paste-values.png "Paste values into an Excel column")
   - The text of the trimmed Titles will be inserted into the `TrimmedTitle` column
6. To keep your cleaned data file usable by other computer programs, it's important to remove dirty data and intermediate steps in the cleaning process. It's okay to delete columns in this version of your data, because you have saved it separately from your raw data.
   - Highlight the `TrimTitleFormula` column and delete it from the spreadsheet (the entire column, not just the cell contents).
   - Repeat this step for the original `Title` column
   - Change the name of the column `TrimmedTitle` to `Title`
7. Save these changes to your file.
   
Your `Title` data is now clean. If you want to practice these steps again, there are also extra whitespace characters in the `Publisher` column.

---

## Check for Missing Data

Another common data cleaning step is checking for missing data. Blank cells could interfere with our uses for the data. In some cases, data creators use cell values such as 0, 999, or N/A to indicate missing data; these values can also interfere with our work. In Excel, we can check for missing data using filters. We will check for missing DOIs in the `DOI` column.

Be sure you are working in your saved file in the `/outputs` directory, e.g.: `/outputs/doaj-article-sample-clean.csv`

1. Click on `Data` in Excel's menu bar
2. In the `Data` ribbon, click on `Filter`. The icon looks like a funnel.
   - Each column header will receive a down arrow icon
   - ![Active filters in an Excel spreadsheet](/img/filter.png "Activate filters for an Excel spreadsheet")
3. In the `DOI` column, click on the `Filter` arrow. There are many ways to filter; for our purposes, we will use the list of cell contents at the bottom of the `Filter` menu.
   - In the list of DOIs, uncheck `(Select All)`
   - ![De-select all DOI results in Excel filter menu](/img/filter-doi-1.png "Uncheck (Select All)")
   - Scroll to the bottom of the list of DOIs and check `(Blanks)`
   - ![Select blank DOI cells in Excel filter menu](/img/filter-doi-2.png "Check (Blanks)")
   - Excel now only shows us 23 rows where the DOI cell is blank 
4. Depending on our needs, we could remove these rows to a different file for further processing. For our purposes, we will leave them in the current file.
5. We need to clear the `DOI` filter when we are finished. With Excel, you can layer filters to find very specific slices of data, e.g.: all rows with missing DOIs and missing license terms. However, it's easy to forget to clear filters; this can lead to incomplete results in subsequent operations.
   - In the `DOI` column, click on the `Filter` icon. Since the column is filtered, the down arrow has changed to a funnel.
   - Select `Clear Filter from "DOI"`
   - ![Clear filter from DOI column](/img/clear-filter.png "Select Clear Filter from DOI")
   
We now know that 23 rows of data do not contain DOIs. If you want to practice these steps again, you can check for missing data in the `License` and `Language` columns.

---

## Consolidate Terms

Imposing consistency on data is another common cleaning step. Inconsistent use of terms, abbreviations, decimals, and other data elements can limit the usefulness of our data and hinder analysis. In Excel, we can consolidate terms using `Find and Replace`. We are going to replace the EN abbreviation for `Language` with the full term English. We are not going to fill in cells where `Language` data is missing.

Be sure you are working in your saved file in the `/outputs` directory, e.g.: `/outputs/doaj-article-sample-clean.csv`

1. Highlight the `Language` column. This prevents us from accidentally overwriting data in other colums.
2. Bring up the `Find and Replace` window using one of these methods:
   - Use the keyboard shortcut `Control + F` (`Command + F` on a Mac). In the resulting window, choose the `Replace` tab.
   - Click on `Home` in Excel's menu bar. In the `Home` ribbon, click on `Find & Select`. The icon looks like a magnifying glass. Click on `Replace`.
   - ![Excel's Replace window](/img/replace.png "Replace window")
3. Fill in the window as follows:
   - Find what: EN
   - Replace with: English
4. Click `Options`. We need to make the search more exact for efficiency
   - Check `Match case`
   - Check `Match entire cell contents`
   - ![Completed options in Excel Replace window](/img/replace-options.png "Complete options for data matching")
5. Click `Find Next` several times to confirm that Excel is only finding cells containing EN in the `Language` column
   - Once you are satisfied, click `Replace` to replace values one by one, or `Replace All` to replace all values at once
   - When it's finished, Excel should have made 871 replacements
6. Save these changes to your file.

---

## Resources

Microsoft Office Support, "Top 10 ways to clean your data" https://support.microsoft.com/en-us/office/top-ten-ways-to-clean-your-data-2844b620-677c-47a7-ac3e-c2e157d1db19