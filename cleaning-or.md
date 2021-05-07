# Data Cleaning with OpenRefine

## Software Installation

This tutorial assumes that you have OpenRefine installed on your computer. To install OpenRefine, [download](https://openrefine.org/download.html) the version that's appropriate for your computer. OpenRefine relies on Java. If you are not sure whether Java or an open Java alternative (e.g.: OpenJDK Java, Amazon Coretto) is installed on your computer, choose an OpenRefine package that includes embedded Java.

Launch OpenRefine on Windows by finding the file `openrefine.exe` inside the directory you downloaded during installation. Launch OpenRefine on a Mac by using Finder to locate it in your Application directory.

When you launch OpenRefine, a command line window will open first, followed by a new tab or window in your default browser. Ignore the command line window; you will work in the browser. OpenRefine does not require an internet connection and is not running in the cloud. It is using your browser as its user interface.

See the OpenRefine Documentation for detailed help with [installing or upgrading OpenRefine](https://docs.openrefine.org/manual/installing#installing-or-upgrading) or with [running OpenRefine](https://docs.openrefine.org/manual/running).

---

## Character Encoding

Unlike Excel, we can't open a data file in OpenRefine without completing some data import steps. During these steps, we can address the file's character encoding.

1. From the OpenRefine home screen, choose `Create Project`
2. In the `Get data from` menu, choose `This Computer`
3. `Browse` to the `data` directory of your downloaded materials for this tutorial
4. Find the `doaj-article-sample.csv` file and click `Open`
   - ![Open data file in OpenRefine](/img/or/import-data.png "Create project by importing data")
5. Click `Next`. OpenRefine will load the data and display a preview
   - ![OpenRefine data import preview](/img/or/data-preview.png "Preview data import settings")
6. In the data import settings under the data preview, we can see that OpenRefine is automatically detecting things about our data that we needed to manually set Excel to do:
   - Parse the data as `CSV / TSV / separator-based files`
   - Detect that columns are separated by `commas (CSV)`
   - Parsing 1 line as the column header
   - Detecting Character Encoding as `UTF-8`
7. For this data file, we don't need to do anything special to change the character encoding to `UTF-8`. If we needed to change the encoding, we could click the Character encoding box to see a list of encoding choices
   - ![Select encoding in OpenRefine](/img/or/select-encoding.png "Options for changing encoding")
   
We will finish parsing and importing the data in the next section.

---

## Trim Whitespace

Beginning with version 3.4, OpenRefine offers the option to strip whitespace in comma-separated and tab-separated files during data parsing and importing. This tutorial will focus on this method.

OpenRefine can also strip whitespace on separated values and other data types after a project is created. This tutorial will not focus on this method; it is described in [OpenRefine Documentation about transforming data](https://docs.openrefine.org/manual/cellediting#transform)

1. Refer to the data preview and data import settings we generated in the previous section
   - ![OpenRefine data import preview](/img/or/data-preview.png "Preview data import settings")
2. The data parsing option `Trim leading & trailing whitespace from strings` option should be checked by default. If it isn't, check it.
   - ![OpenRefine data parsing options](/img/or/trim-option.png "Check the option to trim whitespace")
3. With no other changes to make to how OpenRefine is parsing our data, we can finish creating the project:
   - In the `Project name` box at the top right, give the project a name, e.g. `DOAJ-article-sample`
   - Click `Create Project`
   - ![Name and create OpenRefine project](/img/or/name-create-project.png "Name the project and click Create Project")
   
We have completed two major data cleaning steps while creating a project within OpenRefine. OpenRefine automatically saves subsequent cleaning steps to the project. None of our cleaning steps will affect the original raw data.

---

## Check for Missing Data

With OpenRefine, we can check for missing data using facets. Each column of data has its own menu of operations. We will be working to locate missing DOIs in the `DOI` column.

1. Find the `DOI` column in your new OpenRefine project and click the down arrow beside the column name
   - ![OpenRefine column menu](/img/or/column-menu.png "Click the arrow to access the column menu")
2. In the column menu, choose `Facet`, then `Customized facets`, then `Facet by blank (null or empty string)`
   - ![OpenRefine facet options](/img/or/facet-blank.png "Navigate to Facet by blank")
3. The `Facet / Filter` panel will open on the left. A box using the name of the column we faceted will contain the results of the facet:
   - `false: 978` indicates that 978 rows are NOT blank at the `DOI` column
   - `true: 23` indicates that 23 rows ARE blank at the `DOI` column
   - ![OpenRefine facet results for Facet by blank](/img/or/facet-blank-results.png "Facet results")
4. To see the 23 rows with missing DOIs, click on `true` in the results. Only rows with missing DOIs will be displayed
5. To export only these rows, click `Export` at the top right of the screen while the facet is active
   - Choose a file type that works for you. Depending on your work, good choices include tab- or comma-separated values, Excel, ODF spreadsheet (for LibreOffice Calc), or Google Sheets.
   - Exporting these rows to a file does not remove them from the OpenRefine project.
6. To reset the display, click `reset` at the top of the active facet
   - ![Reset faceted display](/img/or/facet-reset.png "Reset faceted display")
7. As with Excel, it is possible to layer facets to find very specific slices of data, e.g.: all rows with missing DOIs and missing license terms. To do this, repeat the facet steps above on the `License` column while the `DOI` facet is still active
   - A `License` facet will appear below the `DOI` facet, containing our results:
     - `false: 17` indicates that, of 23 rows isolated by the `DOI` facet, 17 rows are NOT blank at the `License` column
	 - `true: 6` indicates that, of 23 rows isolated by the `DOI` facet, 6 rows ARE blank at the `License` column
	 - ![Add a second facet](/img/or/add-facet.png "Add a License facet to further slice the data")
   - To see the 6 rows with missing DOI and missing License data, click on `true` in the `License` facet results
     - Follow the instructions from step 5 to export only these 6 rows
8. To remove a facet, click the `X` at the top left of the facet you want to remove
   - ![Remove one facet](/img/or/remove-facet.png "Remove one facet")
9. To reset or remove all active facets, click either the `Reset All` or `Remove All` button at the top of the `Facet / Filter` panel
   - ![Reset or remove all facets](/img/or/remove-facet-all.png "Reset or remove all facets")

---

## Consolidate Terms

We can also use OpenRefine's facets to consolidate terms. We are going to replace the term "English" in the `Language` column with the abbreviation "EN".

If you haven't already done so, remove all facets from previous steps.

1. Find the `Language` column in your OpenRefine project and click the down arrow beside the column name
2. Choose `Facet`, then `Text facet`
   - ![OpenRefine text facet](/img/or/text-facet.png "Open text facet from the column menu")
3. The new `Language` facet shows our results:
   - ![Language text facet](/img/or/facet-language.png "Language text facet")
4. To edit cells containing "English", hover over the result `English 107` and click `edit`
   - ![Edit cell contents in OpenRefine](/img/or/edit-facet.png "Edit a facet result")
   - In the text box that appears, change `English` to `EN`, then click `Apply`
   - ![Apply changes to an edited facet](/img/or/apply-facet-change.png "Click Apply to change the text")
   - The `Language` facet results now show no cells containing "English" and 978 cells containing "EN"
5. Close the `Language` facet

If you want to practice these steps again, you can look for terms to consolidate in the `Publisher` column.

---

## Using Data Cleaned with OpenRefine

Once we finish cleaning data with OpenRefine, we need to export it in order to use it for our work. The `Export` steps are described in step 5 of the [Missing Data section](https://github.com/jbkieffer/data-cleaning/blob/main/cleaning-or.md#check-for-missing-data). Depending on your next steps, you can export part or all of the data.

To export all of the data, remove all facets before you proceed. To export a piece or slice of the data, use one or more facets to display only the rows you want to export.

---

## Replicate Cleaning Steps with OpenRefine

Often, we need to repeat the same cleaning steps on new data, e.g. if we receive a monthly file from a vendor. This is possible in OpenRefine by extracting operation history.

To extract cleaning steps for future use:

1. In the top left of the OpenRefine screen, click the `Undo / Redo` tab
   - You will see a list of the edits you have made to your data. 
   - This list won't include any operations for viewing data, e.g. the facets we added in the Missing Data section of this tutorial.
   - ![OpenRefine undo redo tab](/img/or/undo-redo.png "Click Undo Redo to extract cleaning steps")
2. Highlight the step or steps you want to extract and click `Extract`
   - OpenRefine will open the `Extract Operation History` window with JSON code highlighted for you
   - ![OpenRefine Extract History window](/img/or/extract-history.png "Copy the highlighted code to extract a cleaning step")
   - Copy that code and paste it into a plain text file, not a Word document. Save the file with your data projects, e.g.: `doaj-cleaning-steps.txt`
   - Close the `Extract Operation History` window

To apply an extracted cleaning step to a different OpenRefine project:

1. Create your new project in OpenRefine
2. Open the `Undo / Redo` tab
3. Click `Apply`
   - OpenRefine will open the `Apply Operation History` window
   - Paste the JSON code you copied from a previous project into the empty box
   - ![OpenRefine Apply History window](/img/or/apply-history.png "Paste JSON code to repeat a cleaning step")
   - Click `Perform Operations`
4. Check the affected columns to confirm that your intended edits are complete

---

## Resources

The [Library Carpentry OpenRefine lesson](https://librarycarpentry.org/lc-open-refine/) includes more cleaning steps using this DOAJ data, as well as more uses for OpenRefine.

The [OpenRefine Documentation](https://openrefine.org/documentation.html) contains links to get started and learn more. 