# SOBA 2024 Power App Demo

Full tutorial for building the Power App covered in the Leveraging Technology to Monitor Boating Access Projects presented at the States Organization for Boating Access (SOBA) 2024 Education and Training Symposium held in Wilmington, North Carolina.

---

### 1. Set up the Databases

- [Create a Reports Database][reportsDatabase]
- [Setup a Database of Projects to Inspect][projectsDatabase]

### 2. Build the Power App

- [Convert Reports Database into a Power App][reportsDatabase2PowerApp]
- [Link the Projects Database][linkProjectDatabase]

### 3. Setup the Power App

- [Edit the App Details][editAppDetails]
- App Screens
  - By default, the app will auto-populate with 3 different screens:
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
- [Customize the Reporting Screen (EditScreen1)][customizeReprotingScreen]
- [Update the Report Details Screen (DetailScreen1)][updateDetailsScreen]
- [Customize the Home Screen (BrowseScreen1)][customizeHomeScreen]

### 4. [Test the App][testing]

### 5. [Publish the App][publish]

---

[reportsDatabase]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/create-reports-database.md
[projectsDatabase]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/upload-projects-database.md
[reportsDatabase2PowerApp]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/convert-reports-database-to-power-app.md
[linkProjectDatabase]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/link-projects-database.md
[editAppDetails]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/edit-app-details.md
[customizeReprotingScreen]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/customize-reporting-screen.md
[updateDetailsScreen]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/update-details-screen.md
[customizeHomeScreen]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/customize-home-screen.md
[testing]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/testing.md
[publish]: https://github.com/odwc-boatingaccess/SOBA-2024-Demo-App/blob/main/sections/publish.md
