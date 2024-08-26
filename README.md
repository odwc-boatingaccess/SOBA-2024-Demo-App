# SOBA-2024-Demo-App
Full tutorial for building the Power App covered in the Leveraging Technology to Monitor Boating Access Projects presented at the States Organization for Boating Access (SOBA) 2024 Education and Training Symposium held in Wilmington, North Carolina.

# SOBA 2024 Power App Demo

Owner: Nathan Copeland
Last edited time: August 26, 2024 11:24 AM

---

# Setup Databases for Reports and Projects

## Create a Reports Database

1. Open your SharePoint site
2. Create a new List from the homepage
3. Select the `Blank list` option
    
    <aside>
    💡 You can also use the `From Excel` or `From CSV` options to set the column names and types before importing as a List
    
    </aside>
    
4. Name the new List as `SOBA 2024 Inspection Reports`
5. Add 9 columns to the new List using the column name and type listed below
    
    
    | Column Name | Column Type |
    | --- | --- |
    | Region | `Text` |
    | Waterbody | `Text` |
    | Project Site | `Text` |
    | Access Road | `Choice` |
    | Parking Area | `Choice` |
    | Boat Ramp | `Choice` |
    | Courtesy Dock | `Choice` |
    | Comments | `Multiple lines of text` |
    | Reporter | `Text` |
    - For the `Choice` column types, set the `Choices` field options to `Acceptable`, `Minor Issue`, & `Needs Repair`
    
    <aside>
    💡 The column type options for Lists also include `Image`, `Yes/No`, `Calculated`, `Date and time`, & `Lookup`. [Follow this link to learn about all the different column types.][LISTS_COLUMN_TYPES]
    
    </aside>
    

## Setup a Database of Projects to Inspect

1. Upload a `CSV` or Excel spreadsheet of boating access projects to the `Documents` directory on your SharePoint site
    - Demo `CSV`:
        
        [SOBA-2024-projects.csv][PROJECTS_CSV]
        
2. Create a new List
3. Select the `From CSV` option
4. Under the `SOBA 2024 Demo > Documents` heading, select the `SOBA-2024-projects.csv` file and then click `Next`
5. After reviewing the column names and types, click `Next`
6. Rename the List to `SOBA 2024 Projects` and select `Create`

---

# Build the Power App

## Convert Reports Database into a Power App

1. Open the `SOBA 2024 Inspection Reports` List
2. Use the `Integrate` menu to create a new app based on the List
    - `Integrate` → `Power Apps` → `Create an app`
    - If the `Integrate` menu is not visible, select the `...` icon to access it

## Link the Projects Database

1. Open the `Data` menu in the left-hand toolbar
2. Select `+ Add data`
3. Under the `Connectors` section, select `SharePoint`
4. Select the SharePoint site where you uploaded the demo projects database (`SOBA-2024-projects.csv`)
5. Select the `SOBA 2024 Projects` and click `Connect`

---

# Setup the Power App

## Edit the App Details

1. Use the `Tree View` menu in the left-hand toolbar, to open the `Screens` view
2. Rename the app and set the icon
    1. Open the `Settings` menu in the top toolbar
        - If not visible, select the `...` icon to access the `Settings` menu
    2. Edit the name field to `SOBA Demo`
    3. Use the `+ Add image` option to change the app's icon

## Default App Screens

By default, the app will auto-populate with 3 different screens:

- `BrowseScreen1`
    - Displays data from the Reports Database
    - Includes preloaded buttons and a search bar
        - `Refresh 🔄`: initiates a sync with the connected database
        - `Sort 🔃`: sorts the list of database rows by alphabetical order
        - `Add ➕`: add a new entry to the database
- `DetailScreen1`
    - View/Edit/Delete an entry from the database
- `EditScreen1`
    - Create a new entry using the connected database's schema

## Customize the Reporting Screen (EditScreen1)

1. From the `Screens` view in the `Tree view` menu, expand the `EditScreen1` object
2. Select the `LblAppName3` element
3. Under the `Properties` view in the right-hand toolbar, select the `Text` field
4. Edit the `Text` field value from `SOBA 2024 Inspection Reports` to `Inspection Report`

### Add Auto-Populated Dropdown Choices from the Projects Database

1. From the `Screens` view in the `Tree view` menu, expand the `EditScreen1` object
2. Expand the nested `EditForm1` object
3. Select and expand the nested `Region_DataCard2` object
4. In the top toolbar, open the `+ Inset` menu
5. Expand the `Input` submenu
6. Select `Drop down` option
    1. If the Data Card is locked, click `Unlock and Add` in the warning message
7. In the `Properties` view, open the `Advanced` menu
8. Update the `AllowEmptySelection`, `Default`, `Items`, `X`, & `Y` fields so the drop-down element will show a blank value until an option has been selected and is aligned with the `DataCardValue10` element
    
    ```visual-basic
    AllowEmptySelection == true
    Default == ""
    Items == Distinct('SOBA 2024 Projects', 'Region')
    X == DataCardValue10.X
    Y == DataCardValue10.Y
    ```
    
    - Using the `Distinct()` function will prevent the drop-down element from including duplicate options
9. Add a descriptive name to `Dropdown` element by double-clicking the element
    - Renaming the `Dropdown` elements with descriptive names will make it easier to reference the element in other views
10. Select the `DataCardValue10` element under the `Region_DataCard2` object in the `Tree view` menu
11. In the `Properties` view, open the `Advanced` menu
12. Update the `Default` & `Visible` fields so the drop-down element selection will be included in the report
    
    ```visual-basic
    Default == Dropdown_region.Selected.Value
    Visible == false
    ```
    
13. Repeat Steps 3-12 for the following Data Cards referencing the correct `DataCardValue` element:
    1. `Waterbody_DataCard2`
        - Add the `Filter()` function to the `Items` field to display waterbodies from within the selected region
        
        ```visual-basic
        Items == Distinct(Filter('SOBA 2024 Projects', Region=Dropdown_region.Selected.Value), 'Waterbody')   
        ```
        
    2. `Project Site_DataCard2`
        
        ```visual-basic
        Items == Distinct(Filter('SOBA 2024 Projects', Waterbody=Dropdown_waterbody.Selected.Value), 'Project Site')
        ```
        

### Update Dropdown Placeholder Text

1. From the `Screens` view in the `Tree view` menu, expand the `EditScreen1` object
2. Expand the nested `EditForm1` object
3. Expand the nested `Access Road_DataCard2` object
4. Select the `DataCardValue13` element
5. In the `Properties` view, open the `Advanced` menu
6. Update the `InputTextPlaceholder` field
    
    ```visual-basic
    InputTextPlaceholder == "Current Status"
    ```
    
7. Repeat Steps 4-6 for the `Parking Area_DataCard2`, `Boat Ramp_DataCard2`, & `Courtesy Dock_DataCard2` objects referencing the correct `DataCardValue` elements

### Create a Comments Data Card

1. From the `Screens` view in the `Tree view` menu, expand the `EditScreen1` object
2. Select the nested `EditForm1` object
3. Under the `Properties` view, click the `Edit Fields` option
4. Click the `Add field` option
5. Select the checkbox next to the `🔤 Comments` option and click `Add` 
6. Edit the `Control type` fields
    
    ```visual-basic
    Control type == 'Edit multi-line text'
    ```
    
7. Expand the new `Comments_DataCard2` object
8. In the `Properties` view, open the `Advanced` menu
9. Update the `HintText`, `Clear`, & `EnableSpellCheck` fields 
    
    ```visual-basic
    HintText == "Describe any issues here"
    Clear == true
    EnableSpellCheck == true
    ```
    

### Create a Reporter Data Card

1. From the `Screens` view in the `Tree view` menu, expand the `EditScreen1` object
2. Select the nested `EditForm1` object
3. Under the `Properties` view, click the `Edit Fields` option
4. Click the `Add field` option
5. Select the checkbox next to the `⏸️ Reporter` option and click `Add` 
6. Edit the `Control type` fields
    
    ```visual-basic
    Control type == 'Edit text'
    ```
    
7. Select and expand the new `Reporter_DataCard2` object
8. In the top toolbar, open the `+ Inset` menu
9. Expand the `Layout` submenu
10. Select the `Horizontal container` option
    1. If the Data Card is locked, click `Unlock and Add` in the warning message
11. In the `Properties` view, open the `Advanced` menu
12. Update the `DropShadow`, `Width`, `X` & `Y` fields to align the Container within the Data Card
    
    ```visual-basic
    DropShadow == DropShadow.None
    Width == DataCardValue24.Width
    X == DataCardValue24.X
    Y == DataCardValue24.Y
    ```
    
13. In the top toolbar, open the `+ Inset` menu
14. Expand the `Media` submenu
15. Select the `Image` option
    1. If the Data Card is locked, click `Unlock and Add` in the warning message
16. Add a descriptive name to the `Image` element by double-clicking the element
17. In the `Properties` view, open the `Advanced` menu
18. Update the `Image`, `Height`, `Radius`, `Width`, `X` & `Y` fields to create a round thumbnail of the user's profile photo
    
    ```visual-basic
    Image == User().Image
    Height == DataCardValue24.Height*1.75
    RadiusBottomLeft == DataCardValue24.Height
    RadiusBottomRight == DataCardValue24.Height
    RadiusTopLeft == DataCardValue24.Height
    RadiusTopRight == DataCardValue24.Height
    Width == DataCardValue24.Height*1.75
    X == Parent.X
    Y == Parent.Y
    ```
    
19. Repeat Steps 8-9 and add a `Vertical container` nested within the `Container1` object
    1. Change the `Width` field for the `Vertical Container` to be
        
        ```visual-basic
        Width == Parent.Width-Image1_user.Width
        ```
        
20. In the top toolbar, open the `+ Inset` menu
21. Expand the `Display` submenu
22. Select `Text label` option
23. Add a descriptive name to the `Label` element by double-clicking the element
24. In the `Properties` view, open the `Advanced` menu
25. Update the `Text`, `PaddingLeft`, `Width`, `X` & `Y` fields to display the user's name and align it with the user’s thumbnail photo
    
    ```visual-basic
    Text == User().FullName
    PaddingLeft == 10
    Width == Parent.Width
    X == Parent.X
    Y == Parent.Y
    ```
    
26. Select the `DataCardValue24` element under the `Reporter_DataCard4` object in the `Tree view` menu
27. In the `Properties` view, open the `Advanced` menu
28. Update the `Default` & `Visible` fields so the drop-down element selection will be included in the report
    
    ```visual-basic
    Default == User().FullName
    Visible == false
    ```
    

### Setup the Report ID

1. From the `Screens` view in the `Tree view` menu, expand the `EditScreen1` object
2. Expand the nested `EditForm1` object
3. Expand the nested `Title_DataCard2` object
4. Select the `DataCardValue13` element
5. In the `Properties` view, open the `Advanced` menu
6. Update the `Default` field to auto-populate with the waterbody, project site, and the current date/time
    
    ```visual-basic
    Default == Dropdown_waterbody.Selected.Value&" - "&Dropdown_projectSite.Selected.Value&" "&Text(Now(),DateTimeFormat.ShortDateTime24)
    Visible == false
    ```
    
7. Select the `Title_DataCard2` object in the `Tree view` menu
8. In the `Properties` view, toggle off the `Visible` field for the `Title_DataCard2` object
    1. This object will not be accessible to the end users

## Update the Report Details Screen (DetailScreen1)

1. From the `Screens` view in the `Tree view` menu, expand the `DetailScreen1` object
2. Expand the nested `DetailForm1` object
3. In the `Properties` view, click the `8 Selected` value for the `Fields` field
4. Click the `Add field` option
5. Select the checkbox next to the `🔤 Comments` & `⏸️ Reporter` options and click `Add` 
6. Close the `Fields` field menu
7. Select the `LblAppName2` element
8. In the `Properties` view, select the `Text` field
9. Edit the `Text` field value from `SOBA 2024 Inspection Reports` to `Completed Report`

## Customize the Home Screen (BrowseScreen1)

1. From the `Screens` view in the `Tree view` menu, expand the `BrowseScreen1` object
2. Select the `LblAppName1` element
3. In the `Properties` view, select the `Text` field
4. Edit the `Text` field value from `SOBA 2024 Inspection Reports` to `Demo App`

### Add an App Icon to the Home Screen

1. Open the `Media` menu in the left-hand toolbar
2. Select the `+ Add media` option
3. Click `⬆️ Upload`to select an file
    1. Short, descriptive file names such as `SOBA-2024-icon.png` are easier to work with
4. Open the `Tree View` menu in the left-hand toolbar
5. In the top toolbar, open the `+ Inset` menu
6. Expand the `Media` submenu
7. Select the `Image` option
    1. If the Data Card is locked, click `Unlock and Add` in the warning message
8. Add a descriptive name to the `Image` element by double-clicking the element
9. In the `Properties` view, open the `Advanced` menu
10. Update the `Image`, `Height`, `Radius`, `Width`, `X` & `Y` fields to create a round thumbnail of the user's profile photo
    
    ```visual-basic
    Image == 'SOBA-2024-icon'
    Height == LblAppName1.Height
    Width == LblAppName1.Height
    X == LblAppName1.X
    Y == LblAppName1.Y
    ```
    
11. Select the `LblAppName1` element
12. In the `Properties` view, open the `Advanced` menu
13. Update the `PaddlingLeft` field to prevent the app icon from covering the app name
    
    ```visual-basic
    PaddlingLeft == Image3_appIcon.Width+15
    ```
    

---

# Test the App

1. From the `Screens` view in the `Tree view` menu, select the `BrowseScreen1` object
2. Select the `Preview` icon `▶️` in the top toolbar
3. Use the tab toolbar to switch the device type used by the testing sandbox
    1. By default the testing sandbox runs the app in `Browser` mode 
4. Select the `+` icon on the home screen in the app to create a new report
5. Complete the report fields
6. Select the `☑️` icon to save the report and return to the home screen
7. Select the `>` icon next to the report entry on the home screen to view it
8. Select the `✏️` icon to edit the report or the `🗑️` icon to delete the report
    1. These options can be disabled by editing the associated elements within the [DetailScreen](https://www.notion.so/SOBA-2024-Power-App-Demo-c2783b7bc3d94fbdacda618181c41569?pvs=21)

---

# Publish the App

1. Select the `Publish` icon the top toolbar (next to the `Save 💾` icon)
2. Select `Publish this version`
    1. If you need to edit the general settings for the app, select `Edit details`
3. Select the `← Back` option in the top toolbar
4. Select `Leave`
5. From the Power Apps homepage
6. Open the Details menu
7. Share the URL or QR Code
8. From your SharePoint site, add a button to the app
9. Add members to control access to the app
---

[LIST_COLUMN_TYPES]: https://support.microsoft.com/en-us/office/list-and-library-column-types-and-options-0d8ddb7b-7dc7-414d-a283-ee9dca891df7
[PROJECT_CSV]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/SOBA-2024-projects.csv
