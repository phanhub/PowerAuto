## Retrieving reports from the past 24 hours
Include statuses such as pending, rejected, or published, and exporting the data into a table with the following columns: Date Created | Title (with hyperlink) | Status.

### SharePoint | Get-Items
|  |  | Example |
|-------:|-------------------|---------------|
|Site Address | Select the path | https://XXXX.sharepoint.com/sites/XXX |
|List Name| Select the sub folder | Reports              |
|Filter Query| Created items at the behinning of the day on EST | (Created ge '@{startOfDay(addDays(convertTimeZone(utcNow(), 'UTC', 'Eastern Standard Time'), -1))}') and (ReportType eq 'PhanHub Mail') | 
|Limit Column by View | Select Sub category | All PhanHub Mail | 
