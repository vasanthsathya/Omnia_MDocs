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

**Alarms** notify the administrator about problems within the system. The administrator accesses alarm information from the Alarms navigation panel.

![](media/alarms_options_alarms_selected.png)

The following settings—Thresholds, Threshold Groups, and Grouping Rules—are available in **Templates → Alarms**.

![](media/threshold_alarms_list.png)

The **Thresholds** feature consists of three sections that work together: **Thresholds**, **Threshold Groups**, and **Grouping Rules**. Together, these create automated notifications that alert administrators when specific metrics exceed, fall below, or meet certain conditions in your network infrastructure.

## Thresholds
**Thresholds** allows administrators to create multiple threshold rules, each monitoring a specific metric with configurable conditions (greater than, less than, equals, etc.) and severity levels.

## Grouping Rules

**Grouping Rules** are collections of logical rules that determine which ports and hardware devices to select. 

## Threshold Groups

**Threshold Groups**  is where metric watching is applied to devices and ports. This section is composed of two lists: Targets and Thresholds.

- **Targets** is where you assign the rules created in the Grouping Rules section.

- **Thresholds** is where you assign the rules created in the Thresholds section.

![](media/threshold_group_example.png)

<!-- In the example image below, a Threshold is created for CPU usage.


![](media/cpu_threshold_example.png)

 -->


**Active Alarms** convey immediate problems occurring in the network right now. The Active Alarms window displays these alarms. A red background highlights the number of active alarms next to the Alarms Main Navigation tab. ![](media/magnified_red_active_alarms_notification.png){:class="pop"}

![](media/alarms_options_alarms_selected-alarms.png)

![](media/alarms_6_6_page.png)

Active Alarms are searchable by name and object type using the search field.

![](media/search_alarms_6_5.png)

The **Sort By** feature is used to sort alarms. Alarms are sorted by **Severity** or by their creation time by enabling the **Created** option.

![](media/active_alarms_sort_by.png)

The **Show Masked Alarms** option shows **Masked Alarms** from within the Active Alarms window.


![](media/show_masked_alarms.png)

# Alarm Mask

**Alarm Mask** lists Masked Alarms.

![](media/alarms_options_alarms_selected-alarm-mask.png)


![](media/alarm_mask_window_6_6.png)

## Masked Alarms

**Masked Alarms** hide from the Active Alarms list. To mask an alarm, click its Mask Alarm button under the **Details** column in the Active Alarms window.

![](media/maked_alarm_button.png)

When you mask an alarm, a pop-up box appears with additional options, including **Mask Duration**, which lets you set a time duration for the alarm mask.

![](media/alarm_mask_pop_up.png)

# Alarm History


While **Active Alarms** notify administrators of immediate problems, **History** records previously resolved issues and tracks less pressing notifications such as user logins.

![](media/alarms_options_alarms_selected-history.png)





## Columns

Each column showcases data pertinent to individual alarm events, with a corresponding description positioned at the top.

![](media/alarm_history_main_window_6_6_.png)

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

 

## AMP Key

The **AMP Key** filters alarms by key. The key is placed in brackets at the beginning of the alarm description.

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

![](media/alarm_search.png)


## Custom Search Filters

![](media/custom_filter_tools_alarm_history.png)

The **TAIL** tab lets you set the initial state of all filter field values. This is useful because it enables you to create a collection of default filter settings before creating custom search filters.

**Add a Custom Search Filter**

The ![](media/buttons/6.5/alarm_custom_search.png){:class="btn"} button allows you to create a custom search filter. This is a user-defined collection of all filter settings. Multiple custom search filters can be created and toggled between when querying Alarm data.

When custom search filters are created, they are represented as numbered tabs with the word *Search* displayed on them. Clicking these tabs anywhere other than on the displayed “x” selects them and populates the fields with the assigned values. Clicking the “x“ deletes the search template and removes it from the list. Clicking **Tail** after creating or selecting a custom search will revert the filter values to the state saved via the **Tail** tab.

![](media/custom_search_tabs_alrm_history.png)

**Copy a Custom Search Filter**

The ![](media/buttons/6.5/alarm_clone_filter_button.png){:class="btn"}  button allows you to clone all filters from the currently active view window. The clone is presented as a newly created active tab.


#  Growl History

**Growl History** lists all system Growls. Growls are errors that occur between the client browser and the Verity orchestration platform. Hovering the mouse over a growl displays more detail about the error.

![](media/alarm_growl_history.png)

![](media/growl_history_6_5.png)