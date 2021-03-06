# Streeng 1.5.3

Perform common operations on strings such as change case, truncate, find/replace, repeat, encode/decode, generate slugs and more.

## Quick Tag Reference (full documentation below)

	allowed="p|span|a" - pass "none" to strip all tags or a pipe (|) delimited list of allowed tags (default = allow all)
	find="string1" - string to find (separate multiple values with the explode variable which defaults to "|", accepts regex)
	replace="string2" - string to replace found string (default = "")
	insensitive="yes" - toggle case sensitivity when finding a string (default = "no")
	explode="|" - string to split find/replace parameters with
	trim="left" - left, right, or both (default = "both")
	encode="yes" - HTML encode the string (default = "no")
	decode="yes" - HTML decode the string (default = "no")
	url="yes" - URL encode the string (default = "no")
	capitalize="yes" - capitalize the first character of the string (default = "no")
	title="yes" - capitalize the first character of every word (default = "no")
	lower="yes" - convert the string to lower case (default = "no")
	upper="yes" - convert the string to upper case (default = "no")
	characters="10" - number of characters to truncate the string to (default = unlimited)
	words="10" - number of words to truncate the string to (default = unlimited)
	append="..." - if truncated append this to the end of the string (default = "&hellip;")
	slug="yes" - convert the string to a slug (default = "no")
	separator="_" - separator for slug (default = "-")
	repeat="3" - number of times to repeat the string, great for prototyping (default = 0)
	count="|" - return number of substring instances of a supplied string (default = false)
	splits="|" - return number of exploded values from a supplied string (default = false)

***

## Parameters

And here is more detailed information on the parameters available for the {exp:streeng} tag pair.

### Stripping HTML Tags

	allowed="none"

or

	allowed="p|span|a"

This will strip either all (if set to allowed="none") or the desired HTML tags from the string enclosed by the tag pair. If this parameter is not set, the default is to allow all.

Example:

	{exp:streeng allowed="none"}
		<p>Our plans for <a href="http://youtu.be/GBkT19uH2RQ">world domination</a> are none of your concern. So go mind your own business!</p>
	{/exp:streeng}

Result:

	Our plans for world domination are none of your concern. So go mind your own business!

Example:

	{exp:streeng allowed="a"}
		<p>Our plans for <a href="http://youtu.be/GBkT19uH2RQ">world domination</a> are none of your concern. So go mind your own business!</p>
	{/exp:streeng}

Result:

	Our plans for <a href="http://youtu.be/GBkT19uH2RQ">world domination</a> are none of your concern. So go mind your own business!

### Find and Replace

	find="string1|string2"
	replace="string3"
	insensitive="yes"
	explode="|" — default: |

find="" accepts a pipe delimited list of strings to find and replace with the contents of replace="". Allows you to find all instances of a string and replace it with your desired text, or you can set replace="" to simply remove the matching string.

Optionally specify case sensitivity. Default is not case sensitive.

Optionally specify the explode parameter. Default is pipe.

You can also use regex in your find="" parameter.

Example:

	{exp:streeng find="well under way" replace="none of your concern"}
		Our plans for world domination are well under way.
	{/exp:streeng}

Result:

	Our plans for world domination are none of your concern.

Example:

	{exp:streeng find="http:\/\/(.*).com" replace="http://caddis.co"}
		http://caddisint.com
	{/exp:streeng}

Result:

	http://caddis.co

#### Special Characters in Find and Replace

Streng also provides some keywords to search for special characters.

find="NEWLINE" — Finds a new line.  
find="PIPE" — Find the | character.  
find="QUOTE" — Find a prime quote: ".  
find="SPACE" — Find a space character.  

### Trim

	trim="left"

Specify the trimming of white space with this parameter. Default = "both"

### Encoding

	encode="yes"
	decode="yes"
	url="yes"

HTML encode or decode, or URL encode a string.

#### HTML Encode

With encode="yes", a prime quotation mark would be encoded as &amp;quot; and ampersands encoded as &amp;amp;

Example:

	{exp:streeng encode="yes"}
		"I'm a test" string & boy don't I look cool? Looking cool really helps with world domination!
	{/exp:streeng}

Result:

	&quot;I'm a test&quot; string &amp; boy don't I look cool? Looking cool really helps with world domination!

This is really useful for protecting code examples and the like.

Example:

	{exp:streeng encode="yes"}
		Streeng will encode prime quotation marks as &quot; entities.
	{/exp:streeng}

Result:

	Streeng will encode prime quotation marks as &amp;quot; entities.

Or you can reverse the process with decode="yes".

Example:

	{exp:streeng decode="yes"}
		String will encode prime quotation marks as &quot; entities.
	{/exp:streeng}

Result:

	String will encode prime quotation marks as " entities.

#### URL Encode

If you need to url encode a string, use url="yes". Say you need to encode segments for use in a querystring. Like /account/login?return="my/url/segments". Of course those slashes in the querystring would need to be encoded.

Example:

	{exp:streeng url="yes"}
		my/url/segments
	{/exp:streeng}

Result:

	my%2Furl%2Fsegments

### Sentence Manipulations

**capitalize="yes"** — capitalize the first character of the string  
**title="yes"** — capitalize the first character of every word  
**lower="yes"** — convert the string to lower case  
**upper="yes"** – convert the string to upper case

### Limiting and Truncating

All limiting and truncating will only count characters and words that are not HTML tags, and HTML tags will be auto-closed for you. In addition, character truncating is word aware and will not cut off words in the middle. Instead, Streeng will truncating immediately preceding the word that would otherwise be truncated.

Here are the parameters:

**characters="20"** — truncate the string by character count  
**words="10"** — truncate the string by word count  
**append="&hellip"** — if truncated this will be appended to the end of the string.

### Slug

This function will replace spaces in your string with dashes (default) or whatever you specify.

**slug="yes"** — Replace spaces in the string with dashes, or your specified separator  
**separator="_"** — Optionally specify the separator to use in the slug

### Repeat

**repeat="3"** — Specify the number of times to repeat the string between the tag pair. This is in addition to the initial content. So if you specify the number two, you will see your string three times.

### Counts and Splits

**count="|"** — return the number of instances the supplied string appears.  
**splits="|"** — return the number of exploded values from the supplied string.

## License

Copyright 2014 Caddis Interactive, LLC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

	http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.