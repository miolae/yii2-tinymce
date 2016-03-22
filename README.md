TinyMCE widget extension with inline mode support for Yii2 framework
====================================================================
There are about 20 extensions at [GitHub](http://github.com) which usually
wrap TinyMCE in Html::activeTextarea() or Html::textarea() so we got
htmlencoded content sent to the end user and moreover - TinyMCE wrapped in
textarea tag which is completely inacceptable to extremly usefull inline 
mode behavior.
 
This extension wrap TinyMCE with div tag and made it inline by default.

There are few things that better to fix and/or add more flexibility:

 * i18n for widget uses yii::$app->language settings but for English
 language it is changed to en_GB by default
 * content_css options ALWAYS use static url to '/css/site.css' file and
 dynamically detects location of the Bootstrap CSS
 * widget ALWAYS use beforeValidate event handler for changing name of
 hidden input generated by TinyMCE for correct posting form variables

Here is short description for parts used in final substitution:

```
$('#{$id}').attr('name');   // original name-attribute for inline editor
$('#{$id}').html();         // original post inside inline editor
$('[name={$id}]')           // hidden input
```

Installation
------------

The preferred way to install this extension should be [composer](http://getcomposer.org/download/).
But I am not ready yet to publish it at packagist, so you have to add
repository manually to your `composer.json`

```
"repositories": [
    {
        "type": "vcs",
        "url": "https://github.com/ComradePashka/yii2-tinymce.git"
    }
```

and add

```
"comradepashka/yii2-tinymce": "**"
```

to the require section of your `composer.json` file.

And then run

```
php composer.phar update
```


Usage
-----

```
$form->field($model, "body")->widget(TinyMce::className(), $optionsArray)
```