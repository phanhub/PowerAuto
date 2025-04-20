## Retrieving reports from the past 24 hours
Include statuses such as pending, rejected, or published, and exporting the data into a table with the following columns: Date Created | Title (with hyperlink) | Status.

### SharePoint | Get-Items
|  |  | Example |
|-------:|-------------------|---------------|
|Site Address | Select the path | https://XXXX.sharepoint.com/sites/XXX |
|List Name| Select the sub folder | Reports              |
|Filter Query| Created items at the behinning of the day on EST | (Created ge '@{startOfDay(addDays(convertTimeZone(utcNow(), 'UTC', 'Eastern Standard Time'), -1))}') and (ReportType eq 'PhanHub Mail') | 
|Limit Column by View | Select Sub category | All PhanHub Mail | 

### Apply to Each 
|  |  | Example |
|-------:|-------------------|---------------|
| Value | Seelect Value from the SharePoint List | 
|Append to string Variable | Select Convert | concat(
  '<tr><td>',
  if(equals(items('Apply_to_each')?['Date_x0020_Published'], null), '', formatDateTime(convertTimeZone(items('Apply_to_each')?['Date_x0020_Published'], 'UTC', 'Eastern Standard Time'), 'M/dd')),
  '</td><td><a href="',
  items('Apply_to_each')?['{Link}'],
  '">',
  items('Apply_to_each')?['Title'],
  '</a></td><td>',
  if(equals(items('Apply_to_each')?['ApprovalStatus/value'], 'Published'), 'Completed', items('Apply_to_each')?['ApprovalStatus/value']),
  '</td></tr>'
) |
