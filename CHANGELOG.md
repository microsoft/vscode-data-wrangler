# Changelog

## Version 0.24.1
### Updates
-   Added support for Jupyter extension versions `v2024.2.2024020201` and higher.

## Version 0.24.0
### Updates
#### Files
-   Added support for opening Data Wrangler from XLSX, XLS, and TSV files.
-   When opening a file in Data Wrangler, a prompt will now offer to configure Data Wrangler as the default editor for all files with that extension.
-   When opening a CSV file in Data Wrangler, the column delimiter is now automatically detected. This enables users to easily open CSV data separated by tabs, semicolons, spaces, etc. This behavior can be disabled from the extension settings.

#### Notebooks
-   The old cell output launch button has been deprecated and removed. It is now replaced with a cell status bar entrypoint using the same launch criteria.
-   The following data types are now also supported: Pandas Series, Lists, Dicts, Tensors.
-   It is now possible to also launch using display(variable_name), print(variable_name) at the end of a cell.
-   Added a new launch entrypoint from the notebook toolbar which displays a list of all variables that can be opened in Data Wrangler.
-   Entering from the notebook now displays a shimmer and missing dependencies are installed using popups. This should make it faster to get started.
-   Add experimental setting to enable use of newly proposed Jupyter extension APIs for code execution.

#### Operations
-   Added compatibility mode for the Sort and Filter operations to cast unknown data types into the string type. This will allow all columns to be filterable and sortable regardless of the contents.
-   Filter operation now supports a shorthand way to specify additional conditions on the same column.
-   Small performance optimizations for sort, filter and group by and aggregate to skip code execution when adding and deleting groups.

#### Statistics
-   Improved the appearance of visualizations on columns with mixed data.
-   Improve histogram binning for float columns with only integer values.
-   Avoid recalculating column statistics if rows are simply reordered by a custom operation.

#### UX
-   Updates to statistics in the summary panel are now visually smoother and have less flickering.
-   Added minimum width to dropdown UI to improve visibility of controls when panels are small.
-   Improvements to notification of kernel reload. It now shows progress per cleaning step.
-   Minor improvements to error stack traces.
-   The executed code and stack trace can now be inspected when an error occurs while loading data.
-   Parquet export is now enabled by default. If pyarrow is not installed, then a prompt will appear to install it.

### Bugfixes
-   Fixed an issue where column visualizations could sometimes fail to update when the data changes.
-   Fixed an issue where multi-selecting columns would also select the column text.
-   Fixed an issue where the launch entrypoints would not work if pandas and numpy are not installed.
-   Fixed an issue where the column visualizations would not be displayed if the “View Past Code Steps” setting was set to “Enabled”.
-   Fixed an issue where the example code snippet in the Code Preview panel could refer to a non-existent column name.


## Version 0.22.3
### Updates
* Support for Pandas 2.2.0

## Version 0.22.2
### Bugfixes
* Fixed an issue where "Sort Descending" was setting the sort order to ascending when invoked from the context menu.

## Version 0.22.1
### Bugfixes
* Fixed an issue where column visualizations could sometimes fail to update when the data changes

## Version 0.22.0
### Updates
* Updates to the Filter, Sort, and Group By and Aggregate operations
  * UX made more compact with fewer dropdowns
  * Groups can now be reordered using drag handle or menu
  * Missing parameters will no longer break the preview
  * It is now possible to perform a group by without aggregations
* Miscellaneous styling updates to make operations more compact

### Bugfixes
* Fixed an issue where, in certain scenarios, some loading failures would occur without generating an error message. This fix will facilitate the identification of issues during the startup process.
* For Python packages where the imported name differs from the package name (e.g., import sklearn vs. package name scikit-learn), Data Wrangler now uses the correct package name when suggesting installation. It does this by keeping an internal mapping of import name to package name for the most commonly used Python packages.

## Version 0.20.0
### Updates
* Missing values are now displayed with a different style in the grid.
* Percentages in column statistics now show "<1%" instead of "0%" when the ratio is below 1% but non-zero. Similar behavior applies to ratios between 99% and 100%.
* It is now possible to export code and data without having to first perform operations. This will allow users additional flexibility with generating import code and with exporting into different file formats. Note: when entering Data Wrangler from a notebook, it will still be required to do operations before exporting the code.
* When an operation fails due to a missing package (such as when importing in a custom operation), Data Wrangler will now display a button to quickly install the missing package based on the imported name.
* Removed the requirement to install `regex` package when loading Data Wrangler.

### Accessibility improvements
* Ensure that all content within the operations and code preview panels remains accessible even at high zoom level.
* Added the ability to select operations using a keyboard.
* Operation preview status is now announced when using a screen reader.
* Added or fixed ARIA labels, roles, and attributes in several places, including:
  * Tree views in the operations and summary panels
  * Operation argument fields
  * Column type and status icons
  * Icon-only buttons in the grid and operations panel

### Bugfixes
* Fixed an issue where the most frequent value was not shown in the summary panel for DateTime or Boolean columns.
* Fixed an issue in numeric histograms where values lying very close to bucket boundaries could sometimes be placed in the wrong bucket.
* Fixed an issue where the code preview panel would not have a title if moved to a different location in the VS Code UI.
* Fixed issue where overriding definitions from the builtins namespace could cause runtime errors.
* Fixed issue where toolbar overflow behaviour was broken. Menu items now move into an overflow menu when there is not enough space.
* Fixed an issue where the placeholder text in the code preview panel could overflow with no available scrollbar.
* Resize the icon for the "Open in Data Wrangler" button, as it was getting cut off in recent versions of VS Code.

## Version 0.18.0
### Updates
* Added new "Go to column" button to reveal and smoothly scroll to a target column in the grid.
* Issue report button now also includes relevant Python package information in the report.
* Launching Data Wrangler from a Jupyter notebook now opens multiple tabs when the same variable name is launched.
* To maximize screen real estate, users can now show or hide the column statistics that appear on the column headers.
* When using a Filter operation, users can now invert the filter conditions by choosing between “Keep matching rows” and “Delete matching rows”.
* Enabled keyboard-accessible tooltips on cleaning steps for improved accessibility.

### Bugfixes
* Double clicking on a column now correctly expands to the full width of the column.
* Fixed issue where the launch button would sometimes not appear after running a cell.

## Version 0.16.0
**Deprecation notice**
* The `mad` (Mean Absolute Deviation) aggregation type has been removed from the Group By and Aggregate operation as it is no longer available in pandas.

### Updates
* Improved support for detecting conditional formulas in the "by example" operations.
* Improved keyboard accessibility by enabling keyboard focus on elements in the Cleaning Steps panel.
* Improved keyboard accessibility in the Grid view by reducing the number of tab stops. Once focused, the grid can be navigated using the arrow keys, page up / down, home, etc.

### Bugfixes
* Fixed issue where data frames with duplicate index keys could not be properly viewed or wrangled. Please note for this scenario that there are some limitations with generating the diff previews, these are outlined [here](https://github.com/microsoft/vscode-data-wrangler/wiki/Known-Issues#pandas-dataframes-with-duplicate-index-keys).

## Version 0.14.0
### Updates
* Added support for exporting data in the Parquet format. The users can enable this option in the settings, and the feature will be enabled by default on a future version.
* Improvements to column visualizations including adjustments to accessibility labels and improved formatting of tooltip contents.

### Bugfixes
* Fixed an issue where Data Wrangler was expanding all VS Code panels (bottom panel and sidebars) even when the Data Wrangler tab was being unfocused.
* Fixed an issue where the wrong column would sometimes be selected for operations when columns are dynamically disabled (e.g., Fill NA).

## Version 0.12.0
### Updates
* Added the ability to copy one or more selected data rows via the grid cell context menu.
* Added command "Reveal Source File in Explorer View" which reveals the original source dataset file in the file explorer pane.
* The operation list expansion state now persists across operations, and is unique to each Data Wrangler tab.
* Enabled additional code editor features in the code preview panel, such as copy/pasting via the context menu, and dragging-and-dropping text content into the editor.
* Column insights are now rendered using a library with much better accessibility support, including keyboard navigation, screen reader feedback, and more.
* Added options "Match full string", "Match case", and "Use regular expression" to operation "Find and replace".
* Added new numerical operations "Round", "Round down (floor)", and "Round up (ceiling)".

## Version 0.10.0
### Updates
* Exports to CSV can now be cancelled before completing, via the VS Code toast notification.
 
### Bugfixes
* Fixed an issue where errors may not be caught in some cases when using IPython version 8.12.1 or above.

## Version 0.8.0
### Updates:
* In "Find and replace" operation, surface a form field error if the "Old value" field is left empty.
* Improve readability of code example in code editor placeholder text by showing `df = df.drop(columns=['ColumnName'])` instead of `df = drop('ColumnName', axis=1)`.
* Removed the `inplace=True` and `copy=False` parameters from generated pandas code, as those aren't considered best practice and [are being considered for deprecation](https://github.com/pandas-dev/pandas/pull/51466) in Pandas.
* Improved support for all VS Code themes.

### Bugfixes:
* In "Find and replace" operation, preserve the contents of fields "Old value" and "New value" when "Target columns" is changed.
* Fixed an issue where timestamps ignored time zone information when displayed in the grid.
* Fixed an issue for the context menu to disable the context menu operations when required.
* Fixed issue where the operation panel collapses when clicking on the grid.
* Fixed an issue where errors may not be caught in some cases when using IPython version 8.12.1 or above.

## Version 0.6.0
### Updates:
* Jupyter extension installer now installs the stable version instead of pre-release to improve stability for the first install experience.
* The Data Wrangler software requires Python 3.8 or a later version to run as older versions of Python are losing support from several open-source libraries used by Data Wrangler.
* When exporting code to a new Jupyter notebook, Data Wrangler will now carry over the compute selection. This way, a user will no longer need to manually choose the same compute a second time after exporting. Note: This change only applies to the “Local Python Interpreter” connection method and is currently only available when using the preview version of the Jupyter extension for VS Code.
* Updated the example Titanic dataset to add a column that was missing.
 
### Bugfixes:
* Fixed an issue where the tooltip for unsupported data types was pointing to the wrong element.
* Fixed an issue where an error would be thrown for the "Calculate Text Length" operation when changing targets with a custom column name set. 

## Version 0.4.0
* General bug fixes and improvements

## Version 0.2.1

### Bugfixes:
* Fixed an issue where the grid would sometimes experience problems after performing an operation that involved editing it.

## Version 0.2.0
* _First release of Data Wrangler! 🎉_
