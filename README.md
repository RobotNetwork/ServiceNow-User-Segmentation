# Explanation - How does this work?

This repo contains two scripts, a UI Script (global) and a Script Include. The UI Script is executed when a form is loaded, but only runs if there are no properties stored, or if the properties haven't been updated in the last 7 days.

The UI Script will call the Script Include and gather data about the user (configurable), then passes it back to the UI Script to unpack the properties. The data is then stored in the browser under a custom property, `top.CustomPropStorage`.

## Setup

#### Script Include

1. Setup a PDI (Personal Developer Instance) via [developer.service-now.com](developer.service-now.com), or use a dev/test environment of your own
2. Navigate to **System Definition > Script Includes**, then create a new record
3. Set the name to `getDataForApty`
   > You can use an alternative name, but it will need to be reflected across both the UI Script and Script Include, else it won't work.
4. Check the box for `Client Callable`
5. Copy/paste the Script Include code into the code body
6. Mark the record as Active and save the record

#### UI Script

1. Navigate to **System UI > UI Scripts**
2. Create a new record
3. Name it how you wish
4. Set the UI Type to Desktop and ensure `Global` is checked
5. Copy/paste the UI Script code into the code body
6. Save, test

#### Applying Scripts to Service Portal

1. Navigate to **Service Portal > Dependencies**
2. Create a new record
3. Name it however you like
4. Set the application scope
5. Check the box for _"Include on Page Load"_
6. Save and return to the new record
7. Under _JS Includes_ click **Edit**
8. Set the Display Name however you please
9. Set the _Source_ to **UI Script**
10. In the _UI Script_ field, locate the name of the UI Script, then save the record
11. Navigate to **Service Portal > Widgets** and choose a widget that is loaded for all users
    > I chose the "Stock Footer", but the choice is dependent on your configuration.
12. Scroll down to the bottom, under the _Dependencies_ tab, click **Edit**
13. In the slushbucket, find the Dependency you created in **step 3** and move it over
14. Save the record

## Testing

1. Navigating to any record will initiate the UI Script
2. Open the dev console (browser) and type **top.CustomPropStorage**
3. Your output should contain data about your user profile in ServiceNow
   > **Note:** If testing is done in a PDI, many properties of _System Administrator_ (default admin account) are not set, like city, company, and location, among others. Impersonate another user with these properties set, or set them manually on the default account.
