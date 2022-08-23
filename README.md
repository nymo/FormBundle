naucon Form Bundle
==================

About
-----
Bundle to integrate naucon form package into the Symfony2 framework.


### Compatibility

* PHP 7.1 - 7.4


Installation
============

Step 1: Download the Bundle
---------------------------

Open a command console, enter your project directory and execute the
following command to download the latest stable version of this bundle:

```console
    composer require naucon/form-bundle
```

This command requires you to have Composer installed globally, as explained
in the [installation chapter](https://getcomposer.org/doc/00-intro.md)
of the Composer documentation.


Step 2: Enable the Bundle
-------------------------

Then, enable the bundle by adding it to the list of registered bundles
in the `app/AppKernel.php` file of your project:

```php
    <?php
    // app/AppKernel.php

    public function registerBundles()
    {
        $bundles = array(
            // ...
            new Naucon\Bundle\FormBundle\NauconFormBundle(),
        );
    }
```

Configuration
-------------

```yml
    naucon_form:
        csrf_parameter: "_csrf_token"
        csrf_protection: true
```

Get Started
-----------

```php
    class DefaultController extends Controller
    {
        public function newAction(Request $request)
        {
            $user = new User();

            $formFactory = $this->get('naucon_form.factory');

            $form = $formFactory->createForm($user, 'user');
            if ($form->isBound()
                && $form->isValid()) {
                // some action, like saving the data to database

                // redirect to success page
            }

            return $this->render('default/new.html.twig', array(
                'form' => $form
            ));
        }
    }
```

Twig Form Extension
------------------------
At the moment we support just a set of form functions which will be further extended in the near future.

Each function expects as a first value a form object which implements the Forminterface

**Simple call**
```php
 {{ ncform_start(form) }}
 {{ ncform_field(form, 'text', 'activation_code') }}
 {{ ncform_end(form) }}
```

**Full featured call**
```php
 {{ ncform_start(form, method='post', action='some-action', enctype='some type', {furtherOptions:'option'}) }}
 {{ ncform_field(form, 'text', 'activation_code', { style: 'some style', id: 'some id', value: 'some value', maxlength: 'some lenght', class: 'css class', required: 'required', 'data-attribute': 'some attribute'}) }}
 {{ ncform_end(form) }}
```

**ncform_field**

This function accepts currently only the following options: 
- style
- class
- id
- value
- maxlength
- required
- data-*


Roadmap
-------
* add more twig form functions
* add naucon validator to translations
