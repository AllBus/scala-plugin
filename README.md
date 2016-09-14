# Scala-plugin for Android

This is mod of gradle-android-scala-plugin from

https://github.com/saturday06/gradle-android-scala-plugin

This version of plugin supported gradle version 2.14.1 and gradle tools 2.1.2


# How to use

In android gradle project

## Setting Gradle

### for Gradle 3.0

1) Open gradle-wrapper.properties and replace version gradle on 3.0

	distributionUrl=https\://services.gradle.org/distributions/gradle-3.0-all.zip

2) in `build.gradle` project
```
	buildscript {
		repositories {
			jcenter()
		}
		dependencies {
			classpath 'com.android.tools.build:gradle:2.2.0-rc2'
			classpath 'jp.leafytree.gradle:gradle-android-scala-plugin:1.4'
		}
	}

	allprojects {
		repositories {
			jcenter()
		}
	}

	ScalaCompileOptions.metaClass.useAnt = false
	
	task clean(type: Delete) {
		delete rootProject.buildDir
	}
```
3) in `build.gradle` module
```
	apply plugin: 'com.android.application'
	apply plugin: 'jp.leafytree.android-scala'

	android {
		compileSdkVersion 24
		buildToolsVersion "24.0.1"

		defaultConfig {
			applicationId "com.mycompany.myproject"
			targetSdkVersion 24
			versionCode 1
			versionName "1.0"
		}
		productFlavors {
			dev {
				minSdkVersion 21 // To reduce compilation time
			}

			prod {
				minSdkVersion 16
			}
		}

		buildTypes {
			release {
				minifyEnabled false
				proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
			}
		}
	}

	dependencies {
		compile fileTree(include: ['*.jar'], dir: 'libs')
		testCompile 'junit:junit:4.12'
		compile 'com.android.support:appcompat-v7:24.1.1'
		compile 'org.scala-lang:scala-library:2.11.8'
	}


	tasks.withType(ScalaCompile) {
			scalaCompileOptions.metaClass.useCompileDaemon = true
			scalaCompileOptions.metaClass.deprecation = false
			scalaCompileOptions.metaClass.additionalParameters = ["-feature","-Xexperimental","-optimise"]
			ScalaCompileOptions.metaClass.useAnt = false
	}
```

### for Gradle 2.14

1) Open gradle-wrapper.properties and replace version gradle on 2.14.1

	distributionUrl=https\://services.gradle.org/distributions/gradle-2.14.1-all.zip

2) in `build.gradle` project
```
	buildscript {
		repositories {
			jcenter()
		}
		dependencies {
			classpath 'com.android.tools.build:gradle:2.1.2'
			classpath 'jp.leafytree.gradle:gradle-android-scala-plugin:1.4'
		}
	}

	allprojects {
		repositories {
			jcenter()
		}
	}

	task clean(type: Delete) {
		delete rootProject.buildDir
	}
```
3) in `build.gradle` module
```
	apply plugin: 'com.android.application'
	apply plugin: 'jp.leafytree.android-scala'

	android {
		compileSdkVersion 24
		buildToolsVersion "24.0.1"

		defaultConfig {
			applicationId "com.mycompany.myproject"
			targetSdkVersion 24
			versionCode 1
			versionName "1.0"
		}
		productFlavors {
			dev {
				minSdkVersion 21 // To reduce compilation time
			}

			prod {
				minSdkVersion 16
			}
		}

		buildTypes {
			release {
				minifyEnabled false
				proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
			}
		}
	}

	dependencies {
		compile fileTree(include: ['*.jar'], dir: 'libs')
		testCompile 'junit:junit:4.12'
		compile 'com.android.support:appcompat-v7:24.1.1'
		compile 'org.scala-lang:scala-library:2.11.8'
	}


	tasks.withType(ScalaCompile) {
		scalaCompileOptions.useCompileDaemon = true
		scalaCompileOptions.deprecation = false
		scalaCompileOptions.additionalParameters = ["-feature"]
	}
```



## Replace plugin file

4) Sync Now gradle

5) In explorer open folder `C:/users/MyName/.gradle/`

6) find `gradle-android-scala-plugin-1.4.jar`

8) Close Android Studio

7) Replace `gradle-android-scala-plugin-1.4.jar` file this modification

8) Open Android Studio

9) Compile project. Congratulations.
