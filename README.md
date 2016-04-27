# [gulp](http://gulpjs.com)-advanced-csv-to-json

>Converts CSV to Json object in various output. You can either do basic conversion or you can use its awesome feature
 to use your own json structure.
> This is very helpful if you have complex json structure that a basic csv to json converter cannot do.

Install :traffic_light:
-------

```bash
$ npm install gulp-advanced-csv-to-json --save
```

## Pipe :neckbeard:

Like any other gulp plugin, get source file then process all. Output file can be configured in the source file.

In your gulpfile.js

**`/gulpfile.js`**


```javascript
var gulp = require('gulp');
var aCsvToJson = require('gulp-advanced-csv-to-json');

gulp.task('bulkCsvToJsonConversion', function(){
        gulp.src('path/to/your/**/*.conf')
            .pipe(aCsvToJson({
                 tabSize : 4
             }))
```

## Config File :page_facing_up:


**`/path/to/*.conf`**


```
[
    {
        "filePath" : "csv/002.csv"
    },
    {
        "filePath" : "csv/001.csv",
        "outputPath" : "output/001.json",
        "contract" : {
            "name" : "name",
            "profile" : {
                "age" : "Double:profile/age"
            },
            "address" : {
                "permanent" : {
                    "city" : "address/permanent/city",
                    "state" : "address/permanent/state"
                },
                "current" : "address/current"
            },
            "tags" : "Array:tags"
        }
    }
]
```

## CSV File :page_facing_up:

**`/path/to/*.csv`**

```

name, address/permanent/city, address/permanent/state, address/current, school_0, year_0, school_1, year_1,tags
Juan Dela Cruz, Quezon city, Metro Manila, Makati city,DPS,1997,PSU,2001,a|b|c
John Doe, Puerto Princesa city, Metro Manila, Palawan, Oxford,1993, Harvard,2003,t1|t2|t3

```

## How it Works :wrench:

Advanced Csv to Json will fetch the config file and process all items. It will read the CSV file that you declared and
check if there's a desired contract that you want to use. If there's none, it will just convert the csv to a flat JSON
object. If there is, it will use the structure and match all values of the JSON to the CSV.

Notice that you can declare the value to be an Array or Double (default is String).

```
{
    key : [dataType]:[csvValue]
}

```

If you look at the json and csv closer

**`json`**
```"tags" : "Array:tags"```
**`csv`**
a|b|c

you may notice that the convention for Array:tags is pipe delimited values.
