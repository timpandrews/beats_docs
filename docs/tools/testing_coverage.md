# Testing & Coverage

![Testing](../assets/icons/django-testing.png){: width="25%"}
![Coverage](../assets/icons/coverage.png)

## Common Setup Mixins

In the project's test setup, a series of mixins have been developed under the module __project.tests.setup__. These mixins serve the purpose of standardizing the creation of various objects such as users, activities, levels, containers, and others, which are commonly used in test cases. By utilizing these mixins, the process of setting up test data becomes consistent and streamlined across different test cases.

These mixins are designed to be inherited by individual TestCase classes based on their specific testing requirements. Test classes can inherit a combination of these mixins depending on the data setup needed for each test scenario. This modular approach allows for greater flexibility and reusability of test setup code, promoting cleaner and more maintainable test suites.

### Usage

- Import required Mixins

```py
from project.tests.setup import BasicUserSetupMixin, LevelSetupMixin
```

- Define TestCase class and inherit required Mixins

```py
class SampleTestCase(TestCase, BasicUserSetupMixin, LevelSetupMixin)
```

- Initiate Mixins in either a setUpTestData or setUp Methods.

<small>__setUpTestData()__: This method is called once per test case class and is used to set up test data that will be shared across all test methods within the class. It's commonly used to create database records or initialize other resources that will be used by multiple test methods.</small>  

```py title="setUpTestData()"
@classmethod
def setUpTestData(cls):
    """Call LevelSetupMixin setUpTestData."""
    BasicUserSetupMixin.setUpTestData()    
    LevelSetupMixin.setUpTestData()
```

<small>__setUp()__: This method is called before each individual test method within the test case class. It's used to set up any test-specific data or resources that are needed for the particular test method being executed. This allows you to customize the test environment for each test method independently.</small>

TODO:Does this actually work?  Need to test using the setUp() method this way

```py title="setUp()"
def setUp(self):
    """Call LevelSetupMixin setUpTestData."""
    super().setUp()
    BasicSetupMixin.setUpTestData()??
    LevelSetupMixin.setUpTestData()??

    # add additonal setup as necessary
```

- Access objects in individual tests with self
```py
self.user
self.profile
...
```

### Mixin Names & Objects Provided

#### - BasicUserSetupMixin
  
- user
- profile

#### - SuperUserSetupMixin

- superuser
- superprofile

#### - LevelSetupMixin

- level(level=1 min_range=0 max_range=99)
- level(level=2 min_range=100 max_range=199)
- level(level=3 min_range=200 max_range=299)

#### - BeatsSetupMixin (inherits BasicUserSetupMixin)

- log1 (transaction_type="add", transaction_amount=100)
- log2 (transaction_type="subtract", transaction_amount=30)
- log3 (transaction_type="add", transaction_amount=50)
- user (from BasicUserSetupMixin)
- profile (from BasicUserSetupMixin)

#### - RoomContainerSetupMixin (inherits BasicUserSetupMixin)

- config_room (The room configuration object created for testing.)
- config_container (The container configuration object created for testing.)
- room
- container
- user (from BasicUserSetupMixin)
- profile (from BasicUserSetupMixin)

## Common Setup Class

A CommonSetup class has been created in projects/tests/setup.py. It allows
you to utilize the pre-defined setup, including users, profiles, and activities, directly in your tests.

To use the CommonSetup class in other tests, inherit test classes from CommonSetup instead of TestCase. 

If additional setup is needed that is not included in CommonSetup() you can call super().setUp() to add to the setUp method.

- Import CommonSetup
```py
from project.tests.setup import CommonSetup
```

- Inherit from CommonSetup
```py
class MyNewTest(CommonSetup):
    def test1(self):
        ...
```

- The Class creates the following objects
```
- userM, userI: Test users with metric and imperial preferences, respectively.
- profileM, profileI: Corresponding profiles detailing unit preferences and
  additional information.
- activityM1, activityM2, activityI1, activityI2: Activity records associated
  with the respective users.
- kudoM2, kudoI2a, kudoI2b: Kudo records linked to the activities (1 trophy
  for userM with activityM2, 2 trophies for userI with activityI2)
- date_range: A dictionary defining the start and end dates for a common 
  testing period.
- userM_distance, userM_elevation, userI_distance_km, userI_distance_mi,
  userI_elevation_m, userI_elevation_ft: Expected results for tests involving
  distance and elevation calculations in both unit systems.
```

```py title="CommonSetup()"
class CommonSetup(TestCase):
    def setUp(self):
        """Set up the test users, profiles, and activities."""
        # setup for metric user
        self.userM = User.objects.create_user(username="testuserM", password="12345")
        self.profileM = Profile.objects.create(
            user=self.userM,
            bio="Metric user",
            units_display_preference="metric",
        )
        self.activityM1 = Activity.objects.create(
            user=self.userM,
            activity_type="ride",
            activity_timestamp=pendulum.datetime(2024, 1, 1, 16, 10, tz="UTC"),
            core_data={
                "distance": 10,
                "duration": 600,
                "elevation": 10,
                "calories": 200,
            },
        )
        self.activityM2 = Activity.objects.create(
            user=self.userM,
            activity_type="ride",
            activity_timestamp=pendulum.datetime(2024, 1, 2, 16, 10, tz="UTC"),
            core_data={
                "distance": 100,
                "duration": 600,
                "elevation": 100,
                "calories": 200,
            },
        )
        self.kudoM2 = Kudo.objects.create(
            kudo_type="trophy",
            user=self.userM,
            kudo_name="Trophy 1",
            active=True
        )
        self.kudoM2.activities.add(self.activityM2)

        # setup for imperial user
        self.userI = User.objects.create_user(username="testuserI", password="12345")
        self.profileI = Profile.objects.create(
            user=self.userI,
            bio="Imperial user",
            units_display_preference="imperial",
        )
        self.activityI1 = Activity.objects.create(
            user=self.userI,
            activity_type="ride",
            activity_timestamp=pendulum.datetime(2024, 1, 1, 16, 10, tz="UTC"),
            core_data={
                "distance": 16.09,  # 10 miles
                "duration": 600,
                "elevation": 3.048,  # 10 feet
                "calories": 200,
            },
        )
        self.activityI2 = Activity.objects.create(
            user=self.userI,
            activity_type="ride",
            activity_timestamp=pendulum.datetime(2024, 1, 2, 16, 10, tz="UTC"),
            core_data={
                "distance": 160.934,  # 100 miles
                "duration": 600,
                "elevation": 30.48,  # 100 feet
                "calories": 200,
            },
        )
        self.kudoI2a = Kudo.objects.create(
            kudo_type="trophy",
            user=self.userI,
            kudo_name="Trophy 1",
            active=True
        )
        self.kudoI2a.activities.add(self.activityI2)
        self.kudoI2b = Kudo.objects.create(
            kudo_type="trophy",
            user=self.userI,
            kudo_name="Trophy 2",
            active=True
        )
        self.kudoI2b.activities.add(self.activityI2)

        # setup for date range this is common between the two users
        self.date_range = {
            "start": pendulum.datetime(2024, 1, 1, 0, 0, tz="UTC"),
            "end": pendulum.datetime(2024, 1, 7, 23, 59, 59, tz="UTC"),
        }
        # setup for expected results for the metric user
        self.userM_distance = 110
        self.userM_elevation = 110
        # setup for expected results for the imperial user
        self.userI_distance_km = 177.024
        self.userI_distance_mi = 110
        self.userI_elevation_m = 33.5488
        self.userI_elevation_ft = 110

    def tearDown(self):
        """Clean up the objects created during setUp."""
        self.userM.delete()
        self.userI.delete()
        # add more if I find that this is necessary
```