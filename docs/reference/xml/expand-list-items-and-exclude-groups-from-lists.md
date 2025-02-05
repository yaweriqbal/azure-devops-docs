---
title: Expand list items and exclude groups from lists
titleSuffix: TFS
description: Examples for expanding pick list items and restricting items using expanditems and filteritems attributes - Team Foundation Server (TFS)
ms.technology: devops-agile
ms.custom: process
ms.assetid: 860a4118-f155-4c6b-9d80-d8a72a8b219f
ms.author: kaelli
author: KathrynEE
monikerRange: '< azure-devops' 
ms.date: 05/10/2017
---

# Expand list items and exclude groups from lists

[!INCLUDE [temp](../../includes/customization-phase-0-and-1-plus-version-header.md)]

You can expand and filter lists by using the `expanditems` and `filteritems` attributes. You can apply these attributes to these list type elements: `ALLOWEDVALUES`, `SUGGESTEDVALUES`, and `PROHIBITEDVALUES`.  
  
To better understand how these attributes are used to populate a field's drop-down menu, review the examples provided below.  

<a name="ExpandListsAndGroups"></a> 
  
##  Expand lists and groups  
 You can assign the values `true` and `false` to `expanditems`; its value is `true` by default. When `expanditems` has the value of `true`, list items that represent groups or global lists are expanded recursively. A group's subgroups are expanded; the subgroups of those subgroups are also expanded, and continues in this pattern. After expansion, list items that represented groups include both groups and users as list item values. If `expanditems` is set to `false`, no group or global list expansion is performed.  

<a name="FilterListsAndGroups"></a> 
  
##  Exclude groups  
 You can assign only the value `excludegroups` to the `filteritems` attribute. When this attribute appears, all the list items are evaluated and any groups are removed. Use the `filteritems` attribute to show only users, not groups.  

<a name="ContentsOfListsAndGroups"></a> 
  
##  Contents of lists and groups used in the examples  
 The examples provided in this topic use the following values:  
  
<table>
<tbody valign="top">
<tr>
<th scope="col"><p>Group name and list</p></th>
<th scope="col"><p>Description</p></th>
</tr>
<tr>
<td>
[Project]\Business Analysts</p>
<ul> 
<li>JayHamlin</li>
<li>PilarAckerman</li>
<li>ReshmaPatel</li>
</ul> 
</td>
<td> 
<p>A project group that contains the names of three business analyst team members.</p>

<p><strong>Note:</strong> Use the literal prefix [Project] instead of using the actual name of the project.</p>
</td>
</tr>
<tr>
<td>
<p>Example1\MyReports</p>
<ul> 
<li>Development</li>
<li>devuser</li>
<li>Test</li>
<li>Test user</li>
<li>Program Management</li>
<li>pmuser</li>
<li>juser</li>
</ul> 
</td>
<td> 
<p>A project group that contains one team member, juser, and three subgroups, where each subgroup contains the name of one team member.</p>
</td>
</tr>
<tr>
<td>
<p>Example1\MyReports</p>
<ul> 
<li>UserOne</li>
<li>UserTwo</li>
<li>UserThree</li>
<li>MyRemotes</li>
<li>UserFour</li>
<li>UserFive</li>
</ul> 
</td>
<td>
<p>A project group that contains the names of three team members and one subgroup which contains the names of two team members.</p>
</td>
</tr>
<tr>
<td>
<p>BoolValues</p>
<ul> 
<li>true</li>
<li>false</li>
</ul> 
</td>
<td>
<p>A global list with two entries.</p>
</td>
</tr>
</tbody>
</table>

## Example: Expand lists and exclude groups

In this example, the field contains a string value, a group, and a global list. At the time it is run, the list is expanded and groups are excluded.

<table>
<thead>
<tr>
<th ><p>Example</p></th>
<th ><p>Drop down list values</p></th>
</tr>
</thead>
<tbody valign="top">
<tr>
<td>

<pre><code>&lt;ALLOWEDVALUES expanditems="true" filteritems="excludegroups"&gt; 
   &lt;LISTITEM value="string" /&gt; 
   &lt;LISTITEM value="[Project]\Business Analysts" /&gt;  
   &lt;GLOBALLIST name="BoolValues" /&gt; </code></pre>


</td>

<td data-th="Drop-down list values">

<ul> 
<li>string</li>
<li>true</li>
<li>false</li>
<li>JayHamlin</li>
<li>PilarAckerman</li>
<li>ReshmaPatel</li>
</ul> 
</td>
</tr>
</table> 


<a id="Example2"></a>
## Example: Expand lists and groups and do not filter

In this example, the field contains a string value, two groups, and a global list. At the time it is run the list is expanded and groups are not excluded.

<table>
<tr>
<th scope="col"><p>Example</p></th>
<th scope="col"><p>Drop-down list values</p></th>
</tr>

<tr valign="top">
<td data-th="Example">

<pre><code>&lt;ALLOWEDVALUES expanditems="true"&gt;
   &lt;LISTITEM value="string" /&gt;
   &lt;LISTITEM value="Example1\MyReports"/&gt;
   &lt;LISTITEM value="Example1\MyTeam" /&gt;
   &lt;GLOBALLIST name="BoolValues" /&gt;
&lt;/ALLOWEDVALUES&gt; 
</code></pre>
</td><td data-th="Drop-down list values">

<ul> 
<li>string</li>
<li>true</li>
<li>false</li>
<li>juser</li>
<li>juser2</li>
<li>devuser</li>
<li>testuser</li>
<li>pmuser</li>
<li>Development</li>
<li>Test</li>
<li>Program Management</li>
</ul> 
</td></tr>
</table>



## Example: Do not expand lists or groups, and do not filter

In this example, the field contains a string value, two groups, and a global list. At run time, the list is not expanded and groups are not filtered out. This means that group names are displayed, but not the users within those groups.

> [!NOTE]    
>The global list name and contents are not displayed.


<table>
<tr>
<th scope="col"><p>Example</p></th>
<th scope="col"><p>Drop-down list values</p></th>
</tr>

<tr valign="top">
<td data-th="Example">

<pre><code>&lt;ALLOWEDVALUES expanditems="false"&gt;
   &lt;LISTITEM value="string" /&gt;
   &lt;LISTITEM value="Example1\MyReports"/&gt;
   &lt;LISTITEM value="Example1\MyTeam" /&gt;
   &lt;GLOBALLIST name="BoolValues" /&gt;
&lt;/ALLOWEDVALUES&gt; 
</code></pre>
</td>
<td data-th="Drop-down list values">

<ul> 
<li>string</li>
<li>MyTeam</li>
<li>MyReports</li>
</ul> 
</td>
</tr></table> 


## Example: Expand lists and exclude groups and global lists
In this example, the field contains a string value, one group, and a global list. At run time, the list is expanded and groups are filtered out.

> [!NOTE]    
>*MyTeam* is a group that is excluded and not expanded, and *BoolValue*s is a global list, so neither one is expanded or shown.

<table><tr><th scope="col"><p>Example</p></th><th scope="col"><p>Drop-down list values</p></th></tr><tr><td data-th="Example">


<pre><code>&lt;ALLOWEDVALUES expanditems="true" filteritems="excludegroups"&gt;
   &lt;LISTITEM value="string" /&gt;
   &lt;LISTITEM value="Example\MyTeam" /&gt;
   &lt;GLOBALLIST name="BoolValues" /&gt;
&lt;/ALLOWEDVALUES&gt; 
</code></pre>
</td><td data-th="Drop-down list values"><p>String</p></td></tr></table>

  
## Related articles 
-  [ALLOWEDVALUES, SUGGESTEDVALUES, and PROHIBITEDVALUES XML elements](define-pick-lists.md)   
-  [GLOBALLIST XML element reference](define-global-lists.md)   
-  [Rules and rule evaluation](../../organizations/settings/work/rule-reference.md)