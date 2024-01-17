# Gym Management System
The Gym Management System seeks automation for its 1000 members and 10 trainers. The system tracks subscriptions, facilitates bookings, and manages attendance for gym use, specialized sessions, and classes (a certain attendance limit).

## Setup environment

1. Populate database
    * Run Final_Scheme_with_data.sql in your Workbench
2. Create a virtual environment for installing Flask
3. Pip install all the dependencies (pip install -r requirements.txt)
4. Set up the local database configuration:
    * Create config.py in root directory.
    * Copy this content into it.
    * Change the values base on your mysql setup
```
SECRET_KEY="dev"
DB_USER = "root"
DB_PASS = "root"
DB_HOST = "localhost"
DB_PORT = "3306"
DB_NAME = "gym"
```
5. Run Python: Flask

## Pythonanywhere deployment adjustments:
1. add `dbconn.execute("SET time_zone = 'Pacific/Auckland';")` to db.py just after `dbconn = connection.cursor()` for setting timezone for the connection
2. Comment out the `BackgroundScheduler` in `autopay.py` that doesn't allow to import in pythonanywhere


--- 
## Auto deduction of member's subscription(membership) fee 
 
* autopay.py
* ONLY members whose membership account status is ACTIVE
* The next membership fee is automatically deducted from their bound bank card at 1 am on the same day their current membership ends based on the membership type
* Conducting automatically on the back end of the system at 1 am in daily routine

***IMPORTANT NOTES: The autopay functionality is implemented by the apscheduler package and can execute smoothly in the local environment, but due to the limitations of the Pythonanywhere platform, the apscheduler package cannot be run the same as in the local environment unfortunately.***
