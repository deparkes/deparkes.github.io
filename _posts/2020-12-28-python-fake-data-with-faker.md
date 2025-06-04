---
layout: post
title: Python Fake Data With Faker
date: 2020-12-28 09:53:10.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- data
- data science
- fake data
- programming
- python
author: deparkes
permalink: "/2020/12/28/python-fake-data-with-faker/"
---
Fake data can be invaluable for testing or demonstrating behaviour without using live, production data. This lets you protect your production data or help you get started when you don't yet have a production system set up. This post gives an overview of the Python fake data package <a href="https://faker.readthedocs.io/en/stable/">faker</a>, which is invaluable for generating this data.
<h2>Faker Basics</h2>
Faker is easily able to handle basic biographic information such as name, address, phone number, sign-post other providers. An example of some of these basics is below:

```python
from faker import Faker
fake_data_generator = Faker()
Faker.seed(123)
# Some basics
# (defaults to US locale)
# Name
fake_data_generator.name()
# Address
fake_data_generator.address()
# Phone number
fake_data_generator.phone_number()
# Generate a whole profile
fake_data_generator.profile()
```

Faker uses the concept of a 'provider' to contain similar types of fake data. A provider can hold multiple methods, which are what you call to generate the data. The methods in each provider are available via the main faker object.

For example the <a href="https://faker.readthedocs.io/en/master/providers/faker.providers.address.html">address provider</a> contains the 'address' method to produce a whole address, as well as a 'building_number' to only generate a building number.
A list of available providers is available <a href="https://faker.readthedocs.io/en/master/providers.html">here.</a>
There are also community-made providers, see <a href="https://faker.readthedocs.io/en/stable/communityproviders.html">here</a>.
<h2>Creating a Custom Provider</h2>
The pre-made providers are often sufficient, but you may want to create your own if you have uncommon data you wish to fake, or find that the built-in providers do not have the richness you require.

Creating a custom provider is a matter of creating a class for your provider, along with generator methods for the fake data you wish to generate. Finally, the custom provider is added to the maker Faker generator object so the new provider methods are accessible.
In the following example we create a new generator for nationalities.

```python
import random
# we'll need this later to make a random choice from a list of possibles
fake_nationality_generator = Faker()
from faker.providers import BaseProvider
class NationalityProvider(BaseProvider):
    def nationality(self):
        nationality = ['French', 'Indian', 'Chinese']
        return random.choice(nationality)
fake_nationality_generator.add_provider(NationalityProvider)
fake_nationality_generator.nationality()
```

<h2>Working With Different Locales</h2>
When working with fake data it is likely that you'll want to have different information depending on the locale, for example different names and addresses for different nationalities. Not all providers are available for all locales. You can see a list of providers and locales <a href="https://faker.readthedocs.io/en/stable/locales.html">here</a>.

Setting the locale you are interested in can be done by specifying the locale when we instantiate the Faker object. In the example below we instantiate first a German faker object and then a Faker object based on Italian, US and Japanese locales.
<a href="https://faker.readthedocs.io/en/stable/fakerclass.html#locale-normalization">Read more about working with locales</a>.

```python
from faker import Faker
german_generator = Faker(['de_DE'])
german_generator.name()
# It is also possible to
multi_locale_generator = Faker(['it_IT', 'en_US', 'ja_JP'])
multi_locale_generator.name()
```

<h2>Generating Larger Multiple Records</h2>
You may find you want to use Faker to generate large amounts of data, rather than just single rows or items. You can wrap the faker in a for loop to generate multiple records (or use list comprehension).

```python
from faker import Faker
multi_faker = Faker()
for i in range(10):
    print(multi_faker.name())
# or use list comprehension:
[multi_faker.name() for i in range(10)]
```

You can also include those list comprehensions in a pandas data frame include a list comprehension in the data frame creation code

```python
from faker import Faker
import pandas as pd
multi_locale_generator = Faker(['de_DE', 'en_US', 'fr_FR'])
multi_locale_generator.name()
num_records = 5
df = pd.DataFrame({'name': [multi_locale_generator.name() for i in range(num_records)],
                   'date_of_birth': [multi_locale_generator.date_of_birth() for i in range(num_records)],
                   'address': [multi_locale_generator.address() for i in range(num_records)]
                   })
```

If you have performance issues with generating <a href="https://stackoverflow.com/questions/45574191/using-python-faker-generate-different-data-for-5000-rows">large volumes of fake data</a> then you may want to check out a similar project <a href="https://github.com/lk-geimfari/mimesis">mimesis</a>.
