# Sitemaps

## Overview

Sitemaps are XML files that list the URLs for a site, along with additional metadata about each URL (such as when it was last updated, how often it changes, and how important it is relative to other URLs on the site). This helps search engines like Google to crawl the site more intelligently.

In this project, we use Django's built-in sitemap framework to generate sitemaps for both static and dynamic content.

### StaticViewSitemap

The StaticViewSitemap class is used to include static pages (like home, about, and contact) in the sitemap.

#### Implementation

The StaticViewSitemap class is defined in project/apps/common/sitemaps.py:

``` py title="sitemaps.py"
from django.contrib.sitemaps import Sitemap
from django.urls import reverse

class StaticViewSitemap(Sitemap):
    """Static views sitemap"""

    priority = 0.5
    changefreq = "monthly"

    def items(self):
        """Items to include in the sitemap"""
        return ["pages:home", "pages:about", "pages:contact"]

    def location(self, item):
        """Location of the item in the sitemap"""
        return reverse(item)
```

#### URL Configuration

The sitemap is included in the URL configuration in project/core/urls.py:

``` py title="urls.py"
from django.contrib.sitemaps.views import sitemap
from project.apps.common.sitemaps import StaticViewSitemap

sitemaps = {
    "static": StaticViewSitemap,
}

urlpatterns = [
    path("sitemap.xml", sitemap, {"sitemaps": sitemaps}, name="sitemap"),
    # ... other url patterns ...
]
```

### Creating Additional Sitemap Classes

To create additional sitemap classes for dynamic content, follow these steps:

1. Define the Sitemap Class: Create a new class in project/apps/common/sitemaps.py or in the relevant app's sitemaps.py file.

    ``` py title="sitemaps.py"
    from django.contrib.sitemaps import Sitemap
    from project.apps.blog.models import Post

    class PostSitemap(Sitemap):
        changefreq = "weekly"
        priority = 0.6

        def items(self):
            return Post.objects.filter(status="published")

        def lastmod(self, obj):
            return obj.updated_at
    ```

2. Update URL Configuration: Add the new sitemap class to the sitemaps dictionary in project/core/urls.py.

    ``` py title="urls.py"
    from project.apps.common.sitemaps import StaticViewSitemap, PostSitemap

    sitemaps = {
        "static": StaticViewSitemap,
        "posts": PostSitemap,
    }

    urlpatterns = [
        path("sitemap.xml", sitemap, {"sitemaps": sitemaps}, name="sitemap"),
        # ... other url patterns ...
    ]
    ```
### Updating Tests

To ensure your sitemaps are working correctly, you can create unit tests. Here’s how to test the StaticViewSitemap:

1. Create Test File: Add a test file test_sitemaps.py in project/tests/apps/common/.

    ``` py title="test_sitemaps.py"
        from django.test import TestCase
    from django.urls import reverse
    from project.apps.common.sitemaps import StaticViewSitemap

    class StaticViewSitemapTests(TestCase):
        """Tests for the StaticViewSitemap"""

        def setUp(self):
            """Set up the sitemap"""
            self.sitemap = StaticViewSitemap()

        def test_static_view_sitemap_items(self):
            """Test the items in the sitemap"""
            expected_items = {"pages:home", "pages:about", "pages:contact"}
            items = set(self.sitemap.items())
            self.assertTrue(expected_items.issubset(items))

        def test_static_view_sitemap_location(self):
            """Test the location of the items in the sitemap"""
            for item in self.sitemap.items():
                url = self.sitemap.location(item)
                self.assertTrue(url.startswith("/"))
                self.assertTrue(reverse(item) == url)
    ```

2. Run Tests: Use Django’s test runner to execute the tests.  Use project Make file targets to run tests.

    ``` bash
    make test-common
    ```

## Conclusion

Sitemaps are a crucial part of SEO, helping search engines to index your site more effectively. By following the steps outlined above, you can easily manage and extend sitemaps in your Django project.
