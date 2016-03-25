TinyMCE widget extension with inline mode support for Yii2 framework
====================================================================
There are about 20 extensions at [GitHub](http://github.com) which usually
wrap TinyMCE in Html::activeTextarea() or Html::textarea() so we got
htmlencoded content sent to the end user and moreover - TinyMCE wrapped in
textarea tag which is completely inacceptable to extremly usefull inline 
mode behavior.
 
This extension wrap TinyMCE with div tag and made it inline by default.

2do list
--------

There are few things that better to fix and/or add more flexibility:

 * i18n for widget uses yii::$app->language settings but for English
 language it will be changed to en_GB by default.
 Not the best way.
 * ~~content_css options ALWAYS use static url to '/css/site.css' file and
 dynamically detects location of the Bootstrap CSS.
 Have to figure out how to attach them automatically.~~ **See below**
 * widget ALWAYS use beforeValidate event handler for changing name of
 hidden input generated by TinyMCE for correct posting form variables

Here is short description for parts used in final substitution:

```
$('#{$id}').attr('name');   // original name-attribute for inline editor
$('#{$id}').html();         // original post inside inline editor
$('[name={$id}]')           // hidden input
```

Bugs
----

Due to dynamic change of form elements there might be strange behavior
related to CSRF. I've got HTTP 400 error during posting form data and couldn't
realize what happens but later when I switch languages in my app everything
start working normally.
Need more investigation.

Installation
------------

The preferred way to install this extension should be [composer](http://getcomposer.org/download/).
Now package published at [Packagist](https://packagist.org/packages/comradepashka/yii2-tinymce)
and support [Semantic Versioning](http://semver.org/)

So you either run

```
php composer.phar require --prefer-dist comradepashka/yii2-tinymce
```

or add

```
"comradepashka/yii2-tinymce": "*"
```

to the require section of your `composer.json` file.


Usage
-----

```
$form->field($model, "body")->widget(TinyMce::className(), $optionsArray)
```

Now you can pass configuration value 'extraCss' 

```
'extraCss' => "/css/site.css,/css/tinyMCE.css,",
```

using configuration array.

Styles will be used in addition to default bootstrap styles internally
in editor.
