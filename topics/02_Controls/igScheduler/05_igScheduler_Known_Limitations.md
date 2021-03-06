<!--
|metadata|
{
    "fileName": "igscheduler-known-limitations",
    "controlName": "igScheduler",
    "tags": ["Known Issues","Tips and Tricks"]
}
|metadata|
-->

# Known Issues and Limitations (igScheduler)


## Known Issues and Limitations Summary


### Known issues and limitations summary chart

The following table summarizes the known issues and limitations of the `igScheduler`™ control. Detailed explanations of some of the issues and the existing workarounds are provided after the summary table.

Legend | Description |
---|---|---
![](../../images/images/positive.png) | Workaround available
![](../../images/images/negative.png) | No known workaround
![](../../images/images/plannedFix.png) | No known workaround, fix planned

Below are listed all current limitations for the initial version of the `igScheduler` widget.

Issue | Description | Status
---|---|---
[Time-zone offsetting](#NoTimeZoneOffsetting) | Time-zone offset settings details|![](../../images/images/negative.png)
[Custom color scheme](#NoCustomColorScheme) | Pre-defined custom color scheme is used |![](../../images/images/negative.png)
[Templating](#NoTemplating) | Templating and changing of appointment appearance is not supported |![](../../images/images/negative.png)
[ARIA support for appointments in calendar (Canvas)](#ARIASupport) | No ARIA support for appointments in calendar (Canvas) |![](../../images/images/negative.png)
[First day of the week setting](#FirstDayOfWeek) | First day of the week settings are set to `Sunday` by design |![](../../images/images/negative.png)
[Using of remote datasource is not supported](#remoteDS) | Local data source should be used. |![](../../images/images/negative.png)
[Swipe-gestures support](#SwipeGesture) | No swipe-gestures support |![](../../images/images/negative.png)
[Tab navigation to appointment popover](#NavigationToAppointmentPopover) | No tab navigation to appointment popover |![](../../images/images/negative.png)
[Min width support – 320 px](#MinWidthSupport) | Minimum width resolution support on mobile devices is 320 px |![](../../images/images/negative.png)
[Setting the views option through MVC wrapper.](#MVCWrappers) | Configuring the views option through the ASP.NET MVC wrapper does not take effect.  |![](../../images/images/plannedFix.png)


## Known Issues and Limitations Details


### <a id="NoTimeZoneOffsetting"></a>No time-zone offset settings

Time in the `igScheduler` is always shown according to the current browser offset (hours). Currently the scheduler does not support showing times in a different zone than the browser's time zone.

### <a id="NoCustomColorScheme"></a>No custom color scheme

A pre-defined color scheme with twelve colors is provided by the scheduler, which cannot be changed by the end user.

![](images/preDefinedColors.png)


### <a id="NoTemplating"></a>No templating

Currently it is not possible to customize the appearance of the scheduler events by using templates.

### <a id="ARIASupport"></a>igScheduler ARIA support
Scheduler appointments are visualized using canvas which could not be processed by screen readers. Consider listing selected appointments separately, in igGrid for instance, for accessibility purposes.

The list below provides links to more details related to how WAI-ARIA support has been implemented in Widgets that are part of the scheduler.

- [igDatePicker](igdatepicker-accessibility-compliance.html#wai-aria)
- [igDateEditor](igdateeditor-accessibility-compliance.html#wai-aria)
- [igTextEditor](igtexteditor-accessibility-compliance.html#wai-aria)

### <a id="FirstDayOfWeek"></a>No first day of the week setting

Sunday is used as the first day of the week by default and currently we do not expose an option that could be used to set a different day of the week (e.g. Monday).

### <a id="remoteDS"></a>Binding to a remote datasource is not supported
Currently igScheduler can handle only local datasource.

### <a id="SwipeGesture"></a>No swipe-gestures support

Currently the `igScheduler` doesn't have swipe gestures support for actions like `swipe left` or `swipe right` for example.

### <a id="NavigationToAppointmentPopover"></a>No tab navigation to appointment popover

There is accessibility limitation with `tab navigation` and `selection` of appointment, by using the keyboard.

### <a id="MinWidthSupport"></a>Min width support – 320 px (Mobile environment)

`320 pixels` is the minimum resolution under which `igScheduler` will be fully visible with properly aligned html elements. This applies for mobile devices.

For next releases it is planned to add a message that will be shown when minimum resolution is reached.

### <a id="MVCWrappers"></a>Setting views option though MVC wrapper is not possible.

Using the `views` option exposed by the MVC wrapper to control which views(`Agenda`, `Week`, `Day`, `Month`) are initialized does not work. This will be implemented for the next scheduler version.

