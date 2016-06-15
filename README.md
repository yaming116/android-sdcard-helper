Android SQLiteSDCardHelper
=========================

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://github.com/yaming116/android-sdcard-helper/blob/master/LICENSE)
[![Jitpack](https://www.jitpack.io/v/yaming116/android-sdcard-helper.svg)](https://www.jitpack.io/#yaming116/android-sdcard-helper)

An Android helper class to manage database creation and version management store in sdcard.

This class provides developers with a simple way to ship their Android app with an existing SQLite database (which may be pre-populated with data) and to manage its initial creation and any upgrades required with subsequent version releases.

It is implemented as an extension to `SQLiteOpenHelper`, providing an efficient way for `ContentProvider` implementations to defer opening and upgrading the database until first use.

Rather than implementing the `onCreate()` and `onUpgrade()` methods to execute a bunch of SQL statements. These will include the initial SQLite database file for creation and optionally any SQL upgrade scripts.

Setup
-----

#### Gradle

If you are using the Gradle build system, simply add the following dependency in your `build.gradle` file:

```groovy

allprojects {
	repositories {
	
		maven { url "https://www.jitpack.io" }
	}
}

dependencies {
    compile 'com.github.yaming116:android-sdcard-helper:1.0.0'
}
```

#### Ant/Eclipse

If you are using the old build system, download the latest library [JAR][1] and put it in your project's `libs` folder.

Usage
-----

SQLiteSDCArdHelper is intended as a drop in alternative for the framework's [SQLiteOpenHelper](https://developer.android.com/reference/android/database/sqlite/SQLiteOpenHelper.html). Please familiarize yourself with the behaviour and lifecycle of that class.

Extend `SQLiteSDCardHelper` as you would normally do `SQLiteOpenHelper`, providing the constructor with a database name and version number:

```java
public class MyDatabase extends SQLiteSDCardHelper {

    private static final String DATABASE_NAME = "northwind.db";
    private static final int DATABASE_VERSION = 1;

    public MyDatabase(Context context) {
	    super(context, DATABASE_NAME, null, DATABASE_VERSION);
    }
}
```

Database Upgrades
-----------------

At a certain point in your application's lifecycle you will need to alter it's database structure to support additional features. You must ensure users who have installed your app prior to this can safely upgrade their local databases without the loss of any locally held data.

To facilitate a database upgrade, increment the version number that you pass to your `SQLiteSDCardHelper` constructor:

```java
private static final int DATABASE_VERSION = 2;
```

### Generating upgrade scripts

You can use 3rd party tools to automatically generate the SQL required to modify a database from one schema version to another. One such application is [SQLite Compare Utility](http://www.codeproject.com/KB/database/SQLiteCompareUtility.aspx) for Windows.

Credits
-------

####Author:

  * [yaming116](https://github.com/yaming116)

#### Contributors:
  * [Jeff Gilfelt](https://github.com/jgilfelt)
  * [Alexandros Schillings](https://github.com/alt236)
  * [Cyril Mottier](https://github.com/cyrilmottier)
  * [Jon Adams](https://github.com/jon-adams)
  * [Kevin](https://github.com/kevinchai)

License
-------

    Copyright (C) 2011 花开堪折枝 Software Ltd
    Copyright (C) 2011 readyState Software Ltd
    Copyright (C) 2007 The Android Open Source Project

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

 [1]: https://www.jitpack.io/com/github/yaming116/android-sdcard-helper/1.0.0/android-sdcard-helper-1.0.0.jar
