1. Preparation Project
    - [X] Installation Laravel
        ```bash
        composer create-project laravel/laravel="8.6.2" Laracamp
        ```
    - [X] Create New Database

2. Migration
    - [X] Migration User Table Pt.1
    - [X] Migration User Table Pt.2
    - [X] Migration Camp Table
    - [X] Migration Camp Benefit Table
    - [X] Migration Camp Benefit Relation
    - [X] Migration Checkout Table

    ```bash
    #Command
    php artisan make:migration create_table_camps --table=camps

    php artisan make:model Camps

    php artisan make:model CampBenefit -m

    Update the Instance Group to the Version 2 Website
Back in the GCP console, click on the hamburger menu icon in the top left corner.
Select Compute Engine. You should see that there are three new instances that are part of the web group and are using instance-template-1.
In the lefthand navigation menu, select Instance templates.
Click the Create Instance Template button.
Under Machine type, select e2-micro.
Under Boot disk, select Change.
In the Boot disk pane, select the Custom images tab.
In the Image dropdown, select web-v2.
Click the Select button.
Back in the instance template page, under Firewall, select Allow HTTP traffic.
Click the Create button. This will create the new image template.
In the lefthand navigation menu, select Instance groups.
Select web-group in the list.
Select Update VMS at the top.
Under New template, select instance-template-2 from the dropdown menu.
Under Update configuration, click the dropdown to enable the Update type menu.
Select Automatic.
Leave all the other settings at their defaults. Make sure that the Temporary additional instances and Maximum unavailable instances options are both set to 1 instance.
Note: If you were to use a multi-zone group vs. a single-zone group, you would be more restricted in regards to the surge/max unavailable settings.

Click Update VMS. The updating process can take a few minutes to complete. You should eventually see that there are four instances.
Return to the browser window or tab where you opened the custom website.
After several minutes, verify that the website eventually displays VERSION 2, confirming that the instance group has been updated successfully. If you refresh, it will eventually swap back to VERSION 1 and then back to VERSION 2. Once it settles on VERSION 2, it should stay that way permanently.