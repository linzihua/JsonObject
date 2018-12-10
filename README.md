# JsonObject

JsonObject is a class witch provide some very simple way to access settings file(witch in xml format or json format).
Just using simply string key to get/set setting value. And the key is support xml path(split by /) or json path(split by dot).

Installation:
  **Install-Package JsonObject**

# Create Instance #
``` c#
var setting = new JsonObject();
//Load exist setting from json file
var setting = new JsonObject("setting.json"); 
//Load exist setting from xml file
var setting = new JsonObject("setting.xml"); 
```

# Set Value #
There is only one way to set one setting value:
``` c#
setting["Cache.Level"] = 1; 
//or
setting["Cache/Level"] = 1;
```
# Get Value #
There are two ways to get one setting value:
``` c#
//using dictionary key
var level = settig["Cache.Level"]; //return object or null if the key do not exist
//or GetValue<T>()
var level = settig.GetValue<int>("Cache.Level");//return value of key in specific type of default(T) if the key do not exist
```
# Save to settings file #
``` c#
// save to json file
setting.SaveFile("setting.json"); 
//save to xml file
setting.SaveFile("setting.xml"); 
```
# Load from settings file #
``` c#
var setting = new JsonObject();
//Load from json file
setting.LoadFile("setting.json"); 
//Load from xml file
setting.LoadFile("setting.xml"); 
```
# Advance Topic #
for xml attribute, add prefix '@' to the last key in xml path, such as:
``` c#
var setting = new JsonObject();
setting["appsetting.Cache.@Level"] = 1; 
setting.SaveFile("setting.xml"); 
```
output:
``` xml
<?xml version="1.0" encoding="utf-8"?>
<appsetting>
	<Cache Level="1" />
</appsetting>
``` 

otherwise:
``` c#
var setting = new JsonObject();
setting["appsetting.Cache.Level"] = 1; 
setting.SaveFile("setting.xml"); 
```
output:
``` xml
<?xml version="1.0" encoding="utf-8"?>
<appsetting>
	<Cache>
		<Level>1</Level>
	</Cache>
</appsetting>
``` 

# Auto initialize setting if settings file do not exist #
``` c#
var init = new Dictionary<string, object>()
{
  {"Cache.Level",1 }
};
var setting = new JsonObject("settingfile.json", init);
```

