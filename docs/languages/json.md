---
Order: 4
Area: languages
TOCTitle: JSON
PageTitle: JSON editing in Visual Studio Code
DateApproved: 3/7/2016
MetaDescription: Edit JSON files in Visual Studio Code
---

# JSON

JSON is a data format that is common in configuration files like `package.json` or `project.json`. We also use it extensively in VS Code for our configuration files.  When opening a file that ends with `.json`, VS Code provides the following set of features that make it simpler to write or modify the file's content.

## JSON Comments

Comments in JSON are an extension to JSON specification that is supported by VS Code. You can use single line (//) as well as block comments (/* */) as used in JavaScript.

## IntelliSense & Validation

For properties and values (`kb(editor.action.triggerSuggest)`), both for JSON data with and without schema, we offer up suggestions as you type with IntelliSense.   We also perform structural and value verification based on an associated JSON schema giving you red squigglies.

![IntelliSense](images/json/intellisense.png)

### Package and Project Dependencies

We also offer IntelliSense for specific value sets such as package and project dependencies in `package.json`, `project.json`, `bower.json`, ...

## Quick Navigation

JSON files can get pretty large and we support quick navigation to properties `kb(workbench.action.gotoSymbol)` (sometimes referred to as goto symbol) with the Command Palette.

![Goto Symbol](images/json/gotosymbol.png)

## Hovers & Toggle Value

When you hover over properties and values for JSON data with or without schema, we will provide additional context.

![Hover and Toggle](images/json/hoverandtoggle.png)

We also support toggling for allowed values by pressing `kb(editor.action.inPlaceReplace.down)` or `kb(editor.action.inPlaceReplace.up)` on a value.  In the image above, this would switch between `true` and `false`.

## Formatting

You can format your JSON document (or just a part of it) using `kb(editor.action.format)` or **Format** from the context menu.

## JSON Schemas & Settings

To understand the structure of JSON files, we use [JSON schemas](http://spacetelescope.github.io/understanding-json-schema/). JSON schemas describe the shape of the JSON file, as well as value sets, default values, and descriptions.

Servers like http://schemastore.org provide schemas for most of the common JSON based configuration files. However, schemas can also be defined in a file in the VS Code workspace, as well as the VS Code settings files.

The association of a JSON file to a schema can be done either in the JSON file itself using the `$scheme` attribute, or in the User or Workspace Settings (**File** > **Preferences** > **User Settings** or **Workspace Settings**) under the property `json.schemas`.

>**Tip:** For an overview on settings, see [User and Workspace Settings](/docs/customization/userandworkspace.md).

### Mapping in the JSON

In the following example, the JSON file specifies that its contents follow the CoffeeLint schema.

```json
{
   "$schema": "http://json.schemastore.org/coffeelint",
   "line_endings": "unix"
}
```

### Mapping in the User Settings

The following excerpt from the User Settings shows how `bower.json` files are mapped to the bower JSON schema located on http://json.schemastore.org/bower.

```json
"json.schemas": [
    {
        "fileMatch": [
            "/bower.json",
            "/.bower.json"
        ],
        "url": "http://json.schemastore.org/bower"
    },
```

### Mapping to a Schema in the Workspace

To map a schema that is located in the workspace, use a relative path. In this example, a file in the workspace root called `myschema.json` will be used as the schema for all files ending with `.foo.json`.

```json
"json.schemas": [
    {
        "fileMatch": [
            "/*.foo.json"
        ],
        "url": "./myschema.json"
    },
```

### Mapping to a Schema in the Settings Files

To map a schema that is defined in the User or Workspace Settings, use the `schema` property. In this example, a schema is defined that will be used for all files named `.myconfig`.

```json
"json.schemas": [
    {
        "fileMatch": [
            "/.myconfig"
        ],
        "schema": {
            "type": "object",
            "properties": {
                "name" : {
                    "type": "string",
                    "description": "The name of the entry"
                }
            }
        }
    },
```


### Mapping a Schema in an Extension

Schemas and schema associations can also be defined by an extension. Check out the [jsonValidation contribution point](/docs/extensionAPI/extension-points.md#contributesjsonvalidation).

## Next Steps

Read on to find out about:

* [Customization](/docs/customization/overview.md) - Customize VS Code to work the way you want
