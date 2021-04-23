# Data Cleaning with MS Excel

## Character Encoding

When we open a data file in MS Excel, sometimes we will see that characters don't correctly display. Find the sample data file `doaj-article-sample.csv` in the `data` directory of your downloaded materials. Double click the file to open it with Excel. Scan through the Title and Authors columns to see some examples of this problem.

![Character display problems in an Excel spreadsheet](../img/encoding-errors.PNG "Example encoding errors")

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
     - **possibly revise** Leave all columns in General format, meaning that Excel will interpret the contents on its own
	 - ![Excel Text Import Wizard Step 3 screen](/img/text-import-3.PNG "Import data step 3")
	 - If there is data you don't want Excel to mess with (e.g.: Dates), change the format of the column to Text
	 - ![Excel Text Import Wizard Step 3 screen](/img/text-import-3-date-text.PNG "Import data step 3")
	 - **possible lesson item** break Dates into M D Y columns - can only do this if the column starts as Text
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

When we try to sort or match data we may encounter errors caused by additional whitespace at the beginning or end of a piece of data. TThe source of these problems can be hard to spot visually since the characters that create whitespace are not rendered in Excel's user interface. A common early step in any data cleaning process is to trim whitespace. We can do this in Excel using a formula.

Be sure you are working in your new saved file in the `/outputs` directory, e.g.: `/outputs/doaj-article-sample-clean.csv`

Instructions at https://support.microsoft.com/en-us/office/trim-function-410388fa-c5df-49c6-b16c-9e5630b479f9

---

## Resources

Microsoft Office Support, "Top 10 ways to clean your data" https://support.microsoft.com/en-us/office/top-ten-ways-to-clean-your-data-2844b620-677c-47a7-ac3e-c2e157d1db19