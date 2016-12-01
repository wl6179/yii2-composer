Yii 2 Composer Installer
========================

This is the composer installer for [Yii framework 2.0](http://www.yiiframework.com) extensions.
It implements a new composer package type named `yii2-extension`,
which should be used by all Yii 2 extensions if they are distributed as composer packages.

For license information check the [LICENSE](LICENSE.md)-file.

[![Latest Stable Version](https://poser.pugx.org/yiisoft/yii2-composer/v/stable.png)](https://packagist.org/packages/yiisoft/yii2-composer)
[![Total Downloads](https://poser.pugx.org/yiisoft/yii2-composer/downloads.png)](https://packagist.org/packages/yiisoft/yii2-composer)


Usage
-----

To use Yii 2 composer installer, simply set `type` to be `yii2-extension` in your `composer.json`,
like the following:

```json
{
    "type": "yii2-extension",
    "require": {
        "yiisoft/yii2": "*"
    },
    ...
}
```

You may specify a bootstrapping class in the `extra` section. The `init()` method of the class will be executed each time
the Yii 2 application is responding to a request. For example,

```json
{
    "type": "yii2-extension",
    ...,
    "extra": {
        "bootstrap": "yii\\jui\\Extension"
    }
}
```

The `Installer` class also implements a static method `postCreateProject()` that can be called after
a Yii 2 project is created, through the `post-create-project-cmd` composer script.
The method allows to run other `Installer` class methods like `setPermission()` or `generateCookieValidationKey()`, 
depending on the corresponding parameters set in the `extra` section of the `composer.json` file.
For example,

```json
{
    "name": "yiisoft/yii2-app-basic",
    "type": "project",
    ...
    "scripts": {
        "post-create-project-cmd": [
            "yii\\composer\\Installer::postCreateProject"
        ]
    },
    "extra": {
        "yii\\composer\\Installer::postCreateProject": {
            "setPermission": [
                {
                    "runtime": "0777",
                    "web/assets": "0777",
                    "yii": "0755"
                }
            ],
            "generateCookieValidationKey": [
                "config/web.php"
            ]
        }
    }
}
```
