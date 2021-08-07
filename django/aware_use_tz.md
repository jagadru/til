# Be careful with setting USE_TZ

Dev environment:
 - Running unit tests in dev environment
 - Creating and storing datetimes in Django ORM with USE_TZ = False with timezone UTC
 - Datetime were unaware of timezones and all tests passed `datetime.datetime(2020, 2, 2, 14, 50, 59)`

 QA/Jenkins:
 - Running unit test suite in Jenkins
 - Creating and storing datetimes in Django ORM with USE_TZ = True with timezone Los Angeles
 - Datetime had shifted values in UTC `datetime.datetime(2020, 2, 2, 22, 50, 59, tzinfo=<UTC>)`
