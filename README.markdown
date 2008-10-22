# Mini-Mallows: A Multi-Part Form Wrapper for Cocoa & iPhone

All I wanted was some simple code to POST an image to a web service from my iPhone project.  No big deal, right?  Apparently, not.

Based on my google search results many people we were wanting the same thing and just not finding it.  There are a couple iphone
development sites giving examples and some really old open-source projects but nothing really felt right to me.  So being a good
developer I hacked something together which works for me and posted it on GitHub.

Issuing standard GETs and POSTs with Cocoa is pretty easy, but I couldn't find anything _easy_ to make multi-part forms for
POSTing.  This is where mini-mallows comes in.  Just make some Cocoa, add some mini-mallows (form fields & a file), and POST.

Easy.

## Current status

This project was written to satisfy my need to POST a single image and related form fields from an iPhone app to a web service.
It only allows for the addition of one file per request.  I am very open to comments, patches, and ridicule.

## Installation

Copy the files `MultipartForm.h` and `MultipartForm.m` anywhere you like into your Xcode project.

## Usage

First, add your standard `#import`.

    #import "MultipartForm.h"

Create a NSURL object as you'll need to send that to Mini-Mallows.

    NSURL *postUrl = [NSURL URLWithString:@"http://www.domain.com"];
    
Now create a `MultipartForm` object and a few form fields and a file.  I really wanted to call the class `MiniMallows` but
`MultipartForm` is easier on the eyes.

    MultipartForm *form = [[MultipartForm alloc] initWithURL:postUrl];
    [form addFormField:@"formFieldName1" withStringData:@"This is some data"];
    [form addFormField:@"formFieldName2" withStringData:@"This is more data"];
    [form addFile:@"path/to/file" withFieldName:@"formFieldForFile"];
    
When you are done adding fields and the file you can get a fully formed `NSMutableURLRequest` object from Mini-Mallows.

    NSMutableURLRequest *postRequest = [form mpfRequest];

All set so POST the form.

    NSData *urlData;
    NSURLResponse *response;
    NSError *error;

    urlData = [NSURLConnection sendSynchronousRequest:postRequest returningResponse:&response error:&error];

## Author

Samuel Schroeder 

* samuelschroeder@gmail.com
* [http://samuelschroeder.com](http://samuelschroeder.com)
* Managing Consultant <:> Proton Microsystems, LLC <:> iPhone/Rails Development
* twitter - [@SamSchroeder](http://twitter.com/SamSchroeder)

## License

Copyright (c) 2008 Samuel Schroeder / Proton Microsystems, LLC

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.