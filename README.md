# django-zxcvbn-password-validator

A translatable password validator for django, based on zxcvbn-python and available with pip.

[![Build Status](https://travis-ci.org/Pierre-Sassoulas/django-zxcvbn-password-validator.svg?branch=master)](https://travis-ci.org/Pierre-Sassoulas/django-zxcvbn-password-validator)
[![Coverage Status](https://coveralls.io/repos/github/Pierre-Sassoulas/django-zxcvbn-password-validator/badge.svg?branch=master)](https://coveralls.io/github/Pierre-Sassoulas/django-zxcvbn-password-validator?branch=master)
[![PyPI version](https://badge.fury.io/py/django-zxcvbn-password-validator.svg)](https://badge.fury.io/py/django-zxcvbn-password-validator)

## Creating a user with django-zxcvbn-password-validator

If the password is not strong enough, we provide errors explaining what you need to do :

![English example](doc/english_example.png "English example")

The error message are translated to your target language (even the string given by zxcvbn that are in english only) :

![Translated example](doc/french_example.png "Translated example")

## How to use

Add it to your requirements and get it with pip.

````
django-zxcvbn-password-validator
````

Then everything happens in your settings file.

Add `'django_zxcvbn_password_validator'` in the `INSTALLED_APPS` :

````python
INSTALLED_APPS = [
	...
	'django_zxcvbn_password_validator'
]
````

Modify `AUTH_PASSWORD_VALIDATORS` :

````python
AUTH_PASSWORD_VALIDATORS = [
	{
		'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
	},
	{
		'NAME': 'django_zxcvbn_password_validator.ZxcvbnPasswordValidator',
	},
	...
]
````

You could choose to use zxcvbn alone, but I personally still use Django's `UserAttributeSimilarityValidator`,
because there seems to be still be some problem with it integrating user informations with zxcvbn (as of june 2018).

Finally you can set the `PASSWORD_MINIMAL_STRENGH` to your liking (default is 2),
every password scoring lower than this number will be rejected :

````python
# 0 too guessable: risky password. (guesses < 10^3)
# 1 very guessable: protection from throttled online attacks. (guesses < 10^6)
# 2 somewhat guessable: protection from unthrottled online attacks. (guesses < 10^8)
# 3 safely unguessable: moderate protection from offline slow-hash scenario. (guesses < 10^10)
# 4 very unguessable: strong protection from offline slow-hash scenario. (guesses >= 10^10)
````

## Translating the project

This project is available in multiple language.
Your contribution would be very appreciated if you
know a language that is not yet available.

### Language available

The following languages are available:

- [x] Dutch thanks to Thom Wiggers (@thomwiggers)
- [x] French thanks to Pierre Sassoulas (@Pierre-Sassoulas)
- [x] English

## Contributing

### Lint

````bash
isort -rc django_zxcvbn_password_validator
pylint django_zxcvbn_password_validator
````

### Testing

````bash
python manage.py test
````

### Coverage

````bash
coverage run ./manage.py test
coverage html
# Open htmlcov/index.html in a navigator
````

### I18n

````bash
python manage.py makemessages
# python manage.py createsuperuser ? (You need to login for rosetta)
python manage.py runserver
# Access http://localhost:8000/admin to login
# Then go to http://localhost:8000/rosetta to translate
python manage.py makemessages --no-obsolete --no-wrap
````
