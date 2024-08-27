# Customize the Home Screen (BrowseScreen1)

1. From the `Screens` view in the `Tree view` menu, expand the `BrowseScreen1` object
2. Select the `LblAppName1` element
3. In the `Properties` view, select the `Text` field
4. Edit the `Text` field value from `SOBA 2024 Inspection Reports` to `Demo App`

### Add an App Icon to the Home Screen

1. Open the `Media` menu in the left-hand toolbar
2. Select the `+ Add media` option
3. Click `⬆️ Upload`to select an file
  - Short, descriptive file names such as `SOBA-2024-icon.png` are easier to work with
4. Open the `Tree View` menu in the left-hand toolbar
5. In the top toolbar, open the `+ Inset` menu
6. Expand the `Media` submenu
7. Select the `Image` option
  - If the Data Card is locked, click `Unlock and Add` in the warning message
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