<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [isValidJson][1]
    -   [Parameters][2]
-   [isValidDBON][3]
    -   [Parameters][4]
-   [newDatabase][5]
    -   [Parameters][6]
-   [Databasetify][7]
    -   [Parameters][8]
    -   [addTable][9]
        -   [Parameters][10]
    -   [insert][11]
        -   [Parameters][12]
    -   [set][13]
        -   [Parameters][14]
    -   [removeKey][15]
        -   [Parameters][16]
    -   [get][17]
        -   [Parameters][18]
    -   [find][19]
        -   [Parameters][20]
    -   [findAll][21]
        -   [Parameters][22]

## isValidJson

### Parameters

-   `string` **[string][23]** The string to check

Returns **[boolean][24]** Return wether the string is valid JSON

## isValidDBON

### Parameters

-   `obj` **[Object][25]** The Object to check

Returns **[boolean][24]** Return wether the string is valid DBON

## newDatabase

Creates a valid mode 1 database for Databasetify

### Parameters

-   `name` **[string][23]** Name you want to give to the database
-   `path` **[string][23]** Path of the JSON file for the database

## Databasetify

Main databasetify class.
Opens a file as a database,
performs operations on it adding or deleting elements
and finding for data

### Parameters

-   `path` **[string][23]** Path of the json file to databasetify.
-   `mode` **[number][26]** 0 or 1. 0 opens the file in simple mode,
                           1 opens the file in strict mode.

### addTable

Adds a table to the currently open database.

#### Parameters

-   `name` **[string][23]** Name of the table.
-   `columns` **[Array][27]&lt;column>** Array of columns.
                             Check the right structure in the documentation.

### insert

Adds a value to an existent table.

#### Parameters

-   `tableName` **[string][23]** Name of the table where you want
                                to insert values
-   `key` **[string][23]** Name of the key.
-   `value` **[Object][25]&lt;[string][23], any>** Object of values,
                                          with columns' names as keys

### set

Set a different value given the table, the key and the column names.

#### Parameters

-   `tableName` **[string][23]** Name of the table where you
                                want to insert values
-   `key` **[string][23]** Name of the key to modify
-   `column` **[string][23]** Name of the column
-   `value` **any** Value to set at given table, key and column

### removeKey

Removes the specified key in the specified table

#### Parameters

-   `tableName` **[string][23]** Name of the table where you
                                want to remove key
-   `key` **[string][23]** Key to remove

### get

Get a value from the database, given the table name, the key and the column

#### Parameters

-   `tableName` **[string][23]** Table of the value you want to get
-   `key` **[string][23]** Key of the value you want to get
-   `column` **[string][23]** Column of the value you want to get

Returns **any?** Value at specified Table, Key and Column, if it exists.
                 If not, returns null

### find

Returns the first element that makes the finder function true

#### Parameters

-   `tableName` **[string][23]** Name of the table where you want to search
-   `finder` **finder** The function to filter all the values

Returns **foundValue** Object with the value, the key, the column
                     and the counter relatives to the value

### findAll

Returns all the elements that makes the finder function true

#### Parameters

-   `tableName` **[string][23]** Name of the table where you want to search
-   `finder` **finder** The function to filter all the values

Returns **[Array][27]&lt;foundValue>** Array of Objects with the value, the key, the
                            column and the counter relatives to the value

[1]: #isvalidjson

[2]: #parameters

[3]: #isvaliddbon

[4]: #parameters-1

[5]: #newdatabase

[6]: #parameters-2

[7]: #databasetify

[8]: #parameters-3

[9]: #addtable

[10]: #parameters-4

[11]: #insert

[12]: #parameters-5

[13]: #set

[14]: #parameters-6

[15]: #removekey

[16]: #parameters-7

[17]: #get

[18]: #parameters-8

[19]: #find

[20]: #parameters-9

[21]: #findall

[22]: #parameters-10

[23]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[24]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[25]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[26]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number

[27]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array

### Database Modes

**Mode 0**

A simple, empty JSON file is valid for mode 0. Every table is a key in the JSON root and its value is an object. For each key of the table, there is a corresponding object, with as keys the columns of the tables and as values the corresponding values. It does not check for eventual errors, it just works.
```json
{
    "table1": {
        "key1": {
            "col1": "value1",
            "col2": "value2",
            "col3": "value3"
        },
        "key2": {
            "col2": "value2",
            "col4": "value3"
        }
    }
}
```
**Mode 1**

For mode 1, you need a Databasetify structured object. This is the structure:
```json
{
    "name": "databaseName",
    "tableCount": 1,
    "tables": [
        {
            "name": "tableName",
            "cols": ["col1", "col2"]
            "numOfCols": 2,
            "keys": ["key1", "key2"],
            "numOfKeys": 2,
            "values" [
                ["value1", "value2"],
                ["value1", "value2"]
            ]
            "isRelational": false,
            "relations": [
                null,
                null
            ]
        }
    ]
}
```
It may seem very complex, but you can create an empty mode 1 database writing: 
```json
{
    "name": "databaseName",
    "tableCount: 0,
    "tables": []
}
```
Or simply using the function newDatabase (for this, you can use the Node console)
```javascript
const databasetify = require("databasetify");
databasetify.newDatabase("name", "path/to/db.json");
```
This mode checks for eventual structure errors.