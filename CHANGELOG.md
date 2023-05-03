# Changelog

## Version 0.8.0
**Updates**:
* In "Find and replace" operation, surface a form field error if the "Old value" field is left empty.
* Improve readability of code example in code editor placeholder text by showing df = df.drop(columns=['ColumnName']) instead of df = drop('ColumnName', axis=1)
* Removed the `inplace=True` and `copy=False` parameters from generated pandas code, as those aren't considered best practice and are being considered for deprecation in Pandas.
* Improved support for all VS Code themes.

**Bugfixes**:
*	In "Find and replace" operation, preserve the contents of fields "Old value" and "New value" when "Target columns" is changed.
* Fixed an issue where timestamps ignored time zone information when displayed in the grid.
*	Fixed an issue for the context menu to disable the context menu operations when required.
*	Fixed issue where the operation panel collapses when clicking on the grid.
*	Fixed an issue where errors may not be caught in some cases when using IPython version 8.12.1 or above.

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
