# django-simplecrud

Create-Review-Update-Delete view and template framework for Django


## Installation

From the top directory of django-crud, run `setup.py install` 


## Usage

1. Add `'simplecrud'` to `INSTALLED_APPS`

2. Define CRUD_SETTINGS in your Django project `settings.py` file. The variable 
is a dictionary that sets certain  parameters for simplecrud. For now there is
only a parameter to set the navbar menu for pages generated by the library: 

	`navbar_menu`: a HTML-safe string. A series of `<li>` tags describing 
	the Bootstrap3 navbar menu options

	For example:

	```python
	CRUD_SETTINGS = {
	    'navbar_menu':  '<li class="active"><a href="/">Home</a></li>',
	}
	```
	
	The `navbar_menu` can be changed dynamically within your code to make the 
	manu bar responsive to what is going on with your site. In a simplecrud 
	template CRUD_SETTINGS can be accessed through the context as `simplecrud`.
	For example:
	
	```
	{{ simplecrud.navbar_menu }}
	```

    #### Overwriting Templates
    
    Any default template can be overwriten in the normal way: by creating a 
    folder in your project template directory (`templates/simplecrud`) and 
    copying the library templates. For example, you could copy the 
    `copyright.html` and `logo.html` templates to setup your site's own 
    copyright message and logo.

3. Add the URL patterns to the models you wish to access through the CRUD library.
For example:

	in the main `urls.py`

	```python
	urlpatterns = patterns('',
		...
		
	    url(r'^mymodel/', include('mymodel.urls') ),
	
		...
	)
	```

	Then in `mymodel/urls.py`

	```python
	import crud
	from .models import MyModel
	
	url_patters = crud.urls(MyModel)
	```
	
	This will create a series of URLs:
	
	```
	/mymodel/create
	/mymodel/update
	/mymodel/delete
	/mymodel/list
	/mymodel/formset
	```

	The `urls` function accepts other parameters such as the forms to be 
	used for create and update, queryset for list and formset and redirect 
	URL for succesful use of create, update, delete and formset

4. Each view accepts a series of options that customise their behaviour. Until
the documentation is expanded, please inspect the code for instructions. The 
default behaviour of the views will be a good guide to how these can be changed 
until better documentation becomes available.

