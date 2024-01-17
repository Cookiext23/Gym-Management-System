## Setup environment

1. Populate database
    * Run Final_Scheme_with_data.sql in your Workbench
2. pip install all the dependencies (pip install -r requirements.txt)
3. Local DB config
    * Create config.py in the root directory.
    * Copy this content into it.
    * Change the values based on your MySQL setup
```
SECRET_KEY="dev"
DB_USER = "root"
DB_PASS = "root"
DB_HOST = "localhost"
DB_PORT = "3306"
DB_NAME = "gym"
```
4. Run Python: Flask

## Develop steps:
1. Create a branch for each user story - copy from the main branch
2. Create XXX.py using template.py
3. Create xxx.html inside templates or related folders using function(templete).html
4. Register the blueprint in app.py
5. update the README file
=== peer review ===
6. merge to main

## Pythonanywhere deployment adjustments:
1. add `dbconn.execute("SET time_zone = 'Pacific/Auckland';")` to db.py just after `dbconn = connection.cursor()` for setting timezone for the connection
2. Comment out the `BackgroundScheduler` in `autopay.py` that doesn't allow to import in pythonanywhere

## Checking roles
    ```
        {% if g.user.isMember %}
        <h1>I'm a member.</h1>
        {% elif g.user.isManager %}
        <h1>I'm a Manager.</h1>
        {% elif g.user.isTrainer %}
        <h1>I'm a Trainer.</h1>
        {% else %}
    ```
#### Functions

## GET /signup
* New member signup

## GET /member/bookclass 
* A drop-down box to select showing either specialized training sessions or group classes
* A button to confirm the selection

## POST /member/bookclass/classlist
* A table to show available group classes in the next 30 days for the member who is currently logging in
* A 'Back to previous page' button

## GET/POST   /member/bookclass/classlist/select_trainer
* A drop-down box to filter the table information by trainer's name with a 'Select' button right next to it.
* A table to show all available specialized training sessions in the next 30 days for the member logging in if the filter is not used.
* A table to show filtered available specialized training sessions in the next 30 days for the member logging in accordingly if the filter is used.
* A 'Back to previous page' button.

## POST /member/bookclass/classlist/select_trainer/bookst
* A message showing 'Specialized Training Session booked successfully!' 
`(no functionally conducted and leave it for us-8 coder)`

## POST /member/bookclass/classlist/bookgc
* A message showing 'Group Class booked successfully!' 
`(no functionally conducted and leave it for us-7 coder)`

## GET /staff/profile
* Show the current staff's profile 
* A button to update the profile

## POST /staff/profile/update
* A function to Update the staff's profile

## GET/POST /trainer/trainingmgmt/training
* List the specialized training
* A function to add specialized training

## GET /trainer/trainingmgmt/
* List schedule for specialized training which creates by current trainer account. 
* A button to update the schedule
* A button to delete the schedule
* A button to add the schedule

## GET /trainer/trainingmgmt/schedule
* same as GET /trainer/trainingmgmt/

## GET/POST /trainer/trainingmgmt/schedule/add
* Add specialized training schedule

## POST /trainer/trainingmgmt/schedule/edit
* A page to edit the specialized training schedule

## POST /trainer/trainingmgmt/schedule/update
* A function to update the specialized training schedule

## POST /trainer/trainingmgmt/schedule/del
* A function to delete the specialized training schedule

## GET /member/profile
* A table to show the current member's profile 
* A table to show the current member's payment history - (Added for User Story 19)
* An update button to update the profile
* A book class button book group class or specialized training

## POST /member/profile/update
* A form for the member to update their details (address/phone number/health condition ONLY)
* A save button to save any changes
* A cancel button to go back to the profile page

## GET /management/member/list
* List all members
* Provide a function to update member's detail
* Provide a function to deactivate members' detail
* Provide a function to add member
* Provide a function to delete member

## POST /management/member/search
* Search member by Name or ID
* List deactivated members - could only be deleted
* Delete members
--- 
# Sprint 2 from here

## GET /trainer/management/memberlist 
* show member list
* trainer_mgmt.py 
* The ‘Member Management’ button was added in the Navigator of base.html

## POST /trainer/management/memberlist/search
* fuzzy search by member’s first/last name or member ID
* trainer_mgmt.py 

## GET /manager/admin/news
* show gym news
* manager_admin.py
* ‘Gym News’ button added in the Navigator of base.html

## GET /manager/admin/class 
* select a class type
## GET/POST /manager/admin/class/specializedtraining 
* show specialized training list in the past 30 days and filter by trainer’s name accordingly
## POST /manager/admin/class/ 
* show group class list in the past 30 days
* manager_admin.py
* ‘Gym Classes’ button added in the Navigator of base.html

## GET /manager/admin/paymentinfo 
* show all payments’ info in two tables for membership fee and specialized training separately
## GET /manager/admin/paymentinfo/membershipfee
* show membership fee table only
## GET /manager/admin/paymentinfo/trainingfee
* show specialized training only
* manager_admin.py
* ‘Payments’ button added in the Navigator of base.html

## GET /member/bookclass/classlist/bookings
* Listing bookings for the member

## GET /member/bookclass/classlist/bookings/history
* Listing booking history for the member

## GET/POST /member/memberattend
* A function for member sign-in and displaying different usage options for using the gym at different times

## GET /trainer/trainingmgmt/traineelist
* Trainees list for both group class and specialized training schedules

## GET /trainer/trainingmgmt/schedule/trainees
* Parameter: scheduleid
* Show trainees who have booked the training schedule

## GET /trainer/trainingmgmt/schedule/search
* Parameters: scheduleid trainee
* Search trainees who have booked the training schedule by first name

## GET /trainer/trainingmgmt/schedule/trainees/detail
* Parameter: traineeID
* Show the trainee's detail

## GET/POST /management/groupclassmgmt/groupclass
* Show the group classes list
* Add group classes

## GET/POST /management/groupclassmgmt
* Show all group class schedule
* Update/delete schedule by manager

## GET/POST /management/groupclassmgmt/schedule
* Same as GET/POST /management/groupclassmgmt

## GET /manager/finance
* Revenue Report 
* Period could be selected
## GET /membership/expiry
* Show the list of members whose membership will expire within a month
* The manager can click on each member to update their details
## GET management/popularclasses/classes
* A List of popular classes
* Manager permission required
* Accepting a query parameter `class_type=group_class` or `class_type=specialized_training_session`



## GET /manager/news
* list/add/edit/update/delete news by manager
* list on the homepage
--- 
## Auto deduction of member's subscription(membership) fee 
 
* autopay.py
* ONLY members whose membership account status is ACTIVE
* The next membership fee is automatically deducted from their bound bank card at 1 am on the same day their current membership ends based on the membership type
* Conducting automatically on the back end of the system at 1 am in daily routine

***IMPORTANT NOTES: The autopay functionality is implemented by the apscheduler package and can execute smoothly in the local environment, but due to the limitations of the Pythonanywhere platform, the apscheduler package cannot be run the same as in the local environment unfortunately.***
