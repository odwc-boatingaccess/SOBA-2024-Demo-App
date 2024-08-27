# Customize the Reporting Screen (EditScreen1)

1. From the `Screens` view in the `Tree view` menu, expand the `EditScreen1` object
2. Select the `LblAppName3` element
3. Under the `Properties` view in the right-hand toolbar, select the `Text` field
4. Edit the `Text` field value from `SOBA 2024 Inspection Reports` to `Inspection Report`

## Add Auto-Populated Dropdown Choices from the Projects Database

1. From the `Screens` view in the `Tree view` menu, expand the `EditScreen1` object
2. Expand the nested `EditForm1` object
3. Select and expand the nested `Region_DataCard2` object
4. In the top toolbar, open the `+ Inset` menu
5. Expand the `Input` submenu
6. Select `Drop down` option
  - If the Data Card is locked, click `Unlock and Add` in the warning message
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
  - `Waterbody_DataCard2`
    - Add the `Filter()` function to the `Items` field to display waterbodies from within the selected region
      ```visual-basic
      Items == Distinct(Filter('SOBA 2024 Projects', Region=Dropdown_region.Selected.Value), 'Waterbody')   
      ```
    - `Project Site_DataCard2`
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
  - If the Data Card is locked, click `Unlock and Add` in the warning message
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
  - If the Data Card is locked, click `Unlock and Add` in the warning message
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
  - Change the `Width` field for the `Vertical Container` to be
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
  - This object will not be accessible to the end users

---

[<kbd> <br> Previous <br> </kbd>][previousLink] [<kbd> <br> Next <br> </kbd>][nextLink]

[previousLink]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/edit-app-details.md
[nextLink]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/customize-reporting-screen.md
