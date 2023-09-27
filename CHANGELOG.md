# Changelog

## Version 0.18.0
**Updates**
* Added new "Go to column" button to reveal and smoothly scroll to a target column in the grid.
* Issue report button now also includes relevant Python package information in the report.
* Launching Data Wrangler from a Jupyter notebook now opens multiple tabs when the same variable name is launched.
* To maximize screen real estate, users can now show or hide the column statistics that appear on the column headers.
* When using a Filter operation, users can now invert the filter conditions by choosing between “Keep matching rows” and “Delete matching rows”.
* Enabled keyboard-accessible tooltips on cleaning steps for improved accessibility.

**Bugfixes**
* Double clicking on a column now correctly expands to the full width of the column.
* Fixed issue where the launch button would sometimes not appear after running a cell.

## Version 0.16.0
**Deprecation notice**
* The `mad` (Mean Absolute Deviation) aggregation type has been removed from the Group By and Aggregate operation as it is no longer available in pandas.

**Updates**
* Improved support for detecting conditional formulas in the "by example" operations.
* Improved keyboard accessibility by enabling keyboard focus on elements in the Cleaning Steps panel.
* Improved keyboard accessibility in the Grid view by reducing the number of tab stops. Once focused, the grid can be navigated using the arrow keys, page up / down, home, etc.

**Bugfixes**
* Fixed issue where data frames with duplicate index keys could not be properly viewed or wrangled. Please note for this scenario that there are some limitations with generating the diff previews, these are outlined [here](https://github.com/microsoft/vscode-data-wrangler/wiki/Known-Issues#pandas-dataframes-with-duplicate-index-keys).

## Version 0.14.0
**Updates**
* Added support for exporting data in the Parquet format. The users can enable this option in the settings, and the feature will be enabled by default on a future version.
* Improvements to column visualizations including adjustments to accessibility labels and improved formatting of tooltip contents.

**Bugfixes**
* Fixed an issue where Data Wrangler was expanding all VS Code panels (bottom panel and sidebars) even when the Data Wrangler tab was being unfocused.
* Fixed an issue where the wrong column would sometimes be selected for operations when columns are dynamically disabled (e.g., Fill NA).

## Version 0.12.0
**Updates**
* Added the ability to copy one or more selected data rows via the grid cell context menu.
* Added command "Reveal Source File in Explorer View" which reveals the original source dataset file in the file explorer pane.
* The operation list expansion state now persists across operations, and is unique to each Data Wrangler tab.
* Enabled additional code editor features in the code preview panel, such as copy/pasting via the context menu, and dragging-and-dropping text content into the editor.
* Column insights are now rendered using a library with much better accessibility support, including keyboard navigation, screen reader feedback, and more.
* Added options "Match full string", "Match case", and "Use regular expression" to operation "Find and replace".
* Added new numerical operations "Round", "Round down (floor)", and "Round up (ceiling)".

## Version 0.10.0
**Updates**
* Exports to CSV can now be cancelled before completing, via the VS Code toast notification.
 
**Bugfixes**
* Fixed an issue where errors may not be caught in some cases when using IPython version 8.12.1 or above.

## Version 0.8.0
**Updates**:
* In "Find and replace" operation, surface a form field error if the "Old value" field is left empty.
* Improve readability of code example in code editor placeholder text by showing `df = df.drop(columns=['ColumnName'])` instead of `df = drop('ColumnName', axis=1)`.
* Removed the `inplace=True` and `copy=False` parameters from generated pandas code, as those aren't considered best practice and [are being considered for deprecation](https://github.com/pandas-dev/pandas/pull/51466) in Pandas.
* Improved support for all VS Code themes.

**Bugfixes**:
* In "Find and replace" operation, preserve the contents of fields "Old value" and "New value" when "Target columns" is changed.
* Fixed an issue where timestamps ignored time zone information when displayed in the grid.
* Fixed an issue for the context menu to disable the context menu operations when required.
* Fixed issue where the operation panel collapses when clicking on the grid.
* Fixed an issue where errors may not be caught in some cases when using IPython version 8.12.1 or above.

## Version 0.6.0
**Updates**:
* Jupyter extension installer now installs the stable version instead of pre-release to improve stability for the first install experience.
* The Data Wrangler software requires Python 3.8 or a later version to run as older versions of Python are losing support from several open-source libraries used by Data Wrangler.
* When exporting code to a new Jupyter notebook, Data Wrangler will now carry over the compute selection. This way, a user will no longer need to manually choose the same compute a second time after exporting. Note: This change only applies to the “Local Python Interpreter” connection method and is currently only available when using the preview version of the Jupyter extension for VS Code.
* Updated the example Titanic dataset to add a column that was missing.
 
**Bugfixes**:
* Fixed an issue where the tooltip for unsupported data types was pointing to the wrong element.
* Fixed an issue where an error would be thrown for the "Calculate Text Length" operation when changing targets with a custom column name set. 

## Version 0.4.0
* General bug fixes and improvements

## Version 0.2.1

**Bugfixes**:
* Fixed an issue where the grid would sometimes experience problems after performing an operation that involved editing it.

## Version 0.2.0
* _First release of Data Wrangler! 🎉_
