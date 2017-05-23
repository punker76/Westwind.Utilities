﻿# Westwind.Utilities Changelog

### 3.0
*not released yet*

* **Support for .NET Core 2.0**
Version 3.0 adds support for .NET Core 2.0. Most features of the toolkit have been carried forward, but some features like configuration using standard .NET Configuration files is not available in .NET Core. There are a few other features that are not available.

* **StringUtils.TokenizeString() and DetokenizeString()**  
Added a function that looks for a string pattern based on start and end characters, and replaces the text with numbered tokens. DetokenizeString() then can reinsert the tokens back into the string. Useful for parsing out parts of string for manipulation and then re-adding the values edited out.

* **StringUtils.GetLines() optional maxLines Parameter**  
Added an optional parameter to `GetLines()` to allow specifying the number of lines returned. Internally still all strings are parsed first, but the result retrieves only the max number of lines.

* **StringUtils.GenerateUniqueId() additional characters**
You can now add additional character to be included in the unique ID in addition to numbers and digits. This makes the string more resilient to avoid dupe values.

* **Add support for HMAC hashing in Encryption.ComputeHash()**
HMAC provides a standardized way to introduces salted values into hashes that results in fixed length hashes are not vulnerable to length attacks. ComputeHash now exposes HMAC versions of the standard hash algorithms.

* **Add Encryption.EncryptBytes() and Encryption.DecryptBytes()**  
Added additional overloads that allow passing byte buffer for the encryption key to make it easier to work with OS data API.

* **DataUtils.DataTableToObjectList<T>**   
You can now convert a data table to a strongly typed list with this new function.

* **XmlUtils.GetXmlEnum()/GetXmlBool() and XmlUtils.GetAttributeXmlBool()**   
Added additional conversion methods to the XML helpers to facilitate retrieving values from XML documents more easily.

> ### Breaking Changes for 3.0
> ##### .NET Core 2.0 Version
> * ConfigurationFileProvider for Configuration is not supported
> * We recommend you switch to JsonConfiguration
> * SqlDataAccess ctor requires that you pass in a **full** connection string or SqlProvider Factory. 
> * SqlDataAccess connection string names and provider names are no longer supported. (this may get fixed as additional .NET Core APIs are made available by Microsoft to support providers)
> * Encrypt.Encrypt()/Decrypt() use 24 bit keys where the old version for full framework uses 16 bit keys  
> The result is that encrypted values can't be duplicated currently with .NET Core implementation. This may get fixed in later updates of .NET Core as 16 bit TripleDES keys are possibly reintroduced.
> * Encryption DataProtection API methods don't work with .NET 2.0 since those are based on Windows APIs


### 2.70
*December 15th, 2016*

* **Fix binary encoding for extended characters in Encryption class**  
Binary encoding now uses UTF encoding to encrypt/decrypt strings in order to support extended characters.

* **Encryption adds support for returning binary string data as BinHex**  
You can now return binary values in BinHex format in addition to the default base64 encoded string values.

* **FileUtils.GetPhsysicalPath()**  
This function returns a given pathname with the proper casing for the file that exists on disk. If the file doesn't exist it

* **Fix Encoding in HttpUtils**  
Fix encoding bug that didn't properly manage UTF-8 encoding in uploaded JSON content.