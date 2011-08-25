---
layout: page
title: Creating a Tails Script
permalink: tails/scripting.html
comments: true
---

A Tails Script is basically a very simple JavaScript file ending with the *tails.js* extension.  To get started, you can build from the [sample Tails script here](http://codeeg.com/tails/scripts/sample.tails.js).

Like a Greasemonkey user script, a Tails Script has a metadata section describing how to install the plugin.  The metadata section starts with the *// ==TailsScript==* comment and ends with the *// ==/TailsScript==* comment.  Metadata values are defined the comment format:

{% codeblock lang:javascript %}
// @name value
{% endcodeblock %}

The supported metadata values are:

- __name__ - The name of the script.  This will be the text of the link if a URL is rendered.
- __namespace__ - The namespace of the script.
- __description__ - A description of the script.  This will be displayed in the script management window.
- __include__ - The microformats that this script can operate on.  Add multiple include lines for each microformat you support.

When a Tails Script is executed, the contents of the script is loaded within a JavaScript *Hash* object, so functions and variables must be defined with the *name: (variable | function)* syntax and separated by commas.

The only method that Tails requires in the script is the __getURL__ function.  This function does not have any parameters and should return the URL of the link to render in the Tails view.  Not returning anything or returning *null* will result in the the link not rendering in the view.  The method can access the current microformat object by accessing the __object__ instance variable:

{% codeblock lang:javascript %}
getURL: function() { if (this.object.__name == 'hcard'){ /* generate URL... */ } }
{% endcodeblock %}

In addition to __getURL()__, you can also specify the following function to further customize the behavior of your script:

- __getLabel()__ - Returns the label for the generated link.  If this method is not defined, the script name will be used instead.

The following instance variables are available to the script in addition to __object__:

- __sourceURL__ - The URL of the web page containing the current microformat.
- __label__ - The name of the script.

Data Object Members
-------------------

The parsed microformat objects always contain the following member:

- ____name__ - The name of the microformat (hcard, hcalendar, etc.)

The following section lists the members variables/functions that might be available for that particular microformat.  Although the specs might specify that some values are required, Tails is pretty forgiving and will more than likely create an object for it anyway.  Just to be safe you should make sure that value is available before accessing it.

For the one-worded object members, you can access them with the standard *object.name* syntax (example: *object.fn*); However, since multi-word names are usually separated by a dash (-), you'll need to use the *object["name"]* syntax instead (example: *object["family-name"]*).

hAtom
-----

- __Basic member variables__ -  entry-title, entry-content, entry-summary, bookmark
- __JavaScript Date values__ - updated_date, published_date
- __author_hcard__ - Post author as an hCard object (see __hCard__ spec below).
- __getTagString()__ - Returns a comma seperated list of tag names.

hCalendar
---------

- __Basic member variables__ - dtstart, dtend, summary, location, comment, description, contact, sequence, priority, dtstamp, last-modified, created, recurrence-id, attendee, organizer, url
- __JavaScript Date values__ - dtstart_date, dtend_date
- __location_hcard__ - The location as an hCard object (see __hCard__ spec below).

hCard
-----

- __Basic member variables__ - n, fn, given-name, family-name, title, note, org, locality, region, street-address, postal-code, country-name, email, logo, photo, url
- __tel__ - An array of telephone numbers (or *undefined* if none were specified).  Each object in the array will at least a __value__ member, and maybe a __type__ member if specified.
- __toAddressString()__ - Method returning a prettied up version the address (street-address, locality, region, postal-code, country.
- __toStreetAddressLocalityRegionAndPostalCodeString()__ - Method returning a prettied up string containing street-address, locality, region, postal-code values.
- __toLocalityAndRegionString()__ - Method returning a prettied up string containing locality, region values.
- __toLocalityRegionAndPostalCodeString()__ - Method returning a prettied up string containing locality, region, postal-code values.
- __toLocalityRegionAndCountryString()__ - Method returning a prettied up string containing locality, region, country values.
- __toLocalityRegionPostalCodeAndCountryString()__ - Method returning a prettied up string containing locality, region, postal-code, country values.

hResume
-------

- __Basic member variable__ - summary
- __contact_hcard__ - hCard of the person described in the resume.
- __education__ - An array or hCalendar events.
- __experience__ - An array or hCalendar events.
- __skill __- An array of skills (String objects).
- __affiliation__ - An array of hCards.
- __publications__ - An array of publications (String objects).

hReview
-------

- __Basic member variables__ - rating, description, summary, type, version, dtreviewed, url
- __JavaScript Date values__ - dtreviewed_date
- __item__ - *item_hcard* variable will be available if an hCard is present and *item_hcalendar* variable for hCalendar.  Otherwise, *item.fn*, *item.photo*, or *item.url* if available.  Finally, if none of those values are present, *item* will be a string of the node's contents.
- __reviewer__ - hCard object of the reviewer

xFolk
-----

- __Basic member variable __- description
- __taggedlink__ - Object representing the bookmarked link, containing object members *name* and *url*.
- __tags__ - An array of tags.  Each tag object will have object members* name* and *url*.

geo
---

- __Basic member variables __- lattitude, longitude, lattitude_label, longitude_label, label.

