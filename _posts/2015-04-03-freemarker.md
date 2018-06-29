---
layout: page
title: "Freemarker"
permalink: /doc/templates/freemarker.html
date: 2015-04-03 15:39:09
---

[Freemarker][freemarker] is a template engine for Java.

#### Setup

1) Add the `pippo-freemarker` dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>ro.pippo</groupId>
    <artifactId>pippo-freemarker</artifactId>
    <version>${pippo.version}</version>
</dependency>
```

2)  Start writing [Freemarker][freemarker] templates in the `templates` folder of your application.  

**Note:** The default file extension of a Freemarker template is `.ftl` and it may be omitted from your templates and your Pippo Java code.

#### Integration

This engine includes some useful Pippo integration features and conveniences like... 

##### i18n

You can access your translation resources using the i18n method.

```
${i18n("key.name")}
```

You can supply arguments to your *MessageFormat* translation resources too.

```
${i18n("key.name", "arg1", "arg2")}
```

##### prettytime (relative time)

The `pippo-freemarker` module supports automatically localized [prettytime][prettytime] out-of-the-box and it is very easy to use.

Assuming you are providing a `java.util.Date` instance to prettyTime...

```
${prettyTime(myDate)}
```

Will produce something like...

```
3 days ago
```

##### formatTime

You can also automatically format localized dates using standard Java date format patterns.

```
${formatTime(now)}
${formatTime(now, "short")}
${formatTime(now, "medium")}
${formatTime(now, "long")}
${formatTime(now, "full")}
${formatTime(now, "HH:mm")}
${formatTime(now, "dd-MM-yyyy HH:mm")}
${formatTime(now, "dd-MM-yyyy HH:mm")}
```    

##### webjarsAt & publicAt

The `pippo-freemarker` module supports context-aware url generation for your classpath resources using the `webjarsAt` and `publicAt` methods.

```html
<!-- Stylesheets -->
<link href="${webjarsAt('bootstrap/3.3.1/css/bootstrap.min.css')}" rel="stylesheet">
<link href="${webjarsAt('font-awesome/4.2.0/css/font-awesome.min.css')}" rel="stylesheet">
<link href="${publicAt('css/style.css')}" rel="stylesheet">

<!-- Scripts -->
<script src="${webjarsAt('jquery/1.11.1/jquery.min.js')}"></script>
<script src="${webjarsAt('bootstrap/3.3.1/js/bootstrap.min.js')}"></script>
<script src="${publicAt('js/main.js')}"></script>
```

**NOTE:** Use of these methods require that you have registered a `WebjarsResourceRoute` and/or a `PublicResourceRoute`.

```java
public class MyApplication extends Application {

    @Override
    protected void onInit() {
        // add routes for static content
        addPublicResourceRoute();
        addWebjarsResourceRoute();
        
        // add other routes
    }
    
}
```

##### Error Templates

The `pippo-freemarker` module  will render special templates for routing problems and exceptions. 
You may override these templates within your own application (put a file with the same name, to same location, in your application classpath)

- `templates/pippo/404notFound.ftl`
- `templates/pippo/500interalError.ftl`

[freemarker]: http://freemarker.org
[prettytime]: http://ocpsoft.org/prettytime
