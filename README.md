# Data Wrangler Extension for Visual Studio Code

[Data Wrangler](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.datawrangler) is a code-centric data cleaning tool that is integrated into VS Code and VS Code Jupyter Notebooks. Data Wrangler aims to increase the productivity of data scientists doing data cleaning by providing a rich user interface that automatically generates Pandas code for and shows insightful column statistics and visualizations.

[<img src="https://user-images.githubusercontent.com/8560030/225425356-c0abf8e2-332f-439c-8de1-9a5946b933ee.png" />](https://youtu.be/KrzcV1c1W1U)

This document will cover how to:

-   Install and setup Data Wrangler
-   Launch Data Wrangler from a notebook
-   Use Data Wrangler to explore your data
-   Perform operations on your data
-   Edit and export code for data wrangling to a notebook
-   Troubleshooting and providing feedback

## Setting up your environment

1. If you have not already done so, install [Python](https://www.python.org/downloads/).  
   **IMPORTANT:** Data Wrangler only supports Python version 3.7 or higher.
2. Install [Visual Studio Code](https://code.visualstudio.com/download).
3. Install the [Data Wrangler extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.datawrangler) from the Visual Studio Marketplace. For additional details on installing extensions, see Extension Marketplace. The Data Wrangler extension is named Data Wrangler and it’s published by Microsoft.

When you launch Data Wrangler for the first time, it will ask you which Python kernel you would like to connect to. It will also check your machine and environment to see if any required Python packages are installed (e.g., Pandas).

> Here is a list of the required versions for Python and Python packages, along with whether they are automatically installed by Data Wrangler:
>
> | Name    | Minimum required version | Automatically installed |
> | ------- | ------------------------ | ----------------------- |
> | Python  | 3.7                      | No                      |
> | pandas  | 0.25.0                   | Yes                     |
> | regex\* | 2020.11.13               | Yes                     |
>
> _\* We use the open-source `regex` package to be able to use Unicode properties (for example, `/\p{Lowercase_Letter}/`), which aren't supported by Python's built-in regex module (`re`). Unicode properties make it easier and cleaner to support foreign characters in regular expressions._

If they are not found on your environment, Data Wrangler will attempt to install them for you via pip. If Data Wrangler is unable to install dependencies, the easiest workaround is to manually run pip install, and then launch Data Wrangler again. These dependencies are required for Data Wrangler such that it can generate Python and Pandas code.

### Connecting to a Python kernel

There are currently two ways to connect to a Python kernel, as shown in the quick pick below.  
![image](https://user-images.githubusercontent.com/8560030/225400310-cea6cf16-de2e-484d-b3d9-3c60ecb36b50.png)

#### 1. Connect using local Python interpreter

If this option is selected, then the kernel connection is created using the Jupyter and Python extensions. We recommend this option for a simple setup and quick way to get started with Data Wrangler.

#### 2. Connect using Jupyter URL and token

If this option is selected, then a kernel connection is created using JupyterLab APIs. Note that there are performance benefits with this option since it bypasses some initialization and kernel discovery processes. However, it will also require separate user management of the Jupyter notebook server. We recommend this option generally in two cases: 1) if there are blocking issues in the first method and 2) for power users who would like to reduce the cold-start time of Data Wrangler.

To set up a Jupyter notebook server and use it with this option, follow the steps below:

1. Install Jupyter. We recommend installing the free version of [Anaconda](https://www.anaconda.com/products/individual) which comes with Jupyter installed. Alternatively, follow the [official instructions](https://jupyter.org/install) to install it.
2. In the appropriate environment (e.g. in an Anaconda prompt if Anaconda is used), launch the server with the following command (replace the jupyter token with your secure token):
   `jupyter notebook --no-browser --NotebookApp.token='<your-jupyter-token>'`
3. In Data Wrangler, connect using the address of the spawned server. E.g. http://localhost:8888 and pass in the token used in the previous step. Once configured, this information is cached locally and can automatically be reused for future connections.

## Launching Data Wrangler

Once Data Wrangler has been successfully installed, there are 2 ways to launch it in VS Code.

### Launching Data Wrangler from a Jupyter Notebook

If you are in a Jupyter Notebook working with Pandas data frames, you’ll now see a “Launch Data Wrangler” button appear after running specific operations on your data frame, such as df.head(). Clicking the button will open a new tab in VS Code with the Data Wrangler interface in a sandboxed environment.

![image](https://user-images.githubusercontent.com/2180824/218180019-d2c434dd-2a27-4355-a00a-f8ec09a1f828.png)

### Launching Data Wrangler directly from a CSV file

You can also launch Data Wrangler directly from a local CSV file. To do so, open any folder in VS Code that has the CSV dataset you’d like to explore. In the File Explorer panel, right click the .CSV dataset and click “Open in Data Wrangler”.

![image](https://user-images.githubusercontent.com/2180824/218180054-386cf32a-8876-48dd-8065-134d0bd932f0.png)

## Using Data Wrangler

![image](https://user-images.githubusercontent.com/2180824/218180077-8bbb9018-c67b-4fda-b4cd-9ea7c67eea5b.png)

The Data Wrangler interface is divided into 6 components, described below.

The **Quick Insights** header is where you can quickly see valuable information about each column. Depending on the datatype of the column, Quick Insights will show the distribution of the data or the frequency of datapoints, as well as missing and unique values.

The **Data Grid** gives you a scrollable pane where you can view your entire dataset. Additionally, when selecting an operation to perform, a preview will be illustrated in the data grid, highlighting the modified columns.

The **Operations Panel** is where you can search through all of Data Wrangler’s built-in data operations. The operations are organized by their top-level category.

The **Summary Panel** shows detailed summary statistics for your dataset or a specific column if one is selected. Depending on the datatype, it will show information such as min, max values, datatype of the column, skew, and more.

The **Operation History Panel** shows a human readable list of all the operations that have been previously applied in the current Data Wrangling session. It enables the user to undo specific operations or edit the most recent operation. Selecting a step will highlight the changes in the data grid and will show the generated code associated with that operation.

The **Code Preview** section will show the Python and Pandas code that Data Wrangler has generated when an operation is selected. It will remain blank when no operation is selected. The code can even be edited by the user, and the data grid will highlight the effect on the data.

### Example: Filtering a column

Let’s go through a simple example using Data Wrangler with the Titanic dataset to filter adult passengers on the ship.

We’ll start off by looking at the quick insights of the Age column, and we’ll notice the distribution of the ages and that the minimum age is 0.42. For more information, we can have a glance at the Summary panel to see that the datatype is a float, along with additional statistics such as the mean and median age of all the passengers.

![image](https://user-images.githubusercontent.com/2180824/218180630-73009474-54ff-439d-bd22-a3cc97363904.png)

To filter for only adult passengers, we can go to the Operation Panel and search for the keyword “Filter” to find the **Filter** operation. (You can also expand the “Sort and filter” category to find it.)

![image](https://user-images.githubusercontent.com/2180824/218180718-1e6da67f-cf5c-43b8-be80-e22e722aa908.png)

Once we select an operation, we are brought into the Operation Preview state where parameters can be modified to see how they affect the underlying dataset prior to applying the operation. In this example, we want to filter the dataset to only include adults, so we’ll want to filter the Age column to only include values greater than or equal to 18.

![image](https://user-images.githubusercontent.com/2180824/218180755-3d9eb2d0-e4c0-4959-9ba1-75b19df047eb.png)

Once the parameters are entered in the operation panel, we can see a preview of what will happen to the data. We’ll notice that the minimum value in age is now 18 in the Quick Insights, along with a visual preview of the rows that are being removed highlighted in red. Finally, we’ll also notice the Code Preview section automatically shows the code that Data Wrangler produced to execute this Filter operation. We can edit this code, such as change the filtered age to 21, and the data grid will automatically update accordingly.

After confirming that the operation has the intended effect, we can click Apply.

## Editing and exporting code

Each step of the generated code can be modified. As you make changes, changes to the data will be highlighted in the grid view.

Once you’re done with your data cleaning steps in Data Wrangler, there are 3 ways to export your cleaned dataset from Data Wrangler.

1. Export code back to Notebook and exit: This creates a new cell in your Jupyter Notebook with all the data cleaning code you generated packaged up into a clean Python function.
2. Export data as CSV: This saves the cleaned dataset as a new CSV file onto your machine.
3. Copy code to clipboard: This copies all the code that was generated by Data Wrangler for the data cleaning operations.

![image](https://user-images.githubusercontent.com/2180824/218180955-ed417931-5337-4c8a-93c7-36a6b3c13332.png)

Note: If you launched Data Wrangler directly from a CSV, the first export option will be to export the code into a new Jupyter Notebook.

## Data Wrangler operations

These are the Data Wrangler operations that are currently supported in the initial launch of Data Wrangler (with many more to be added in the near future).

| Operation                      | Description                                                                                           |
| ------------------------------ | ----------------------------------------------------------------------------------------------------- |
| Sort values                    | Sort column(s) ascending or descending                                                                |
| Filter                         | Filter rows based on one or more conditions                                                           |
| Calculate text length          | Create new column with values equal to the length of each string value in a text column               |
| One-hot encode                 | Split categorical data into a new column for each category                                            |
| Multi-label binarizer          | Split categorical data into a new column for each category using a delimiter                          |
| Create column from formula     | Create a column using a custom Python formula                                                         |
| Change column type             | Change the data type of a column                                                                      |
| Drop column                    | Delete one or more columns                                                                            |
| Select column                  | Choose one or more columns to keep and delete the rest                                                |
| Rename column                  | Rename one or more columns                                                                            |
| Drop missing values            | Remove rows with missing values                                                                       |
| Drop duplicate rows            | Drops all rows that have duplicate values in one or more columns                                      |
| Fill missing values            | Replace cells with missing values with a new value                                                    |
| Find and replace               | Replace cells with exact matching pattern                                                             |
| Group by column and aggregate  | Group by columns and aggregate results                                                                |
| Strip whitespace               | Remove whitespace from the beginning and end of text                                                  |
| Split text                     | Split a column into several columns based on a user defined delimiter                                 |
| Convert text to capital case   | Capitalize the first character of a string with the option to apply to all words                      |
| Convert text to lowercase      | Convert text to lowercase                                                                             |
| Convert text to uppercase      | Convert text to UPPERCASE                                                                             |
| String transform by example    | Automatically perform string transformations when a pattern is detected from the examples you provide |
| DateTime formatting by example | Automatically perform DateTime formatting when a pattern is detected from the examples you provide    |
| New column by example          | Automatically create a column when a pattern is detected from the examples you provide.               |
| Scale min/max values           | Scale a numerical column between a minimum and maximum value                                          |
| Custom operation               | Automatically create a new column based on examples and the derivation of existing column(s)          |

## Troubleshooting

### General kernel connectivity issues

For general connectivity issues, please see the "Connecting to a Python kernel" section above on alternative methods to connect. To debug issues related to the local Python interpreter option, one way to potentially fix the issue would be to try installing different versions of the Jupyter and Python extensions. For example, if stable versions of the extensions are installed then one could try installing the pre-release (and vice versa). If the issue is new, then consider reverting to a previous version.

To clear an already cached kernel, you can run the `Data Wrangler: Clear cached runtime` command from the command palette (Ctrl/Cmd+Shift+P).

### UnicodeDecodeError

If you run into a UnicodeDecodeError when opening a data file directly from Data Wrangler, then this could be caused by two possible issues:

1. The file you're trying to open has an encoding other than utf-8, and/or
2. The file is corrupted.

To work around this error, you’ll need to open Data Wrangler from a Jupyter Notebook instead of directly from a data file. Use a Jupyter Notebook to read the file using Pandas, for example using the [read_csv](https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html) method. Within that read method, use the _encoding_ and/or _encoding_errors_ parameters to define the encoding to use or how to handle encoding errors. If you don’t know which encoding might work for this file, you can try a library such as [chardet](https://github.com/chardet/chardet) to try to infer an encoding that works.

## Questions and feedback

If you have problems, have feature requests, or any other feedback, please submit an Issue on our GitHub repository: [https://github.com/microsoft/vscode-data-wrangler/issues/new/choose](https://github.com/microsoft/vscode-data-wrangler/issues/new/choose)

## Privacy Statement

The [Microsoft Enterprise and Developer Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=521839) describes the privacy statement of this software.
