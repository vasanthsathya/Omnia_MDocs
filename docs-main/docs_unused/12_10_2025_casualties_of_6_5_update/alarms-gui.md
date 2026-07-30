---



title: "Alarms"
description: "How to Configure Alarms"
tags: [Monitoring, Alarms]
search:
boost: 2
parent: Monitoring





hide:
- toc
---

# Alarms

**Alarms** are notifications that inform the administrator about changes in the network state. Alarm information is viewed from the **Alarms** navigation panel.

![](media/alarms_nav_6_5.png)

## Active Alarms

Active Alarms are displayed in the **Active Alarms** view. 

![](media/active_alarms_nav_6_5.png)

![](media/active_alarms_window_6_5.png)

Active Alarms are searchable by name and object type using the search field.

![](media/search_alarms_6_5.png)

The **Sort By** feature is used to sort alarms. Alarms are sorted by **Severity** or by their creation time by enabling the **Created** option.

![](media/active_alarms_sort_by.png)

The **Show Masked Alarms** option shows **Masked Alarms** from within the Active Alarms window.


![](media/show_masked_alarms.png)

## Masked Alarms

**Masked Alarms** are alarms that are hidden from the Active Alarms list. You mask an alarm by clicking its Mask Alarm button under the Details column..

![](media/maked_alarm_button.png)

When you mask an alarm, a pop-up box appears with additional options, including **Mask Duration**, which allows you to set a time duration for the alarm mask.

![](media/alarm_masking_options.png)

## Alarm Mask

Masked Alarms are listed under the tab titled **Alarm Mask.**


![](media/alarm_menu_alarm_mask.png)


![](media/alarm_mask_window_6_5.png)




## History

The history of all notifications is displayed in the alarm’s navigation panel under the **History** tab. The History window includes alarms and other notifications such as authentication notifications.

![](media/alarm_history_menu_item.png)

![](media/alarm_history_6_5.png)



## Columns

Each column showcases data pertinent to individual alarm events, with a corresponding description positioned at the top.

![](media/alarm_history_columns.png)

## Filtering

Each column features a form field positioned above it. These form fields enable the filtering of alarm data based on the content of the column. To use the filters, you choose a field(s), input a query, and press **Enter** on your keyboard to apply the filter. In addition to conventional search text, filters also accept Regex and glob patterns.

![](media/alarms_history_filter_6_5.png)

## Before Timestamp

**Before Timestamp** excludes events that happened after a set date. After the fields are set, only events that happened before the selected time value are displayed.

![A screen shot of a number Description automatically generated](media/8beb8bd915428f96bd4468d3ea4c5231.png)


## Type

**Type** filters alarms by their type, which can be **Alarm**, **Event** or **Clear**. Setting the value to **All** shows all items and invalidates the filter.

![](media/filter_type_alarm_history.png)

Messages under Type and Severity are color-coded by **Type**.

![](media/filter_severity_type.png)

## Severity

**Severity** filters alarms by their severity, such as **Critical**, **Error**, **Warning**, or **Notice**. Setting the value to **All** displays all items and disables the filter.

![](media/severity_filter.png)

 

## Amp Key

The **Amp Key** filters alarms by key. The key is placed in brackets at the beginning of the alarm description.

![](media/ampkey_filter.png)



## Error Text

The **Error Text** field filters alarms based on the content of **Error Text** column.

![](media/error_text_alarm_history_filter.png)

## Element

**Element** filters alarms by device name.

![](media/alarm_history_element_filter.png)

## User

The **User** column indicates who triggered an alarm. This field filters alarms by the **User** responsible for them.

![](media/user_alarm_filter.png)

## Site 

!!! Multisite Only 
    This column is only available on *multisite* systems.

The **Site** column indicates the site of the device.



## Search

The search feature at the top of the page allows you to search for any text displayed in the current list of alarms. Any matching text is highlighted in yellow.

![](media/alarm_history_filter_search.png)


## Custom Search Filters

![](media/custom_filter_tools_alarm_history.png)

The **TAIL** tab lets you set the initial state of all filter field values. This is useful because it enables you to create a collection of default filter settings before creating custom search filters.

**Add a Custom Search Filter**

The ![](media/buttons/6.5/alarm_custom_search.png){:class="btn"} button allows you to create a custom search filter. This is a user-defined collection of all filter settings. Multiple custom search filters can be created and toggled between when querying Alarm data.

When custom search filters are created, they are represented as numbered tabs with the word *Search* displayed on them. Clicking these tabs anywhere other than on the displayed “x” selects them and populates the fields with the assigned values. Clicking the “x“ deletes the search template and removes it from the list. Clicking **Tail** after creating or selecting a custom search will revert the filter values to the state saved via the **Tail** tab.

![](media/custom_search_tabs_alrm_history.png)

**Copy a Custom Search Filter**

The ![](media/buttons/6.5/alarm_clone_filter_button.png){:class="btn"}  button allows you to clone all filters from the currently active view window. The clone is presented as a newly created active tab.



## Navigating Rows

The **Navigate Rows** buttons allow you to scroll through the alarm history view, from the newest to the oldest alarms.

![](media/navigation_alarm_history_bottom_controls.png)


## Growl History

Growls are errors that occur between the client browser and the Verity orchestration platform. Holding the mouse over the growl gives the user more detail about the error. 



![](media/alarms_growl_history_menu.png)

![](media/growl_history_6_5.png)
