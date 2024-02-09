# Testing & Coverage

### TODO: Complete Testing & Coverage Docs

![Testing](../assets/icons/django-testing.png){: width="25%"}
![Coverage](../assets/icons/coverage.png)

### CommonSetup

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