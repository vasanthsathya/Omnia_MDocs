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

**Alarms** are notifications that inform the administrator about changes in the network state.

![](media/alarms_6_5_diagram_2.png)

### Viewing Alarms

Alarms are displayed in the **Alarms** view. 

![](media/alarms_alarm_menu_diagram_6_5.png)

![](media/alarms_window_6_5.png)

Alarms are searchable by name and object type using the search field.

![](media/cdb71fbe5d7ce85cdcec0f9507ab03dd.png)

The **Sort By** feature is used to sort alarms. Alarms are sorted by **Severity** or by their creation time by enabling the **Created** option.

![](media/3b1bb4dca2b54a4008a0913454dccf2a.png)


### Alarm Table Columns
| Header | Value |
| - | - |
| Type | **Type** filters alarms by their type, which can be **Alarm**, **Event** or **Clear**. Setting the value to **All** shows all items and invalidates the filter. ![](media/ccddcae166fb613dffd11f99303646ba.png){: class="pop"} Messages under Type and Severity are color-coded by **Type**. ![](media/ccf8f62341a0fc2d2842192bddc9a8e8.png){: class="pop"} |
| Severity | **Severity** filters alarms by their severity, such as **Critical**, **Error**, **Warning**, or **Notice**. Setting the value to **All** displays all items and disables the filter. ![](media/e6a8f23dfbfb8ee9b86e8fb656461b03.png){: class="pop"}|
| Amp Key | The **Amp Key** filters alarms by key. The key is placed in brackets at the beginning of the alarm description. ![](media/5766682f2d451d477525e8643ab3c492.png){: class="pop"} |
| Error Text | The **Error Text** field filters alarms based on the content of **Error Text** column. ![](media/cf28ec7a8ee6f54f4b9d67141e39ad1e.png){: class="pop"} |
| Element | **Element** filters alarms by device name. ![](media/eb6628cc40936bbd474986f5c280386f.png){: class="pop"} |
| User | The **User** column indicates who triggered an alarm. This field filters alarms by the **User** responsible for them. ![](media/362f62a7ed1a99b46fb4a8d9320393b5.png){: class="pop"} |
| Site | This column is only available on *multisite* systems. The **Site** column indicates the site of the device. ![](media/alarms_site_field.png){: class="pop"} |

### Masked Alarms

**Masked Alarms** are alarms that are hidden from the Active Alarms list. You mask an alarm by clicking its Mask Alarm button.

![](media/mask_alarm_6_5.png)

When you mask an alarm, a pop-up box appears with additional options, including **Mask Duration**, which allows you to set a time duration for the alarm mask.

![](media/alrms__masking_prompt_6_5.png)

### Alarm Mask

Masked Alarms are listed under the tab titled **Alarm Mask.**

**![](media/alarm_mask_6_5_tile.png)**

**Show** **Mask Alarms** allows you to view all masked alarms from within the Active Alarms display.

**![](media/76698434d66ddbfbde73be878bb060d8.png)**

### History

The history of all notifications is displayed in the alarm’s navigation panel under the **History** tab.

![](media/alrm_history_6_5_tile.png)


### Filtering

Each column features a form field positioned above it. These form fields enable the filtering of alarm data based on the content of the column. To use the filters, you choose a field(s), input a query, and press **Enter** on your keyboard to apply the filter. In addition to conventional search text, filters also accept Regex and glob patterns.

![](media/42b31338ff190c43c557115a1fca4e30.png)

### Before Timestamp

**Before Timestamp** excludes events that happened after a set date. After the fields are set, only events that happened before the selected time value are displayed.

![](media/8beb8bd915428f96bd4468d3ea4c5231.png)



### Search

The search feature at the top of the page allows you to search for any text displayed in the current list of alarms. Any matching text is highlighted in yellow.

![](media/a653fb203333566bfaa793f72a4fd276.png)

### Empty and Unassigned Fields
To search for empty or unassigned objects, use - as a search term. 

![](media/alarms_search_empty_items.png)


### Custom Search Filters

![](media/ca1433cf9fa8695094a8323a78a7162c.png)

The **TAIL** tab lets you set the initial state of all filter field values. This is useful because it enables you to create a collection of default filter settings before creating custom search filters.

**Add a Custom Search Filter**

The ![](media/df9adfd203ac3472bd0e7e5ea91c1b98.png){:class="btn"} button allows you to create a custom search filter. This is a user-defined collection of all filter settings. Multiple custom search filters can be created and toggled between when querying Alarm data.

When custom search filters are created, they are represented as numbered tabs with the word *Search* displayed on them. Clicking these tabs anywhere other than on the displayed “x” selects them and populates the fields with the assigned values. Clicking the “x“ deletes the search template and removes it from the list. Clicking **Tail** after creating or selecting a custom search will revert the filter values to the state saved via the **Tail** tab.

![](media/c747c1e30ea13a616508a04d5200fa14.png)

**Copy a Custom Search Filter**

The ![](media/8fcca6c27af96e4551fe8d170484c04e.png){:class="btn"}  button allows you to clone all filters from the currently active view window. The clone is presented as a newly created active tab.



### Navigating Rows

The **Navigate Rows** buttons allow you to scroll through the alarm history view, from the newest to the oldest alarms.

![](media/alarm_history_bar.png)