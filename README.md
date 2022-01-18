## Explanation - How does this work?

The Script Include is a client-callable extension of _AbstractAjaxProcessor_ which allows you to call `getData` to retrieve data about the user, such as name, company, location, etc. The data retrieved by the system is then passed back into the client (UI) script as an XML Object, which is then iterated over to extract the users properties. After the iterations are complete, the data is then stored in the browser under a custom property, top.CustomPropStorage.

## Setup

#### Script Include
1. Setup a PDI (Personal Developer Instance) via [developer.service-now.com](developer.service-now.com) or use a dev/test environment of your own
2. Navigate to System Definition > Script Includes, create a new record
3. Name it `storeUserDataInBrowser`
> You can use an alternative name, but it will need to be reflected across both the UI Script and Script Include, else it won't work.
4. Check the box for `Client Callable`
5. Copy/paste the Script Include code into the code body.
6. Mark the record as Active and save it  

#### UI Script
1. Navigate to System UI > UI Scripts
2. Create a new record
3. Name it how you wish
4. Set the UI Type to Desktop and ensure `Global` is checked
5. Copy/paste the UI Script code into the code body
6. Save, test

## Testing

1. Navigating to any record will initiate the UI Script
2. Open the dev console (browser) and type **top.CustomPropStorage**
3. Your output should look similar to the below
> **Note:** If this is tested in a PDI, many properties of the _System Administrator_ (default) account are not set, like city, company and location, among others. Impersonate another user with these set, or set them manually.
 
 
