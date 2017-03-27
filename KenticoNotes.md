1. While restoring the Backup
  - *add new website* 
  - point to the *CMS* folder
  - configure ConnectionString
  
  
2. To access, the unmapped fields from inside search transformation, use: GetSearchValue("FieldName") [if the property exists on the matched pagetype, the value of that field is returned]

3. To enable search through query string parameters, in the smartSearchResults, webpart repeater, set: 
    - Paging Mode = "QueryString"
    - Search Condition = {%IfEmpty(QueryString["datefilter"],"","+" + QueryString["DateFilter"])#%} [appends this condition to any search query]
    
4.   
