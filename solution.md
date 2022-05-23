# Pages

I used 2 routes which are the following :

# home ( / )

    which serve as the landing page and the page 1 of the application

# wizard (/wizard)

3 components: ( Forms, PageError and Final Summary)

#Forms template has two parts : The form fields and the short summary 1. Form fields - shows the input fields 2. Short summary - shows the premium price ( which changes automatically based on user input) and the action buttons

Steps in Form fields

```
Fill up name and age, then select a country.
```

```
Package choices will not be shown unless age and country is filled up.
```

```
Package Choices contains the 3 cards which the user can select by clicking.. Prices were displayed also based on user input
```

# Final Summary

    Contains the user information and the package that is being selected. Actions buttons also were included, in this case it is "back" and "buy". Buy will redirect you to home page.

# Page error:

    Once the next button in the short summary template of the wizard page is clicked and the age is over 100, you will be directed to this page

# Styling

    Some html elements uses tailwind css/classes
    Some html element uses standard css/scss

# Technologies Used

    Frontend : Vue3 ( Vue Cli)
    Styling : Tailwind and standard css/scss
    Prettier/EsLint
    No state management(vuex) is implemented since this is just a simple application

# Developer Approach

    Landing Page contains a button that will redirect you to the wizards form page

    A form is directly bind to model which is an object contain the properties ( name , age , country)

    A Check will be initiated once there is a change in user input, specially on the age and country ( for computation )

    If age and country is defined, the package choice flag will be activated and will be displayed.

    Package choices contains the 3 cards ( standard, safe, super safe), User selects one , and will display the premium price ( short summary component)

    The user will be having two action buttons ( Back and Next )

    Back will redirect the user to the previous page, while Next button will be having a check if the age is over 100, if yes the user will be directed to the page error page, other wise will proceed to the last step which contains the summary of the user transactions and buttons of Back and Buy provided that all 3 input fields are filled up, otherwise the button is disabled. Back button will redirect you to the previous page with information user provided. Then Buy button will redirect to the landing page.

# One route solution

    git checkout wizard_covergo_one_route
