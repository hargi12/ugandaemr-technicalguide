# Report Development Guidelines

1. Fork the UgandaEMR Reports repository and clone the fork onto your computer 
2. Open the ugandaemr reports module in your IDE.
3. In the api module, go to org.openmrs.module.ugandaemrreports.reports package.
4. This is where all reports are made. To create a new report copy and paste one of the existing report files and rename your file appropriately.
5. In the new file created, we need to change various values
   1. ```text
      return value of the getExcelDesignUuid() method. This should be a unique string, different from other report ids.
      ```
   2. return value of the getUuid\(\) method method. This should also be a unique string.
   3. return value of the getName\(\) method. This will be the name of your report.
   4. return value of the getDescription\(\) method.
6. Copy a template of a report form that is in xls format and paste it in resources folder in org.openmrs.module.ugandaemrreports.reports package.
7. Copy the name of your xls file and paste it to buildReportDesign method as the third parameter in the createExcelTemplateDesign \(getExcelDesignUuid\(\), reportDefinition, "FILE\_NAME.xls"\).
8. Change the dataset name to be same as name of your report your working on also in the props.put\("repeatingSections","sheet:1,row:7,dataset: "REPORT\_NAME"\); this also is under the buildReportDesign method.
9. In the constructReportDefinition\(\) change also the first parameter of the rd.addDataSetDefinition \(\) method to match dataset name in the previous step.
10. Open the omod module of your project and open the ugandaemr\_reports\_app.json in the main &gt; resources &gt; apps folder.
11. To that end of that file, we need to add a new object with following attribute values as shown below

    ```text
    ,{
    "id":"Your_Report_Name",
    "extensionPointId":"org.openmrs.module.ugandaemr.mer",
    "type":"link",
    "label":"Your_Report_Name",
    "url":"reportingui/runReport.page?reportDefinition= id",
    "order":5
    }
    ```

    **NB:** In the code given above, we need to change our id on the url to be same as getUuid\(\) return id in our java file step described in Step 4.

12. Open your webapps &gt; pages in your omod module and open reports.gsp.
13. Add a new def to the other list of defs at the top of the file and give it a name appropriately referring to the group of reports it will fall under e.g name quarterly to represent quarterly reports, the name extension should also be changed to include the group name as shown in code below.

    ```text
    def quarterly =appFrameworkService.getExtensionsForCurrentUser("org.openmrs.module.ugandaemr.quarterly ")
    ```

14. To create a new report group, inside reports.gsp we add a new

    ```text
    <div class="info-container column"> </div>
    ```

    Add the following code in the div created

    ```text
    <% if (quarterly) { %>
     <div class="info-section">
        <div class="info-header"><h3>Quarterly Reports</h3></div>
           <div class="info-body">
               <ul>
                   <% quarterly.each { %>
                        <li>
                            ${ui.includeFragment("uicommons", "extension", [extension: it, contextModel: contextModel])}
                        </li>
                    <% } %>
                </ul>
             </div>
         </div>
     <% } %>
    ```

    **NB**: In the above code, replace "quarterly" with a your group name same as the one in the previous step.

15. Now refresh your reports page in the browser to see the changes made.

