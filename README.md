<h1 align="center">Welcome to googlemaps-cypress auto tests 🌄</h1>

### 🏠 [Homepage]()

## Description

This module exposes a function that tests google map application. It uses [cypress](https://github.com/cypress-io) to achieve variants of acceptance criteria.
Additionally, it has options to provide test in different language depends ond location.

## Installaion

_Below step by step how you can install and run project._

1. Clone repo
   ```sh
   git clone https://github.com/Bibek02/google_map
   ```
2. Install NPM packages
   ```sh
   npm install
   ```
3. Open Cypress
   ```sh
   npx cypress open
   ```

## Run
_Below lists of run scripts with different tests data for each geolocation. 
If your geolocation from which you want to run the tests is missing, add it to the config files_

|Location        | Run script                                |
|----------------|-------------------------------------------|
|Great Britan    |npm run cypress:en                         | 
|Holland         |npm run cypress:nl                         | 
|France          |npm run cypress:fr                         |
|Japan           |npm run cypress:jp                         |
|Poland          |npm run cypress:pl                         |
|United States   |npm run cypress:us                         |

## Tests
_List of tests done/undone_

Status  |Scenario       | Test_set    | Spec_file    | Test_name
:------ | :------------ | :---------- | :----------- | :---------------------------------------------------
&#x2611;| search_bar    | insert      | left_panel   |Insert city and check headline
&#x2611;| search_bar    | insert      | left_panel   |Insert city and check autofil in the direction field'
&#x2611;| search_bar    | insert      | left_panel   |Insert random numbers and check content in left panel
&#x2612;| search_bar    | remove      | top_bar      |Remove city
&#x2612;| search_bar    | edit        | left_panel   |Edit inserted city

## Adding test
_Instruction for adding new test in Page Object Pattern_

Page Object Pattern Guide
1. Understand: Gain a clear understanding of the structure of the page you're testing.

```
    .
    ├── ...
    ├── pages
    │   ├── map
    │   │   ├── destination.ts
    │   │   ├── map.ts
    │   ├── privacy
    │   │   ├── privacy.ts
    └── ...
```
2. Page Object Classes: Create dedicated Page Object classes for each page or component.
```typescript
export class MapPage{
    ...
}
export onMapPage = new MapPage()
```
3. Abstract Operations: Define methods within Page Object classes to perform actions on the page.
```typescript
    searchBar = {
        click: {
            searchButton(): void {...}
            },
        fill: {
            searchInputText(test: string): void{...} }
        }
```
4. Separate Logic: In your tests, utilize methods from Page Object classes to interact with the interface.

5. Avoid Repetition: Prevent redundant code by utilizing the capabilities of Page Object classes.

6. Locators: Store element locators within the relevant Page Object classes.
```typescript
export class MapPage {
    private static BAR_INPUT_ID = "searchboxinput"
    private static SEARCH_BUTTON_ID = "searchbox-searchbutton"
    private static CLOSE_BUTTON_TAG = "button.vF7Cdb"
```

7. Limit Access: Expose only necessary methods to interact with elements, rather than exposing the elements directly.
```typescript
    private static BAR_INPUT_ID = "searchboxinput"

//map.ts
```
8. Assertions: Use assertions within Page Object methods to verify the expected state.
```typescript
    leftPanel = {
        assert: {
            header(text: string): void {...})
            }
...

//map.ts
```
9. Tests with Page Objects: Construct your tests using the actions provided by the Page Object methods.
```typescript
  it('Insert city and check autofil in the direction field', { tags: '@happyPath' }, () => {
    //given
    const city = Cypress.env('secondCity')
    //when
    onMapPage.searchBar.fill.searchInputText(city)
 ...
```
10. Configuration: Manage configuration and initialization of your Page Objects.
```typescript
        setupNodeEvents(on, config) {
            // if version is not loaded use local
            const version = config.env.version || 'local'
            // load env from json
            config.env = require(`./cypress/config/${version}.json`)
            config.baseUrl = config.env.baseUrl
            return config;
        }

//Look to cypress.config.ts and cypress/config/
```
11. Maintenance: Keep your Page Objects up to date to accommodate changes in the interface.

## Report
_Report are generated after tests complite in mochawesome-report/mocawesome.html folder_
```
    ├── ...
    ├── mochawesome-report
    │   ├── mochawesome.html
    ├── ...

```
To open the generated report, install the [Live Server]() plugin in your IDE and then use it to launch the report file. The [Live Server]() will provide a live preview of the report in your browser.

### TypeScript support

The code is written in Typescript.
