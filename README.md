# Google Drive File Link Management

A Google Drive application to manage file download and export links.
Export options are supported for Google office suite documents.

```Note: native Google office suite documents hereinafter referred to as the NGD.```

## The Problem

When you share a link to a file located on Google Drive your vis-a-vis 
may face:
 * need to switch to a Google account in order to access NGD
 * inability to access NGD when vis-a-vis has got no Google account
 * take extra step to download other types of files as by default those
   are opened in a preview mode
 * inability to access any file if access permissions aren't
   set properly

You may also want to track access activities.

## Contents
 * [Solution](#solution)
 * [Features explained](#features)
 * [Installation](#installation)
 * [Credits](#credits)
 * [Copyright](#copyright)
 * [Resources](#resources)

## Solution

 * Convert NGD into Microsoft Office or other 
   types on the fly.
 * Provide vis-a-vis with a direct download link.
 * Grant download access in a single click.

### Features
 * Convert and download link for NGD
 * NGD gets converted to MSO document, pdf, or other types
 * Google Sheets pdf export can be tuned
 * Direct download link for other types
 * goo.gl url shortener embedded
 * access authorization shortcut
 
### NGD export support

| NGD file type       | MSO         | OpenDoc | html  | rtf / epub | pdf   | txt | csv / tsv | jpg / png / svg |
|---------------------|:-----------:|:-------:|:-----:|:----------:|:-----:|:---:|:---------:|:---------------:|
| Docs                | docx        | odt     | `(1)` | +          | +     | +   | -         | -               |
| Sheets              | xlsx        | ods     | `(1)` | -          | `(2)` | -   | `(3)`     | -               |
| Slides              | ppsx / pptx | odp     | -     | -          | +     | +   | -         | `(4)`           |
| Drawings            | -           | -       | -     | -          | +     | -   | -         | +               |
| Forms `(5)`         | -           | -       | -     | -          | -     | -   | -         | -               |
| Fusion Tables `(6)` | -           | -       | -     | -          | -     | -   | -         | -               |
 
Notes:
 * `(1)` - zipped web-page with media assets if any 
 * `(2)` - customized pdf output available
 * `(3)` - available on per sheet basis and therefore
   from Sheets open context; 
   see [Google Sheets](#google-sheets) 
   section below for details
 * `(4)` - available on per slide basis and therefore
    from Slides open context; 
    see [Google Slides](#google-slides) 
    section below for details
 * `(5)` - Google Forms download or export 
   makes no sense, therefore only open link shortening offered
 * `(6)` - Google Fusion Tables is an experimental
   application and not supported yet
 
### Security

This app is based on the drive.file OAuth2 scope, 
where permission is granted only for individual files 
that the user authorizes.

[[back to contents]](#contents)

## Features explained

### Links

#### Long URLs
 
 * `open` - equivalent to shareable link available from
   Google Drive context menu. NGD are get opened with
   native google applications. Other files are get opened with
   Drive preview or associated application if any.
 * `download` - direct file download link. NGD can
   be exported in either of
   [supported formats](#ngd-export-support), so user is presented
   with a list of links.

#### goo.gl shortened links

When Google authorized user requests a short url via
google URL shortener a new goo.gl id
is being generated every time, which makes stats collection
near senseless. This app generates goo.gl id for each type
of targeted long URL only once and stores those in file
description as a JSON document.

**NB!** The JSON preceded with `LINKMAN=` string is appended to the
end of file description. However user can accidentally remove 
or corrupt the JSON, in which case new goo.gl ids will be generated.

File description gets updated only upon Save action 
or upon first access to a file.

Types of short URLs stored:
 * `open` : preview|NGD open
 * `DL`   : download for non-NGD files

For NGD documents exporting urls are stored.
MSO and pdf export urls are generated by default. Other types
require manual activation.

#### NGD specifics

##### Google Sheets

Google Sheets pdf export can be customized.

Available settings are:
 * `size = letter|A4|A3...`
 * `portrait = true|false`
 * `fitw = true|false`
 * `source = custom string`
 * `sheetnames = true|false`
 * `printtitle = true|false` // optional headers and footers
 * `pagenumbers = true|false`
 * `gridlines = true|false`
 * `fzr = true|false`        // frozen rows on each page
 * `gid = sheet_Id`          // not , see remark below

**NB!** Per sheet exports (employing `gid` sheet id)
available only from Sheets open context.
Please, use [ExportLink](#exportlink-script) 
Google Script.

Short url for each set of export settings can be stored in the
LINKMAN JSON.

```
pdf : [
        { settings : export settings,
          shortUrl : shortened url for given settings
        },
        ...
    ]
```

##### Google Slides

Export to images is supported on per slide basis and therefore
is available only from Slides open context.
Please, use [ExportLink](#exportlink-script) 
Google Script.

##### Google Forms

Exporting Google Forms makes no sense. Therefore only `open`
link gets shortened.

##### Google Fusion Tables

Google Fusion Tables is an experimental application
and not supported yet. It is most likely exporting those
will not make much sense and therefore only `open`
link shortening will be available.

If you feel it's time to start supporting Google Fusion Tables
drop the [author](#copyright) a note on that.

### Access authorization shortcut

While this feature allows to grant
"`Anyone with the link can view (download) the file`"
powers it is recommended to grant access on per folder basis.

In either case consider possible negative consequences
when granting any level of access.

[[back to contents]](#contents)

## Installation

### Chrome web-store

Install the application from [Chrome web-store](https://google.com/).

### Customize the app

Clone and customize the script. The resulted app should have been
hosted somewhere.

Options for hosting include Google App Engine,
where a simple Python configuration provides an easy-to-use 
way to expose only static content
(in this case, serving the JavaScript and html). 
Other alternatives include using a Google Drive 
public folder to host the files, or your own web server.

In all cases, a configuration will need to be created in the
Google Developers Console, as outlined
[here](https://developers.google.com/drive/web/enable-sdk).

Note: The resulting App ID, Client ID, and API Key 
generated as part of that process will need to be put 
into the your app's configuration (in actual code).
For ZIP Extractor, that configuration information in found
in `config.js` under the `/js/linkman/` directory.

[[back to contents]](#contents)

## Credits

These projects were used as a source of inspiration 
and Google Drive Apps building practices:
 * [ZIP Extractor](https://github.com/googledrive/zipextractor)
 * [web-quickeditor](https://github.com/googledrive/web-quickeditor)

[[back to contents]](#contents)

## Copyright

© [Oleksiy Rudenko](https://github.com/OleksiyRudenko), 2017

[[back to contents]](#contents)

## Resources
* [Drive API](https://developers.google.com/drive/v3/web/install)
* [Drive App Examples](https://developers.google.com/drive/v3/web/examples/)
* [ngclipboard](https://sachinchoolur.github.io/ngclipboard/)


### Alternatives

[Direct Link Creator app](http://directlink.booogle.net/)

### Notes

For native google documents {exportIds} sent to an app
instead of {ids}.
[Details](https://developers.google.com/drive/v3/web/integrate-open)

[File Meta-data](https://developers.google.com/drive/v2/web/file)

[File Properties](https://developers.google.com/drive/v2/web/properties)

[Web Store Listing](https://developers.google.com/drive/v2/web/listing)

[Publishing](https://developers.google.com/apps-marketplace/listing)
& [Integrate with button](https://developers.google.com/apps-marketplace/button)

[MIME-types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types)

[Web-app checklist](https://developers.google.com/web/progressive-web-apps/checklist)

### App publishing notes
 * add API
 * add and use credentials
 * check app permissions before production
 * verify your ownership of domain your app resides at

### ExportLink script
[ExportLink](https://google.com/?q=ExportLink+google+script)
is a script that also is able of generating links for
individual sheets and slides.

[[back to contents]](#contents)
