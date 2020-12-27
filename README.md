# MMM-Icestatus
A MagicMirror module that displays information from any Icecast Server

## What it Looks Like!
Nothing too pretty, just the data you want to see :)

There are some config options to make the json keys a bit prettier though, mentioned below in the config.

![Screenshot](https://raw.githubusercontent.com/wirelessphreak/MMM-Icestatus/master/Screenshot.png)

Here is the above json example data:
```
{
  "andrewMcolash":true,
  "AndrewMc":"123",
  "test_this":["a","b","c"],
  "Test_This":{"e":true,"f":"abc"}
}
```

## Install
`cd MagicMirror/modules`
`git clone https://github.com/wirelessphreak/MMM-Icestatus.git`

## Update
`cd MagicMirror/modules/MMM-Icestatus`
`git pull`

## Configuration
It is very simple to set up this module, a sample configuration looks like this:

```
modules: [
  {
    module: 'MMM-Icestatus',
    position: 'bottom_bar',
    config: {
      urls: [
        'http://your.server.json.here/abc1.json',
        'http://your.server.json.here/abc2.json',
      ]
    }
  }
]
```

## Configuration Options

| Option               | Description
| -------------------- | -----------
| `prettyName`         | Pretty print the name of each JSON key (remove camelCase and underscores). <br><br> **Default value:** `true`
| `stripName`          | Removes all keys before the printed key. <br><br>**Example:** `a.b.c` will print `c`.<br> **Default value:** `true`
| `title`              | Title to display at the top of the module. <br><br> **Default value:** `JSON Feed`
| `urls`               | An array of urls for your json feeds. Note that duplicate keys *WILL* be clobbered.<br><br> **Default value:** `REQUIRED`
| `url`                | **DEPRECATED, Please use `urls` instead.**<br>~~The url of the json feed. <br> **Default value:** `REQUIRED`~~
| `updateInterval`     | The time between updates (In milliseconds). <br><br> **Default value:** `300000 (5 minutes)`
| `singleLine`         | Display all values on a single line.<br><br> **Default value:** `false`
| `values`             | Specify specific values from the json feed to only show what you need. <br><br>**Example:** `["key1", "key2", "keyA.keyB.keyC"]`<br> **Default value:** `[]` (Shows all keys in the object)
| `arrayName`          | Name of array of items to iterate through.<br><br> **Default value:** `undefined`
| `arraySize`          | Number of array of items to show.<br><br> **Default value:** `999`
| `replaceName`        | Specify key names to replace in the json. This is an array of arrays [find, replace]<br><br>**Example:** `[ ["body", "replaced body"], ["id", "replacedID"] ]`<br>

## Using an Array of Data and Custom Parsing
You can use the new config `arrayName` to parse through an array and then add parts from each object.

For the given json:
```
{
  messages: [
    { name: "a", id: 1, somethingElse: false },
    { name: "b", id: 2, somethingElse: false },
    { name: "c", id: 3, somethingElse: true }
  ]
}
```
you could have in your config (to show only the parts you care about and limit to 5 entries):
```
config: {
  ...
  arrayName: "messages",
  arraySize: 5,
  values: [ "name", "id" ]
}
```
