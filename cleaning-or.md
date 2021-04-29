# Data Cleaning with OpenRefine

## Software Installation

This tutorial assumes that you have OpenRefine installed on your computer. To install OpenRefine, [download](https://openrefine.org/download.html) the version that's appropriate for your computer. OpenRefine relies on Java. If you are not sure whether Java or an open Java alternative (e.g.: OpenJDK Java, Amazon Coretto) is installed on your computer, choose an OpenRefine package that includes embedded Java.

Launch OpenRefine on Windows by finding the file `openrefine.exe` inside the directory you downloaded during installation. Launch OpenRefine on a Mac by using Finder to locate it in your Application directory.

When you launch OpenRefine, a command line window will open first, followed by a new tab or window in your default browser. Ignore the command line window; you will work in the browser. OpenRefine does not require an internet connection and is not running in the cloud. It is using your browser as its user interface.

See the [OpenRefine Documentation](https://docs.openrefine.org/manual/running) for help with running OpenRefine.

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


---

## Check for Missing Data


---

## Consolidate Terms


---

## Resources