# UpdateCatalogParseLib

This library was made to help me or anyone else using it collect data from https://www.catalog.update.microsoft.com/ in
comfortable and usable way.

``` java
<dependency>
  <groupId>com.microsoft.cataloge</groupId>
  <artifactId>mscatalog-parser</artifactId>
  <version>1.1.1</version>
</dependency>
```

## Credits

Big thanks to ryan-jan (https://github.com/ryan-jan) and his MSCatalog poweshell module. At first I was trying to
re-write this module as C# class library.)

## How to use it

Right now there is only two functions available.

``` java
SendSearchQuery(HttpClient client, string Query)
```

This method will return you collection of CatalogResultRow objects. Each of this objects represent search result from
catalog.update.microsoft.com with data available through
search results page only:

1. Update's ID
2. Title
3. Products
4. Classification
5. Last Updated date
6. Version
7. Size
8. Size in bytes

If `ignoreDublicates` parameter is TRUE than function will return only updates with unique `Title` and `SizeInBytes`
fields.

``` java
GetUpdateDetails(HttpClient client, string UpdateID)
```

If you need to get more information about some update you've found from previous method - you need to use this function
and pass it's `UpdateID` parameter to it.
It will return you object derived from `UpdateBase` class (ether `Update` or `Driver` classes) with all information
available about it from details page or download page.
Like list of HardwareIDs if it is a driver or Supersedes if it is an Update.

## Limitations

What this library does - is basicly parses HTML pages from catalog.update.microsoft.com, so it's derives it's
limitations directry from it.

* It cannot return more than 1000 search results at once.
* It's speed depends on how fast your connection with catalog is. On my testing environment (1Gb/s internet connection)
  SendSearchQuery method running about 40 seconds.
