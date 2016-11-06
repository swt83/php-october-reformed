# Reformed for October

An OctoberCMS form model, assisting in the PRG form pattern.

## Install

Normal install via Composer.

## Usage

We are just using the normal [Reformed](https://github.com/swt83/php-laravel-reformed) model, but to make it work w/ October we need to add some special sauce.

When working w/ components, add this to your component class:

```php
use Author\Name\Classes\Forms\FoobarForm

function onRun()
{
    // if post...
    if (\Request::isMethod('post'))
    {
        // redirect
        return FoobarForm::run();
    }

    // bind
    $this->page['input'] = \Input::all();
    $this->page['alert'] = FoobarForm::get_alert();
}
```

When working w/ pages or partials, add this to your code section:

```php
use Author\Name\Classes\Forms\FoobarForm

function onStart()
{
    // if post...
    if (\Request::isMethod('post'))
    {
        // redirect
        return FoobarForm::run();
    }

    // bind
    $this['input'] = \Input::all();
    $this['alert'] = FoobarForm::get_alert();
}
```

When building your form using Twig, in either a component or a partial, do something like this:

```
{{ form_open() }}
{% if (alert.msg) %}
    <div class="alert {{ alert.level }}">
        <ul>
        {% for m in alert.msg %}
            <li>{{ m }}</li>
        {% endfor %}
        </ul>
    </div>
{% endif %}
{{ form_label('first', 'First *') }}
{{ form_text('first', input.first) }}
{{ form_label('last', 'Last *') }}
{{ form_text('last', input.last) }}
{{ form_label('email', 'Email *') }}
{{ form_text('email', input.email) }}
{{ form_label('subject', 'Subject *') }}
{{ form_text('subject', input.subject) }}
{{ form_label('message', 'Message *') }}
{{ form_textarea('message', input.message) }}
{{ form_submit('Submit') }}
{{ form_close() }}
```
