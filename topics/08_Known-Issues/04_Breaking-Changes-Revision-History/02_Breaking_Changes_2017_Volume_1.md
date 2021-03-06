﻿<!--
|metadata|
{
    "fileName": "breaking-changes-2017-volume-1",
    "controlName": "",
    "tags": ["Breaking Changes","Known Issues"]
}
|metadata|
-->

# Breaking Changes 2017 Volume 1

The following topic summarizes the breaking changes of the 2017 Volume 1 release.

## General

### Split of the Infragistics Util file

From version 17.1 the `infragistics.util.js` file has been split into a non-jQuery specific file and jQuery specific files. The new structure is the following:

-   `infragistics.util.js` - holds only utility functions that do not depend on jQuery framework.
-   `infragistics.util.jquery.js` - holds jQuery dependant utility functions.
-   `infragistics.util.jquerydeferred.js` - custom CommonJS Promises/A implementation, for users that are using versions of the jQuery, prior to version 1.5, which doesn't support $.Deferred.

For applications that are using the igLoader to load %%ProductName%% controls' dependencies, no change is required, because the loader is handling this internally. The other applications that load manually the files, may take advantage and not include the unnecessary utility references.

There is a new, jQuery dependant file, explicitly needed for Ignite UI DV components - `infragsitics.dv_jquerydom.js`. It needs to be loaded prior to the `infragistics.dv_core.js` dependancy.

```
...
<script src="js/modules/infragistics.dv_jquerydom.js"></script>
<script src="js/modules/infragistics.dv_core.js"></script>
...
```

#### Related Topics
-   [JavaScript Files in %%ProductName%%](Deployment-Guide-JavaScript-Files.html)

### New Bootstrap themes structure

The default and all Bootstrap 3 based themes have moved under a common "/bootstrap3" folder. The following lists the current Bootstrap 3 themes currently shipped with %%ProductName%% and the location of the `infragistics.theme.css` relative to the product source root ("~"):


Themes | Previous path | New Path
-------|---------------|---------
Bootstrap 3 (default) |  ~/css/themes/bootstrap/ | ~/css/themes/bootstrap3/
Flatly | ~/css/themes/flatly/ | ~/css/themes/bootstrap3/flatly/
Yeti | ~/css/themes/yeti/ | ~/css/themes/bootstrap3/yeti/
Superhero | ~/css/themes/superhero/ | ~/css/themes/bootstrap3/superhero/

So for pages referencing the current Yeti theme for example, the new link becomes:
```html
<link href="/css/themes/bootstrap3/yeti/infragistics.theme.css" rel="stylesheet" type="text/css" />
```
Or if using the Infragistics Loader with [`theme`](%%jQueryApiUrl%%/ig.loaderClass#options:settings.theme) option:

```js
$.ig.loader({
    //...
    theme: "bootstrap3/yeti"
});
```

## igGrid

### headerText option behavior changes
When headerText option is not set in columns definition of the grid, then column key is used as header text.

### Options changes in igGrid Summaries
The options [*isGridFormatter*](http://www.igniteui.com/help/api/2016.2/ui.iggridsummaries#options:isGridFormatter) and [*defaultDecimalDisplay*](http://www.igniteui.com/help/api/2016.2/ui.iggridsummaries#options:defaultDecimalDisplay) in the igGrid Summaries main level options have been removed.
The [*isGridFormatter*](http://www.igniteui.com/help/api/2016.2/ui.iggridsummaries#options:columnSettings.summaryOperands.isGridFormatter) and [*decimalDisplay*](http://www.igniteui.com/help/api/2016.2/ui.iggridsummaries#options:columnSettings.summaryOperands.decimalDisplay) options under [columnSettings.summaryOperands](http://www.igniteui.com/help/api/2016.2/ui.iggridsummaries#options:columnSettings.summaryOperands) have been removed as well.

The new [*format*](%%jQueryApiUrl%%/ui.iggridsummaries#options:columnSettings.summaryOperands.format) option in the igGrid Summaries can be used now in conjunction with the column [*format*](%%jQueryApiUrl%%/ui.iggrid#options:columns.format) and [*autoFormat*](%%jQueryApiUrl%%/ui.iggrid#options:autoFormat) options to determine how the summary would be formatted.

With this option can be set how many decimals after the floating point will be displayed similar to the deleted *decimalDisplay* option. If the [*format*](%%jQueryApiUrl%%/ui.iggridsummaries#options:columnSettings.summaryOperands.format) option for the summaryOperand is not set the format for the summary will be taken based on the column it is displaying for, meaning if that column has set [*format*](%%jQueryApiUrl%%/ui.iggrid#options:columns.format) - that format will be taken into account.

If no format is set for the summary and the current column the regional settings for the column type will be applied to that summary. Since due to [*autoFormat*](%%jQueryApiUrl%%/ui.iggrid#options:autoFormat) being default to 'date', the regional settings will be applied only to summaries in that type of column and in other type of columns won't receive any formatting. Meaning that if regional settings need to be applied for other type of columns when the *format* option is not set for both summary and column the [*autoFormat*](%%jQueryApiUrl%%/ui.iggrid#options:autoFormat) option needs to be set. It will specify which summaries will receive the regional auto formatting depending the column they are in.

### Date handling

The option [`enableUTCDates`](%%jQueryApiUrl%%/ui.iggrid#options:enableUTCDates) has now a different function. It affects only the dates serialization. You should use the new option [`dateDisplayType`](%%jQueryApiUrl%%/ui.iggrid#options:columns.dateDisplayType) in the grid column's definition to handle date timezone display. Please follow the [Migrating enableUTCDates option after 17.1](migrating-enableutcdates-option-in-17-1.html) topic to see how you can adapt to the new changes and the [Using Ignite UI controls in different time zones](Using-IgniteUI-controls-in-different-time-zones.html) topic for more detailed information of how the both options work.

## igDateEditor/igDatePicker

The option [`enableUTCDates`](%%jQueryApiUrl%%/ui.igdateeditor#options:enableUTCDates) has now a different function. You can use the [`displayTimeOffset`](%%jQueryApiUrl%%/ui.igdateeditor#options:displayTimeOffset) if you want to show the time in the editor with the desired offset. Please follow the [Migrating date handling in 17.1](igDateEditor-migrating-date-handling-in-17-1.html) topic to see how you can adapt to the new changes and the [Using Ignite UI controls in different time zones](Using-IgniteUI-controls-in-different-time-zones.html) topic for more detailed information of how the both options work.

## igNumericEditor

In previous versions of the product, if user sets or enters a value in a numeric editor that has more decimal places than the one defined in the `maxDecimals` option, then the value was truncated. E.g. If an editor with defined 'maxDecimals' to `3`, receives a value `123.4567`, then it will be truncated to `123.456`. With version 17.1 of the product, a new option [`roundDecimals`](%%jQueryApiUrl%%/ui.ignumericeditor#options:roundDecimals) is introduced, which is enabled by default and rounds the numeric values, using the JavaScript `Math.round()` function. This means that the value of `123.4567` will be rounded and displayed in the editor as `123.457`. If the [`roundDecimals`](%%jQueryApiUrl%%/ui.ignumericeditor#options:roundDecimals) is disabled, then it will truncate the value and will show it as `123.456`, like in the old versions.