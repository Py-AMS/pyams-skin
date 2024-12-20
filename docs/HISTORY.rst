Changelog
=========

2.4.0
-----
 - added custom mapping widget and data converter

2.3.0
-----
 - added dotted decimal field data converter
 - make menu URL property as not required

2.2.4
-----
 - updated widget configuration getter of TinyMCE HTML editor
 - updated object field input template

2.2.3
-----
 - added MyAMS target URL support to submit button

2.2.2
-----
 - updated doctests

2.2.1
-----
 - added condition to display icon tag in menu item
 - updated dynamic select widget terms factory

2.2.0
-----
 - added support for custom modal content class

2.1.1
-----
 - added translation for Bootstrap status labels

2.1.0
-----
 - updated modal page layout
 - added modal forms interfaces

2.0.2
-----
 - updated Buildout configuration

2.0.1
-----
 - updated doctests

2.0.0
-----
 - upgraded to Pyramid 2.0
 - added color selection widget

1.11.0
------
 - viewlets refactoring
 - updated Bootstrap thumbnails selection field
 - added metas headers to fullpage modal layout

1.10.0
------
 - added form errors viewlet
 - updated base form template to include errors
 - updated time data converter
 - update date and datetime ranges schema fields interfaces

1.9.0
-----
 - added new textline widgets with button to copy input value to clipboard

1.8.4
-----
 - updated default field management of Bootstrap thumbnails selection field to be able to
   set default column width for each device

1.8.3
-----
 - code cleanup

1.8.2
-----
 - doctests update

1.8.1
-----
 - templates updates

1.8.0
-----
 - added new schema field and widget to handle selection of boolean values matching Bootstrap
   devices; this is used for example in PyAMS_portal to select devices for which a given portlet
   is displayed or not
 - added support for Python 3.11
 - renamed Bootstrap thumbnail selection schema field and widget
 - updated doctests


1.7.2
-----
 - updated translations

1.7.1
-----
 - updated HTML editor widget configuration getter

1.7.0
-----
 - added Bootstrap images thumbnails selection schema field and widget
 - added support for Python 3.10
 - handle optional icon on action button
 - updated ordered select input widget template to correctly handle items order
 - merged resources management adapters in PyAMS_layer package
 - replace formats with f-strings

1.6.2
-----
 - updated default widget layout

1.6.1
-----
 - updated widgets templates
 - added base class for adding actions

1.6.0
-----
 - added custom template for ordered select widget
 - added CSS class property to context actions viewlet
 - updated condition to display form's fieldset border
 - updated components CSS class

1.5.3
-----
 - added missing text lines widget input template
 - updated form's fieldset class handler

1.5.2
-----
 - added content-type and charset metas headers
 - added support of AJAX params to Select2 input widget
 - updated translation

1.5.1
-----
 - updated actions templates

1.5.0
-----
 - removed support for Python < 3.7
 - added flex classes to main form template
 - added custom widgets for date and datetime ranges fields
 - added check in dynamic select terms factory
 - updated text lines display widget template
 - updated dropdown menus templates

1.4.0
-----
 - updated forms templates
 - added forms header and footer viewlet managers
 - updated Gitlab-CI configuration
 - removed Travis-CI configuration

1.3.1
-----
 - updated doctests for Gitlab-CI

1.3.0
-----
 - added TALES "metas" extension and base classes to handle metas headers
 - added custom ObjectWidget layout and templates
 - defined SingleCheckboxFieldWidget as default widget factory for boolean fields

1.2.0
-----
 - added breadcrumbs viewlet manager
 - added datetime, date and time input widgets
 - small updates in forms templates
 - updated doctests

1.1.1
-----
 - added attribute to store values separator in OrderedListWidget
 - added missing editor options attribute to HTML input widget template
 - updated doctests

1.1.0
-----
 - added form widget for HTTPMethod schema field
 - added form widget for OrderedList schema field

1.0.5
-----
 - package version mismatch

1.0.4
-----
 - updated forms legend display condition

1.0.3
-----
 - updated forms templates

1.0.2
-----
 - updated Sonar properties

1.0.1
-----
 - updated Gitlab-CI configuration

1.0.0
-----
 - initial release
