# Changelog

## Version 1.20.0
### Updates
- Improved the display of error messages shown before the data is loaded.
- Added an indicator next to required fields for improved clarity.

### Accessibility improvements
- Added screen reader announcement when searching for operations and there are no results
- Improved labeling of form fields and buttons in filter operations.

### Bugfixes
- Fixed an issue where an error message appeared in the output above DataFrames that subclass Pandas DataFrames (e.g., GeoDataFrame).
- Fixed an issue where a KeyError would sometimes be thrown when launching Data Wrangler while debugging with Python 3.12.
- Fixed an issue where changing kernels could fail if the currently selected kernel had also failed to load the data, such as due to missing dependencies.
- Fixed a few minor styling issues.

## Version 1.18.2
- General bugfixes and improvements.

## Version 1.18.1
### Bugfixes
- Fixed an issue where the output renderer was not rendering correctly in vscode.dev.

## Version 1.18.0
### Updates
- Data Wrangler is now supported in Jupyter notebook outputs! 🎉 The new output renderer provides a compact viewer for quick explorations within the notebook and can be invoked by producing a Pandas DataFrame expression in the last line of a cell or by displaying it with `display(<expression>)`.
- The Copilot prompt widget for Edit mode is now shown by default to help users discover GitHub Copilot Free. This can be disabled by setting `dataWrangler.experiments.copilot.enabled` to false.
- CSV file export now preserves the initial delimiter if opened from a CSV file.

### Bugfixes
- Fixed an issue where changing a kernel would still use the old cached kernel until VS Code was reloaded.
- Fixed a few minor styling issues.

## Version 1.16.0
### Updates
- Optimized loading performance when viewing datasets that present specific cases like memory fragmentation, or low kernel performance.
- Improvements to the loading view with an updated shimmer.
- Reduced jitteriness when applying operations while scrolled down in the grid.
- Added new quick filter mode to search for values by string. This should help address the need for simple faster filtering. The original filter menu can be accessed by showing advanced options or shown by default using the `dataWrangler.defaultViewingFilterOptions` setting.
- Updated the column width default to be a fixed width of 200px. This value is configurable with the `dataWrangler.grid.defaultColumnWidth` setting.
- Improved the display of columns at smaller widths by condensing column insights and header buttons.

### Bugfixes
- Fixed an issue where a named index would not be included in CSV exports if it was a MultiIndex.
- Fixed a styling issue causing panels to use the wrong background color.
- Fixed an issue causing performance issues when loading DataFrames using the interchange protocol API.
- Fixed an issue where the Ctrl+Tab VS Code shortcut would not work when the data grid was focused.
- Fixed an error that could occur when previewing changes to nested arrays.

## Version 1.14.0
### Updates
- Added new setting `config.dataWrangler.panels.displayOnTabFocus` which can optionally disable Data Wrangler's bottom and side panels from being automatically re-opened when a user starts Data Wrangler or clicks on one of its windows.
- Sorting and filtering by the index column is now supported. The index can also be renamed when in editing mode.
- Removed the header text label for default (unmodified) index columns.
- Column insights and summary stats are now shown for user-set index columns.
- Added support for copying cell contents using keyboard shortcuts (ctrl+C or cmd+C).
- Added optimizations for variable import to support different viewing strategies, which should generally improve the layout of the data on import (e.g., support for list of dictionaries, using index orientation for flat dictionaries).
- Added support for PySpark Connect DataFrames.
- Derivative DataFrame classes are now supported when Pandas converters exist (e.g., toPandas(), to_pandas(), interchange API).
- Added ability to edit the initial code when importing a variable, similar to how it is possible to edit for file imports.
- Improvements to automatically generated diffs when previewing custom operations.
- Removed the "Use Jupyter Proposed API" setting. The API is stable and now used by default.
- Show a more descriptive error message when access has not been granted to the Jupyter kernel.
- Added a warning message for users with invalid `extensions.experimental.affinity` setting. Namely, when the affinity value doesn't match the one set in all the extensions that Data Wrangler depends on.
- Small context menu style tweaks.

### Bugfixes
- Fixed an issue where the "missing value" label would sometimes not be visible in the grid.
- Fixed an issue where the second click on a sort/filter view tag would not close the context menu.
- Fixed an issue where filtering for isMissing or isNotMissing in compatibility mode would no-op as values are always casted to strings.

## Version 1.12.0
### Updates
- Added a new Copilot-powered prompt widget above the code editor to generate data-aware code using natural language. This feature can be enabled from the VS Code extension settings page for Data Wrangler, and requires both the [GitHub Copilot Chat VS Code extension](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat) and having an active [Copilot Subscription](https://github.com/features/copilot).

## Version 1.10.0
### Updates
- Improved error messaging for unsupported variable types.
- Added experimental support for loading PySpark DataFrame variables. This can be enabled using the `dataWrangler.experiments.datatypes.pyspark` setting.
- Added experimental support for JSONL files. This can be enabled using the `dataWrangler.enabledFileTypes.jsonl` setting.

### Bugfixes
- Fixed an issue where the order of copied rows was sorted incorrectly.
- Fixed an issue where overridden built-ins could cause launch to fail.

## Version 1.8.1
## Bugfixes
- Fixed an issue causing the extension to crash on older VS Code versions.
- Fixed an issue preventing subsequent debug data viewer launches when multiple debug sessions have the same ID.

## Version 1.8.0
### Updates
- Added extra fallback for debug launch scenario to help increase reliability.
- Added an option to disable showing column header stats on initialization. This can be useful in some workflows where column stats are not needed.
- New operation parameters
  - (Drop missing values) specify how many values must be missing from the selected columns for a row to be dropped.
  - (Split text) specify a maximum number of splits allowed.

### Bugfixes
- Fixed a launch issue affecting interactive window Python debugging using older IPython versions.
- Fixed an issue that could cause datasets with extremely long string values to get stuck loading indefinitely.

## Version 1.6.0
### Updates
- Raised the minimum required version of Pandas from 0.25.4 to 1.2.0.
- Added support for the "View data" toolbar menu in interactive window notebook.
- Shortened tab length and swapped editor icon to use color.
- Updated overflow logic for numeric fields to hide from the right side instead of the left.
- Small theming improvements.

### Bugfixes
- Fixed an issue where numeric data could be incorrectly formatted under certain circumstances such as when there is a column of complex values elsewhere.
- Fixed an issue where the notebook kernel for IPYNB files was not always automatically reconnecting after a debug session terminated.
- Fixed an issue where the datetime picker would render incorrectly when using the "Find and replace" operation on a datetime field.
- Fixed an issue where missing dependencies were not being prompted for install.
- Fixed an issue where package dependencies may not be correctly detected in some Python configurations.
- Fixed an issue where opening Data Wrangler from a long file path with the "Debug" setting enabled would cause stability issues.

## Version 1.4.2
### Bugfixes
- Fixed an issue where the filter menu would sometimes disappear when working with certain datasets.

## Version 1.4.1
### Bugfixes
- Fixed an issue causing data export (ie. to CSV or Parquet) to fail when debugging a Python file.

## Version 1.4.0
### Updates
- Added basic support for displaying nested DataFrames and Series in the grid as text.
- Added support for GPU-backed and sparse PyTorch tensors.
- When exporting to CSV, the data index will now be included if it has been changed from the default index (for example if `set_index` has been used).
- Custom operations now use isolated scoping. This means that variables declared in operations are now fully isolated from one another and can be easily undone when the operation is removed.
- Data Wrangler is now supported on local VS Code servers started with `code serve-web`.
- Removed dependency on setuptools. This will remove an extra install step needed for environments that do not have it.

### Bugfixes
- Fixed an issue where backslashes were double-escaped in the code to load data from a file.

## Version 1.2.1
### Bugfixes
- Fixed an issue causing spurious error messages when the new Jupyter extension API is enabled.

## Version 1.2.0
### Updates
- Improved performance of column statistics calculations when working with non-hashable data, especially numpy arrays.
- Added handling for Python `bytes` data with invalid UTF-8 sequences.
- “By Example” operations no longer fail after a timeout and can now be cancelled if it is taking too long. This allows the user to have more flexibility to decide if they want to wait for more complex generations.
- Added support for launching Data Wrangler from the "View Value in Data Viewer" debugger variables context menu for both `.py` and `.ipynb` files. Please ensure that you are using VS Code version 1.90.0 or higher (Insiders only as of May 31 2024) and using the latest `prerelease` version of the Jupyter extension.

### Bugfixes
- Fixed an issue affecting Mac machines where certain input events such as copy pasting and selecting all text were not working in the Viewing mode filter context menu form.
- Fixed an issue that could prevent Data Wrangler from opening on systems with improperly configured locales.
- Fixed an issue where Data Wrangler launch would hang when opening from an interactive notebook with an active debug session.

## Version 1.0.2
### Updates
- Added support for additional DataFrame types.

## Version 1.0.0
### Updates
- **Web support added! 🎉** Data Wrangler is now supported in the browser for notebook entry points. You can try installing the extension in vscode.dev.
- Added support for viewing data from a notebook while in debugging mode.
- Data Wrangler has a vibrant new icon!
- Data Wrangler is now available in 14 display languages supported by Visual Studio Code.
- The “preview” label in the extension name and marketplace entry have been removed.
- Changed .NET to be an optional dependency. When attempting to use "by example" operations for the first time, a prompt will be shown to ask users if they want to install .NET. This should lead to a smoother experience for users who are unable to install .NET in certain environments.
- Added the functionality to delete the most recently committed history step, even when a preview is active on it, which can save time by not requiring discarding the step before deletion.
- One-hot encode now generates code to create columns next to the targets instead of at the end. This makes it easier to verify by not having to scroll to the end of the grid to see the new results.
- Updated the cell status bar entrypoint label to: "Open <variable> in Data Wrangler". This makes it easier for new users to discover.
- Statistics are now displayed with greater precision in the summary panel.
- Added a documentation link in input box for setting up JupyterLab kernels. This will help users who are unfamiliar with Jupyter to set up their environment.
- Several experimental features have been upgraded to a stable state and their associated flags in VS Code settings have been removed. These had previously been enabled by default and so should result in no change for most users.
- Error stack traces are now displayed using a VS Code terminal instead of a text editor. This improves color contrast and enables line highlights to be displayed in some cases.
- Added support for Jupyter extension version 2024.3.2024030101 and above.
- Updated the “Auto Detect Csv Delimiter” experimental setting to be disabled by default.
 
### Accessibility improvements
- Automatically move keyboard focus to the operations panel when an operation is triggered using the grid context menu.
- Improved ARIA role for the "truncate the data" button when loading large files.
- Enable resizing columns in the grid via keyboard by pressing Ctrl + Alt + Left/Right.
- Ensure that focus outlines are visible on disabled toolbar items.
- Improved titles in extension webviews for a clearer experience when using a screen reader.
- Use the application role within webviews for improved accessibility when using a screen reader.
 
### Bugfixes
- Fixed a typo in the settings description for "Start in edit mode for notebook entrypoints" that referred to viewing mode instead of editing.
- Fixed an issue where the Data Viewer would launch in viewing mode even if set to open in editing mode by default.
- Fixed an issue where the "View data" notebook toolbar item was accessible when a non-notebook editor window was focused, but would be unable to load Data Wrangler.
- Fixed an issue where the "View data" notebook toolbar item would disappear when focusing dialog windows.
- Fixed an issue where data loading with nested numpy arrays would crash on load.
- Fixed an issue where an error notification could appear after closing Data Wrangler before it has finished connecting to the runtime.
- Fixed an issue where very large numeric values could lose precision when displayed in the grid or statistics.
- Fixed an issue where the sort and filter commands were available in the command palette even when they should be disabled.
- Fixed an issue where the variable name displayed in the "custom operation" help text could sometimes be incorrect.
- Fixed an issue where one-hot encoding more than one column would not delete all of the original columns.
- Fixed an issue where PyTorch Tensor objects would fail to open in Data Wrangler when opened from a notebook.
- Fixed an issue where notebooks created via export would be unable to open the data viewer without reloading.
- Fixed an issue where the Data Wrangler extension was not being activated for interactive notebooks.


## Version 0.28.0
### Updates
- Progress messages while previewing, undoing, discarding and committing operations now only appear after a short delay. This reduces flickering of notifications when several actions happen in a short time span.
- Added a delayed progress message for the View data toolbar menu item when the kernel is busy to make it clear that there is a pending background task.
 
### Accessibility improvements
- Improved color contrast of various UI controls in some VS Code themes.
- Improved visibility of keyboard focus outlines across the UI.
- The code preview panel will now display the text cursor even when the code is not editable. This enables users to select code more easily using only the keyboard.
- Improved keyboard navigation order for some controls.
 
### Bugfixes
- Fixed an issue where filter was being re-executed when switching from Editing to Viewing mode with the filters panel open.

## Version 0.26.0
### Updates
- Introducing a data viewing mode for Data Wrangler, which integrates into the Jupyter Notebooks data viewer. The new data viewing mode provides a lightweight and faster experience for quickly viewing, sorting and filtering data. This mode is now the default Data Wrangler entrypoint from the notebook, which can be disabled from setting to default back to the original editing mode. To manually enter this mode, select “Viewing” in the mode toggle in the toolbar.
- The data import step can now be edited like any other step when data has been loaded from a file. Some basic arguments have been added including file path, delimiter, and page # for Excel files.
- Added a confirmation dialog when clicking "Back to all operations" for custom operations to warn potential loss of code.
- Improvements to list and dict variable loading support.
- Clicking on the data shape now also reveals the summary panel.

### Accessibility Improvements
- Improved keyboard accessibility for several links and buttons across the UI.
- Improved screen reader announcements after loading data, accepting/rejecting/undoing operations, and more.
- Improved contrast of various UI elements in some themes.
- Added or fixed ARIA labels, roles, and attributes in several places, including:
  - Tree view in the summary panel
  - Sortable lists in sort, filter, and group by operation arguments
    - Argument fields in sort and filter operations
    - Sort and filter buttons in the grid cells and toolbar
    - And more...

### Bugfixes
- No longer shows the "Open source file in basic editor" button for sessions entered from the notebook as it was always disabled.
- Fixed issue where operations found in the search bar required a double click to select.
- Minor theming fixes.

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
