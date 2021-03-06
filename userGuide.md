# nidirect-prototypeForm: user guide

Once you have a copy of the **nidirect-prototypeForm** repository on your computer, you can start building your prototype in a HTML editor like [Visual Studio Code](https://code.visualstudio.com/).

## How does it work?
The prototype kit uses JavaScript and the browser’s Session Storage to save and retrieve values entered by the user.

![The prototype kit save the data entered in the form pages into the browser's session storage. The check page then retrieves and displays those values from the browser's session storage.](./assets/github_images/protoForm_pages.png)

The kit consists of three HTML template pages to build your prototype with:

### formPage.html
The 'form page' is used to display the [GOV.UK design system - components](https://design-system.service.GOV.UK/components/) that make up your prototype application.

Each 'form page' collects, validates, and saves the entered values into the browser’s Session Storage. 
### checkPage.html
The 'check page' uses the [GOV.UK Design System - check answers pattern](https://design-system.service.GOV.UK/patterns/check-answers/) to let the user check and change their answers saved in the Session Storage. 

You can have only one 'check page' per application in this version of the prototype kit.
### endPage.html
The 'end page' is used to let the user know they’ve completed the application successfully.
 

## Building your prototype

### Step 1: know what you’re building
Before you start building, sketch out your design for the prototype.

Sketches allow you to explore design ideas much faster and at lower risk than using the prototype kit right away.

### Step 2: make a copy of the HTML template files

1.	Open your copy of the **nidirect-prototypeForm** folder on your computer.

2.  Make a copy of the following HTML template files:
    *   checkPage.html
    *   endPage.html
    *   formPage.html

    To make a copy of a file in [Visual Studio Code](https://code.visualstudio.com/):
    1. Right click on the file you want to copy
    2. Select **Copy** from the pop up menu
    3. Right click below the files in the folder
    4. Select **Paste** from the pop up menu
    5. The copy of the file will appear in the folder with the word 'copy' after the original file name

        ![use the right click function to make a copy of a file in Visual Studio Code](./assets/github_images/github-guide-images-vscodeCopyFile-350px.gif)


### Step 3: build your form pages
'Form pages' are used to ask the user questions and collect their answers.

You can have as many 'form pages' as you need for your application. 


1.  Open your copy of the 'form page' HTML template.


2.	Go to [GOV.UK design system - components](https://design-system.service.GOV.UK/components/) and copy the HTML of the component you want to use in your prototype.

    ![use the copy code button to copy the HTML code of the component to your computer’s clipboard](./assets/github_images/protoForm-guide-copyCode.png)

3.	Paste the HTML of the component into your copy of the 'form page' below the `<h1>` heading.

4.	If the component is used to enter data, add a [GOV.UK design system - error message]( https://design-system.service.GOV.UK/components/error-message/) after the label and hint text of the component. 

    If the component is a fieldset of radios or checkboxes, add a [GOV.UK design system - error message]( https://design-system.service.GOV.UK/components/error-message/) after the legend and hint text of the component. 

    ```html
    <div class="govuk-form-group">
        <label class="govuk-label govuk-label--m" for="firstname">
            Firstname
        </label>
    
    |   <span id="firstname-error" class="govuk-error-message">
    |       <span class="govuk-visually-hidden">Error:</span> Enter your first name
    |   </span>
    
        <input class="govuk-input " id="firstname" name="firstname" type="text">
    </div>
    ```

    The error message should describe what to do when the user hasn't answered the question.

    The prototype kit will only show your error message if the question hasn’t been answered, when the **save and continue** button is pressed.


5.	Make sure each input and error component has a unique `id`.

    The `id` will be used to identify and save the entered value into the browser’s Session Storage.
    ```html
    <input class="govuk-input " id="firstname" name="firstname" type="text">
    ```
6.	To make an input component optional, add the text `--opt` to the end of the component’s `id`.

    If the component is marked as **optional** it will save any value entered. But it will not show its error message if the question hasn’t been answered.

    ```html
    <input class="govuk-input " id="firstname--opt" name="firstname" type="text">
    ```
    Remember to update the `for` attribute in the component's label to match the new `id` and add the text **(optional)** to the label.

    ```html
    <label class="govuk-label govuk-label--m" for="firstname--opt">
        Firstname (optional)
    </label>
    ```

7.	In the **save and continue** button component, at the bottom of the page, enter the next page of your prototype into the **saveData** JavaScript function.

    In the example below, the next page will be `'checkPage-1.html'`.
    ```html
    <button class="govuk-button" onclick="saveData('checkPage-1.html')">
        Save and continue
    </button>
    ```


### Step 4: build your check page
The 'check page' lets the user check and change their answers saved in the Session Storage. 

The 'check page' uses the [GOV.UK design system - summary list with actions component]( https://design-system.service.GOV.UK/components/summary-list/#summary-list-with-actions) to display the values saved in the Session Storage.

Use a separate summary list for each group of related answers *(e.g. title, first name, and surname)*. And use a `<h2>` heading tag to give each group a name. 

1.  Open your copy of the 'check page' HTML template.

    The 'check page' HTML template already has a summary list with its corresponding `<h2>` heading in place.
    
    To add another summary list go to [GOV.UK design system - summary list with actions component]( https://design-system.service.GOV.UK/components/summary-list/#summary-list-with-actions), copy the HTML of the component and paste it into your copy of the 'check page' below the current summary list.

2.	Each row of the summary list should display:
    * the question (the component’s label)
    * the user’s answer
    * a link to change their answer

3.	Between the `<dt>` tags with the `class="govuk-summary-list__key"` enter the question (the component’s label).
    ```html
    <dt class="govuk-summary-list__key">
        First name
    </dt>
    ```
4.	Between the `<dd>` tags with the `class="govuk-summary-list__value ` insert a `<span>` tag with the same `id` as the input component.

    This will display the value saved in the browser’s Session Storage.


    ```html
    <dd class="govuk-summary-list__value">
        <span id="firstname"></span>
    </dd>
    ```
    To display the saved values of a radio group or checkbox group, insert a `<span>` tag with its corresponding `id` for each available radio button or checkbox.
    
    Nothing will be displayed if there is no corresponding value saved in the Session Storage.

     ```html
    <dd class="govuk-summary-list__value">
        <span id="radio-confirmAge"></span>
        <span id="radio-confirmAge-2"></span>
    </dd>
    ```

    To insert a line break after the value, add the attribute `name="newline"` to the `<span>`.

    ```html
    <dd class="govuk-summary-list__value">
        <span id="address-street1" name="newline" ></span>
        <span id="address-street2" name="newline" ></span>
        <span id="address-city" name="newline" ></span>
        <span id="address-postcode"></span>
    </dd>
    ```

    To insert a forward slash character `/` after the day and month values of a date (for example 07/09/1988), add the attribute `name="addslash"` to the `<span>`s corresponding to the day and month.

     ```html
    <dd class="govuk-summary-list__value">
        <span id="dob-day" name="addslash"></span><span id="dob-month" name="addslash"></span><span id="dob-year"></span>
    </dd>
    ```


5.	Between the `<dd>` tags with the `class="govuk-summary-list__actions"` insert the link address to the input component’s 'form page'.
    
    Make sure to add the component’s label between the `<span>` tags with the ` class="govuk-visually-hidden"`.

    This will help users using assistive technologies to understand the purpose of the link.

    ```html
    <dd class="govuk-summary-list__actions">
        <a class="govuk-link" href="formPage-1.html">
            Change<span class="govuk-visually-hidden"> first name</span>
        </a>
    </dd>
    ```
6.	In the **accept and send** button component, at the bottom of the page, enter the 'end page' of your prototype into the **goTo** JavaScript function.

    In the example below, the 'end page' will be `'endPage-1.html'`:
    ```html
    <button class="govuk-button" data-module="govuk-button" onclick="goTo('endPage-1.html')">
        Accept and send
    </button>
    ``` 

### Step 5: build your end page
The 'end page' is used to let the user know they’ve completed the application successfully.

1.  Open your copy of the 'end page' HTML template.

2.  Add your 'application completed' message.

    As the nidirect 'end page' design is different from the [GOV.UK design system - end page](https://design-system.service.GOV.UK/patterns/confirmation-pages/), use the guidance on the [nidirect user experience model (UXM)](http://uxm.nidirect.GOV.UK/writing-guide.html#transaction-end-pages) to write your 'application completed' message.

3.  The 'end page' contains a **clear session** link in the footer at the bottom of the page.

    Enter the start page of your prototype into the `href` attribute of the **clear session** link.

    In the example below, the prototype will go to `'formPage-1.html'` after the user data is cleared from the Session Storage. 

    ```html
    <li>
        <!-- clear data entered and return to first form page -->
        <!--enter the first 'form page' of your prototype into the href attribute-->
        <a class="govuk-link" href="formPage-1.html" onclick="clearData()">
            Clear session
        </a>
    </li>
    ```

    In usability testing, use this link to clear the user data saved in the Session Storage and return to the first page of your prototype application for the next participant.

### Step 6: test your prototype for errors
1.	Open the first page of your prototype in the Google Chrome browser.

2.	Move through the prototype checking:

    * the correct error messages are shown for unanswered questions
    * the questions marked optional do not show an error message when left unanswered
    * the 'form page' moves to the next page when all the required questions have been answered
    * the back link at the top of each 'form page' works
    * the 'check page' displays the entered values correctly
    * the change links on the 'check page' go to the correct 'form page'
    * once the value has been updated and submitted on a 'form page' it returns to the 'check page' with the new value displayed

3. The main cause of errors is normally due to:
    * an input or error component with a duplicate `id`
    * an input or error component with no `id`

    Make sure each input and error component in your prototype has a unique `id`.
