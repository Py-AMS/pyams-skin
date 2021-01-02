==================
PyAMS_skin package
==================

Introduction
------------

This package is composed of a set of utility functions, usable into any Pyramid application.

    >>> import pprint

    >>> from pyramid.testing import setUp, tearDown
    >>> config = setUp(hook_zca=True)

    >>> from pyams_utils import includeme as include_utils
    >>> include_utils(config)
    >>> from pyams_form import includeme as include_form
    >>> include_form(config)
    >>> from pyams_skin import includeme as include_skin
    >>> include_skin(config)

    >>> from pyams_utils.testing import call_decorator
    >>> from pyams_utils.adapter import adapter_config


Custom buttons
--------------

    >>> from pyams_layer.interfaces import IFormLayer

    >>> from pyams_form.interfaces.button import IButtonAction
    >>> from pyams_form.interfaces.widget import IFieldWidget

    >>> from pyams_skin.interfaces.form import IActionButton, ICloseButton, IResetButton, ISubmitButton
    >>> from pyams_skin.interfaces.widget import IActionWidget, ICloseWidget, IResetWidget, ISubmitWidget

    >>> from pyams_skin.widget.button import SubmitFieldWidget, SubmitButtonAction
    >>> call_decorator(config, adapter_config, SubmitFieldWidget,
    ...                required=(ISubmitButton, IFormLayer), provides=IFieldWidget)
    >>> call_decorator(config, adapter_config, SubmitButtonAction,
    ...                required=(IFormLayer, ISubmitButton), provides=IButtonAction)

    >>> from pyams_skin.widget.button import ActionFieldWidget, ActionButtonAction
    >>> call_decorator(config, adapter_config, ActionFieldWidget,
    ...                required=(IActionButton, IFormLayer), provides=IFieldWidget)
    >>> call_decorator(config, adapter_config, ActionButtonAction,
    ...                required=(IFormLayer, IActionButton), provides=IButtonAction)

    >>> from pyams_skin.widget.button import ResetFieldWidget, ResetButtonAction
    >>> call_decorator(config, adapter_config, ResetFieldWidget,
    ...                required=(IResetButton, IFormLayer), provides=IFieldWidget)
    >>> call_decorator(config, adapter_config, ResetButtonAction,
    ...                required=(IFormLayer, IResetButton), provides=IButtonAction)

    >>> from pyams_form.testing import TestRequest

    >>> from zope.interface import alsoProvides, Interface
    >>> from pyams_skin.schema.button import SubmitButton, ActionButton, ResetButton, CloseButton

    >>> class ITestButtons(Interface):
    ...     submit = SubmitButton(name='submit', title="Submit")
    ...     action = ActionButton(name='action', title="Action")
    ...     reset = ResetButton(name='reset', title="Reset")
    ...     close = CloseButton(name='close', title="Close")

    >>> from pyams_form.button import Buttons
    >>> from pyams_form.field import Fields
    >>> from pyams_form.form import EditForm

    >>> class TestForm(EditForm):
    ...     buttons = Buttons(ITestButtons)
    ...     fields = Fields(Interface)

    >>> request = TestRequest()
    >>> alsoProvides(request, IFormLayer)
    >>> IFormLayer.providedBy(request)
    True

    >>> form = TestForm(None, request)
    >>> form.update()

    >>> 'submit' in form.actions
    True
    >>> form.actions['submit']
    <SubmitButtonAction 'form.buttons.submit' 'Submit'>
    >>> form.actions['submit'].render()
    '<input type="submit"\n       id="form-buttons-submit"\n       name="form.buttons.submit"\n       class="submit-widget submitbutton-field"\n       value="Submit" />'

    >>> 'action' in form.actions
    True
    >>> form.actions['action']
    <ActionButtonAction 'form.buttons.action' 'Action'>
    >>> form.actions['action'].render()
    '<input type="submit"\n       id="form-buttons-action"\n       name="form.buttons.action"\n       class="submit-widget actionbutton-field"\n       value="Action" />'

    >>> 'reset' in form.actions
    True
    >>> form.actions['reset']
    <ResetButtonAction 'form.buttons.reset' 'Reset'>
    >>> form.actions['reset'].render()
    '<input type="submit"\n       id="form-buttons-reset"\n       name="form.buttons.reset"\n       class="submit-widget resetbutton-field"\n       value="Reset" />'

    >>> 'close' in form.actions
    True
    >>> form.actions['close']
    <CloseButtonAction 'form.buttons.close' 'Close'>
    >>> form.actions['close'].render()
    '<input type="submit"\n       id="form-buttons-close"\n       name="form.buttons.close"\n       class="submit-widget closebutton-field"\n       value="Close" />'


Custom form fields
------------------

    >>> from zope.schema import Tuple, TextLine
    >>> from pyams_utils.schema import HTTPMethodField

    >>> class IMyContent(Interface):
    ...     list_field = Tuple(title="List field",
    ...                        value_type=TextLine())
    ...     http_method = HTTPMethodField(title="HTTP method")

    >>> from zope.interface import implementer
    >>> from zope.schema.fieldproperty import FieldProperty

    >>> @implementer(IMyContent)
    ... class MyContent:
    ...     list_field = FieldProperty(IMyContent['list_field'])
    ...     http_method = FieldProperty(IMyContent['http_method'])

    >>> content = MyContent()
    >>> content.list_field = ('value 1', 'value2')
    >>> content.http_method = ('POST', '/api/auth/jwt/token')

    >>> from zope.interface import alsoProvides
    >>> from pyams_layer.interfaces import IFormLayer

    >>> request = TestRequest(context=content)
    >>> alsoProvides(request, IFormLayer)

    >>> from pyams_skin.widget.list import OrderedListFieldWidget
    >>> list_widget = OrderedListFieldWidget(IMyContent['list_field'], request)
    >>> list_widget.extract()
    <NO_VALUE>

    >>> request = TestRequest(context=content, params={
    ...     'list_field': 'value2;value1'
    ... })
    >>> alsoProvides(request, IFormLayer)
    >>> list_widget = OrderedListFieldWidget(IMyContent['list_field'], request)
    >>> list_widget.extract()
    ('value2', 'value1')

    >>> from pyams_form.interfaces.form import IContextAware
    >>> from pyams_skin.widget.http import HTTPMethodFieldWidget, HTTPMethodDataConverter

    >>> http_widget = HTTPMethodFieldWidget(IMyContent['http_method'], request)
    >>> http_widget.context = content
    >>> alsoProvides(http_widget, IContextAware)
    >>> http_widget.update()
    >>> http_widget.value
    ('POST', '/api/auth/jwt/token')
    >>> http_widget.display_value
    ('POST', '/api/auth/jwt/token')

    >>> http_widget.extract()
    <NO_VALUE>

    >>> request = TestRequest(context=content, params={
    ...     'http_method-empty-marker': '1',
    ...     'http_method-verb': 'GET',
    ...     'http_method-url': '/api/auth/jwt/another'
    ... })
    >>> http_widget = HTTPMethodFieldWidget(IMyContent['http_method'], request)
    >>> http_widget.context = content
    >>> alsoProvides(http_widget, IContextAware)
    >>> http_widget.extract()
    ('GET', '/api/auth/jwt/another')
    >>> http_widget.http_methods
    ('GET', 'POST', 'PUT', 'PATCH', 'HEAD', 'OPTIONS', 'DELETE')


Tests cleanup:

    >>> tearDown()
