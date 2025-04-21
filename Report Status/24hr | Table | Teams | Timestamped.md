## Retrieving reports from the past 24 hours
Include statuses such as pending, rejected, or published, and exporting the data into a table with the following columns: Date Created | Title (with hyperlink) | Status | Published Time
![image](https://github.com/user-attachments/assets/2edc8328-4023-43f4-bc64-2953629debb6)

### SharePoint | Get-Items
![image](https://github.com/user-attachments/assets/724f6029-ae5c-4894-85b2-c2a83288e677)

|  |  | Example |
|-------:|-------------------|---------------|
|Site Address | Select the path | https://XXXX.sharepoint.com/sites/XXX |
|List Name| Select the sub folder | Reports              |
|Filter Query| Created items at the behinning of the day on EST | (Created ge '@{startOfDay(addDays(convertTimeZone(utcNow(), 'UTC', 'Eastern Standard Time'), -1))}') and (ReportType eq 'PhanHub Mail') | 
|Limit Column by View | Select Sub category | All PhanHub Mail | 

### Apply to Each

| Field Name                         | Description                                 | Example Code Snippet                                                                                           |
|------------------------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Value                              | Select Value from the SharePoint List       | ![image](https://github.com/user-attachments/assets/da34d095-5b88-4d15-aefd-3175bb7b37c8)                                                                                                                                                                                                                                     |
| Append to String Variable <br> Select "Convert" | <ul><li>Starting Midnight</li><li>UTC to EST</li><li>Format</li><li>Hyperlink</li><li>Published to Completed</li></ul> | ```concat( '<tr><td>', formatDateTime(convertTimeZone(items('Apply_to_each_4')?['Created'], 'UTC', 'Eastern Standard Time'), 'M/d'), '</td><td><a href="', items('Apply_to_each_4')?['{Link}'], '">', items('Apply_to_each_4')?['Title'], '</a></td><td>', items('Apply_to_each_4')?['ApprovalStatus/value'], '</td><td>', if(equals(items('Apply_to_each_4')?['Date_x0020_Published'], null), '', formatDateTime(convertTimeZone(items('Apply_to_each_4')?['Date_x0020_Published'], 'UTC', 'Eastern Standard Time'), 'h:mm tt')), '</td></tr>' ) ``` ![image](https://github.com/user-attachments/assets/b0ba9365-bdc6-49bb-8b19-e0f0e53af56d) |

### Compose
| Field Name         | Description             | Example Code Snippet                                                                                                                                                                                                                                                                                                                               |
|---------------------|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Table format and headers | Defines the structure and appearance of the table | ```<table style='border-collapse: collapse; width: 100%;'> <tr style='background-color: #002060;'> <th style='border: 1px solid black; padding: 8px; color: #FFFFFF; width: 10%;'>Date</th> <th style='border: 1px solid black; padding: 8px; color: #FFFFFF; width: 80%'>TITLE w/Link</th> <th style='border: 1px solid black; padding: 8px; color: #FFFFFF;'>Status (Pending/Completed)</th> <th style='border: 1px solid black; padding: 8px; color: #FFFFFF;'>Notes</th> </tr> @{variables('Convert')} </table>``` ![image](https://github.com/user-attachments/assets/8d118677-cd01-494f-ac6b-8412ff23c2b6) |

### Post Message in Teams Chat
@{outputs('Compose')}
