# Develop with Apps Script and AppSheet: Challenge Lab

## Solution here

### Task 1. Create and customize an app

1. After you've logged into `AppSheet`, open the `ATM Maintenance` app in a new browser tab.

2. In the left navigation menu, click `Copy app` (copy).

3. In the Copy app form, for App name, type `ATM Maintenance Tracker`, and leave the remaining settings as their defaults.

4. Click `Copy` app.

5. Click `Customize your app` to go to the `AppSheet editor`.

6.To open the Chat app builder, select Chat apps (chat icon) in the left navigation menu.

7. Click Create.

8. In the Enable card, click Next to automatically configure your project.

9. In the Customize card, click First message to expand the section.

10. For message text, change the greeting to: Welcome to the ATM Maintenance Tracker app. What do you want to do today?

11. In the list of app cards, click My Tickets, and then select Issues Reported By Me in the dropdown to change the chat card.

12. To remove the Manage Techs view, click Delete.

13. In the Actions section, click + New action.

14. Select Slash command: Open app view from the list of options.

15. Select Issues Reported By Me from the App View dropdown.

16. Type /myissues for the Name.

17. In the Description field, type Lists tickets that include your email address.

18. Click Next.

### Task 2. Add and test an automation

1. In the Test card, click Go to deployment settings to open the Deploy tab in the AppSheet UI.

2. If the deployment check does not begin automatically, click Run Deployment Check.

3. The output of the deployment check lists any errors or warnings that you should fix, before deploying the app.

4. Click App description.

5. The section expands to provide more details on the warning.

6. Click Continue editing so you can address the App description warning before publishing your app.

7. In the left navigation menu, click Settings (settings).

8. In the Information tab, in the App Properties section, click the dropdown for Function.

9. Select Maintenance from the list of options.

10. Click the dropdown for Industry and select Financial Services.

11. Click Save.

12. In the left navigation menu, click Manage (manage) to return to the Deploy options.

13. In the Deployment Check section, click Run deployment check to rerun the process.

14. Click Move app to deployed state.

15. In a new incognito tab, open Google Chat.

16. If a modal appears, click Get Started, and then click X to close the tutorial.

17. In the lower left pane, in Spaces, click + to Create or find a space, and then click Create space.

18. Type a space name, and then click Create.

19. Click Add people & apps, select the ATM Maintenance Tracker app from the list, and then click Add.

20. Return to your AppSheet tab and select Chat apps (chat icon) in the left navigation menu to open the Chat app builder.

21. Click the Customize card in the Chat app editor.

22. Click + New action, and then select Build my own...

23. The automation page in the AppSheet editor will open in the same tab.

24. Click Configure event, and then click Create a custom event.

25. In the Settings panel, provide the following information:

Event name	New ticket

Event type	add Adds only

Table		Tickets

26. In the main panel, click + Add a step, and then select Create a custom step.

27. Click New step to open the Settings for the custom step you just created.

28. In the Settings panel, click chat icon Send a chat message.

29. For Message Content, choose the Select chat spaces option.

30. For Space ID(s), click Add, and then select the space you created in the previous task.

31. In the Message Text box, type the message: You have created a new ticket.

32. At the top right of the page, click Save to update your app.

33. Navigate back to Google Chat and open the space in Google Chat that you created in the previous task.

34. Click New Ticket in the ATM Maintenance Tracker App.

35. In the First Name box, type Freeda.

36. Provide the information of your choosing for ATM ID and Symptom.

37. Click Save.


### Task 3. Create handlers for Google Chat events and publish the bot

1. Click this Google Apps Script editor link to open the Google Apps Script online editor.

2. Click Untitled project (the current name).

3. In the Edit project name dialog, rename the project to Attendance Bot, and then click Rename.

4. Update the manifest file

5. In the left panel, click Project Settings (settings gear icon).

6. Check Show "appsscript.json" manifest file in editor in the General settings section.

7. Go to the Google Cloud console, click the Navigation menu (Navigation menu icon) in the upper left and navigate to APIs & Services > OAuth consent screen.

8. Set User Type to Internal and click Create.

9. On the next page, (the OAuth consent screen), configure the following:

10. On the next page (Scopes), leave all the fields empty, and then click Save and Continue.

11. As shown in the next page (Summary), the OAuth Consent Screen is now created for your app.

12. Click Back to Dashboard at the bottom of the page.
 
13. Click the Console icon.

14. Record the Project number to use in the next step to configure your project.

15. In the App Script editor, navigate to the Project Settings (project icon).

16. Under Google Cloud Platform (GCP) Project, click Change project.

17. When prompted, enter the Project number value, copied earlier, in the GCP Project number field. Then click Set project.

18. Go to the Apps Script editor and get the Deployment ID. You do this by clicking on Deploy > New Deployment in the top-right of the screen.

19. In the Description field, enter App Script lab bot, and click Deploy.

20. Note down the Deployment ID to use later and click Done.

21. Go to the Google Cloud console, navigate to Navigation Menu (Navigation menu icon) > APIs & Services > Library.

22. In the Library, search for Google Chat API. Select the API from the list of results.

23. By default, the Google Chat API is already enabled. If it is not enabled, click Enable.

24. Click Manage and then click the Configuration tab under the Google Chat API section.

25. In the Configuration dialog, set the fields with the following values:

26. After the changes are saved, scroll to the top of the Configuration dialog to update the App Status to LIVE – available to users. You may have to reload the browser page to see the App Status field.

27. Click SAVE again.