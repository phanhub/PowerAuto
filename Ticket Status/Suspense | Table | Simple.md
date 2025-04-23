### Table of TIckets 
<li>Specific Category</li> 
<li>Suspense Datest</li> 
<li>Ordered by Older to Newer/Nearest due date</li>  

## Scenario | Tickets for Requesting for Information

<details>
<summary>  SharePoint | Get-Items</summary>
  
|  |  | Example |
|-------:|-------------------|---------------|
|Site Address | Select the path | https://XXXX.sharepoint.com/sites/XXX |
|List Name| Select the sub folder | Master List |
|Filter Query| Defining the desired | (ReportingStatus eq 'ENTER_CATEGORY') and (ContentType ne 'ABC') and (ContentType ne 'DEF or GHI') and (ContentType ne 'Incident or Event') | 
|Limit Column by View | Select Sub category | Open RFI | 
|Order By | | Suspense_x0000_Date asc
  
</details>

<details>
<summary>Apply to Each</summary>
  
| Field Name                       | Description                               | Example Code Snippet                                                                                             |
|----------------------------------|-------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| Value                            | Select Value from the SharePoint List     | ![image](https://github.com/user-attachments/assets/da34d095-5b88-4d15-aefd-3175bb7b37c8)                        |
| Append to String Variable<br>Select "Convert" | <ul><li>Starting Midnight</li><li>UTC to EST</li><li>Format</li><li>Hyperlink</li><li>Published to Completed</li></ul> |

```javascript
concat(  
  '<tr><td>', items('Apply_to_each_2')?['ItemInternalId'], ' | ',
  if(equals(items('Apply_to_each_2')?['Suspense_x0020_Date'], null), '', 
  formatDateTime(convertTimeZone(items('Apply_to_each_2')?['Suspense_x0020_Date'], 'UTC', 'Eastern Standard Time'), 'M/d h:mm tt')), ' | ',
  '<a href="', items('Apply_to_each_2')?['{Link}'], '">',
  items('Apply_to_each_2')?['Title'], '</a>', ' | ',
  items('Apply_to_each_2')?['IncidentNumber'],
  '</td></tr>')
```


</details>

