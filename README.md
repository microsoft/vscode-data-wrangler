# Data Wrangler Extension for Visual Studio Code

 - 📊 Visualize & filter large tabular datasets
 - 🧹 One-click transforms (fill, drop, type-cast…)
 - 🐼 Automatic Pandas code preview & export
 - 🚀 Launch from CSV/Parquet/Excel/Jsonl files or Jupyter notebooks
 - 🤖 GitHub Copilot integration: just ask it to perform the data operations you need
 - ⚙️ Give it an example and it will figure out the rest of the rows based on it

[Data Wrangler](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.datawrangler) is a data viewing and cleaning tool that is integrated into VS Code and VS Code Jupyter Notebooks. It provides a rich user interface to view and analyze your data, show insightful column statistics and visualizations, and can automatically generate Pandas code as you clean and transform the data if that's your goal.

**Data Exploration**

![a gif of opening Data Wrangler from a .csv file, looking through the data, navigating to specific columns, viewing column statistics, sorting columns, and applying column filters.](https://github.com/microsoft/vscode-data-wrangler/blob/bd86979f293036db078028a0268c1b36b226caca/assets/data-wrangler-marketplace-data-exploration.gif?raw=true)

**Data Preparation**

![a gif of opening Data Wrangler from a notebook, looking through the data, switching from Viewing to Editing mode, applying data transformations, and exporting the generated Python code back into the notebook](https://github.com/microsoft/vscode-docs/assets/15910920/1a6d8fd1-6454-4289-b8c4-fe84050ae981)

The goal of this page is to help you quickly get up and running with Data Wrangler.

## Set up your environment

1. If you have not already done so, install [Python](https://www.python.org/downloads/)
   (**Note:** Data Wrangler only supports Python version 3.8 or higher).
2. <a class="install-extension-btn" href="vscode:extension/ms-toolsai.datawrangler">Install the Data Wrangler extension</a>

When you launch Data Wrangler for the first time, it asks you which Python kernel you would like to connect to. It also checks your machine and environment to see if the required Python packages are installed, such as Pandas.

Note: to use a local Python interpreter as a runtime, you will need to first install both the [Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) and [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) extensions.

## Open Data Wrangler

Anytime you are in Data Wrangler, you are in a _sandboxed_ environment, meaning you are able to safely explore and transform the data. The original dataset is not modified until you explicitly export your changes.

### Data Wrangler with Jupyter Notebooks

If you have a Pandas data frame in your notebook, you can explore its contents using Data Wrangler without leaving the notebook’s output cell since it is seamlessly integrated into one experience.

![a gif of viewing the contents of a Pandas dataframe using the integrated Data Wrangler experience from inside the notebooks output cell.](https://github.com/microsoft/vscode-data-wrangler/blob/main/assets/data-wrangler-marketplace-output-mode.png?raw=true)

From here, you can also launch Data Wrangler in full screen mode by simply clicking the Open ‘df’ in Data Wrangler button.

![a screenshot showing the entry point into Data Wrangler from a notebook](https://github.com/microsoft/vscode-data-wrangler/blob/main/assets/data-wrangler-marketplace-open-df.png?raw=true)

### Launch Data Wrangler directly from a file

You can also launch Data Wrangler directly from a local file (such as a `.csv`). To do so, open any folder in VS Code that contains the file you’d like to open. In the File Explorer view, right click the file and click **Open in Data Wrangler**.

![a screenshot showing the entry point into Data Wrangler from a file](https://github.com/microsoft/vscode-docs/assets/15910920/517e1e29-ba45-4e24-87fb-adb53a6207f1)

## UI tour

Data Wrangler has two modes when working with your data. The details for each mode are explained in the subsequent sections below.

1. **Viewing mode:** The viewing mode optimizes the interface for you to quickly view, filter and sort your data. This mode is great for doing initial exploration on the dataset.
2. **Editing mode:** The Editing mode optimizes the interface for you to apply transformations, cleaning, or modifications to your dataset. As you apply these transformations in the interface, Data Wrangler automatically generates the relevant Pandas code, and this can be exported back into your notebook for reuse.

Note: For notebook files, Data Wrangler opens by default in the Viewing mode. You can change this behavior in the Settings editor `kb(workbench.settings.dataWrangler.startInEditModeForNotebookEntrypoints)`. For other file types, the current default is Editing mode only.

### Viewing mode interface

![a screenshot showing the different components in the UI for Data Wrangler in Viewing mode](https://github.com/microsoft/vscode-docs/assets/15910920/16d7d4d9-63e8-459f-9b7c-5bb1908b245d)

1. The **Data Summary** panel shows detailed summary statistics for your overall dataset or a specific column, if one is selected.

2. You can apply any **Data Filters/Sorts** on the column from the header menu of the column.

3. Toggle between the **Viewing** or **Editing** mode of Data Wrangler to access the built-in data operations.

4. The **Quick Insights** header is where you can quickly see valuable information about each column. Depending on the datatype of the column, quick insights shows the distribution of the data or the frequency of datapoints, as well as missing and distinct values.

5. The **Data Grid** gives you a scrollable pane where you can view your entire dataset.

---

### Editing mode interface

Switching to Editing mode enables additional functionality and user interface elements in Data Wrangler. In the following screenshot, we use Data Wrangler to replace the missing values in the last column with the median of that column.

![a screenshot showing the different components in the UI for Data Wrangler in Editing mode](https://github.com/microsoft/vscode-docs/assets/15910920/8ec458aa-556d-4f03-beda-c86898d97112)

1. The **Operations** panel is where you can search through all of Data Wrangler’s built-in data operations. The operations are organized by category.

2. The **Cleaning Steps** panel shows a list of all the operations that have been previously applied. It enables the user to undo specific operations or edit the _most recent_ operation. Selecting a step will highlight the changes in the data grid and will show the generated code associated with that operation.

3. The **Export Menu** lets you export the code back into a Jupyter Notebook or export the data into a new file.

4. When you have an operation selected and are previewing its effects on the data, the grid is overlayed with a **data diff** view of the changes you made to the data.

5. The **Code Preview** section shows the Python and Pandas code that Data Wrangler has generated when an operation is selected. It remains empty when no operation is selected. You can edit the generated code, which results in the data grid highlighting the effects on the data.

## Example: Replace missing values in your dataset

Given a dataset, one of the common data cleaning tasks is to handle any missing values that lie within the data. The example below shows how Data Wrangler can be used to replace the missing values in a column with the median value of that column. While the transformation is done through the interface, Data Wrangler also automatically generates the Python and Pandas code required for the replacement of missing values.

![an example of using Data Wrangler to replace missing values in your dataset](https://github.com/microsoft/vscode-docs/assets/15910920/2235a291-e26f-4741-b5fc-bd570c8f66d1)

1. In the **Operations Panel**, search for the **Fill Missing Values** operation.
2. Specify in the parameters what you would like to replace the missing values with. In this case, we will be replacing the missing values with the median value for the column.
3. Validate that the data grid is showing you the correct changes in the data diff.
4. Validate that the code generated by Data Wrangler is what you intended.
5. Apply the operation and it will be added to your cleaning steps history.

# Next steps

This page covered how to quickly get started with Data Wrangler. For the full documentation and tutorial of Data Wrangler, including all the built-in operations that Data Wrangler currently supports, please see the following page.

[Working with Data Wrangler](https://code.visualstudio.com/docs/datascience/data-wrangler)

## Questions and feedback

If you have problems, have feature requests, or any other feedback, please submit an Issue on our GitHub repository: [https://github.com/microsoft/vscode-data-wrangler/issues/new/choose](https://github.com/microsoft/vscode-data-wrangler/issues/new/choose)

## Data and telemetry

The Microsoft Data Wrangler Extension for Visual Studio Code collects usage data and sends it to Microsoft to help improve our products and services. Read our [privacy statement](https://go.microsoft.com/fwlink/?LinkId=521839) to learn more. This extension respects the `telemetry.telemetryLevel` setting which you can learn more about at https://code.visualstudio.com/docs/getstarted/telemetry.
