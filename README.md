mcurl - Memento wrapper for cURL
================================

Download
-------------------------

Most updated version: [Download](http://search.cpan.org/dist/HTML-Parser/ Download)

Environment setup
-------------------------

* curl 7.15.5 or later
* perl 5 or later
* HTML::Parser package download

Examples
-------------------------

In this section, I will add the switch examples that may describe the code behavior.

Calling an original resource with the default timegate

        mcurl.pl -I -L --debug --datetime 'Sun, 23 July 2006 12:00:00 GMT' http://www.cnn.com 
        Expected results: it will do the content negotiation in the datetime dimension, it uses the default timegate when required 
        Response code: 302 -> 200 


Calling timemap in link format with the default timegate

        mcurl.pl -I -L --debug --timemap link http://www.cnn.com 
        Expected results: it will download the timemap on application-link format, it uses the default timegate 
        Response code: 200 

Calling an original resource with a specific timegate

        mcurl.pl -I -L --debug --timegate 'http://mementoproxy.lanl.gov/aggr/timegate/' http://www.cnn.com 
        Expected results: it will do the content negotiation in the datetime dimension and get the last memento, it uses the specified timegate when required 
        Response code: 302 -> 200 

Calling an original resource with a specific timegate

        mcurl.pl -I -L --debug --datetime 'Sun, 23 July 2006 12:00:00 GMT' --timegate 'http://mementoproxy.lanl.gov/aggr/timegate/' http://www.cnn.com 
        Expected results: it will do the content negotiation in the datetime dimension, it uses the specified timegate when required 
        Response code: 302 -> 200 
        
Calling timemap in link format with the specific timegate

        mcurl.pl -I -L --debug --timemap link --timegate 'http://mementoproxy.lanl.gov/aggr/timegate/' http://www.cnn.com 
        Expected results: it will download the timemap on application-link format, it uses the specified timegate when required 
        Response code: 200 

Calling an original resource that has a specific timegate

        mcurl.pl -I -L --debug --datetime "Thu, 23 July 2009 12:00:00 GMT" http://lanlsource.lanl.gov/hello 
        Expected results: it will do the content negotiation in the datetime dimension, the site will provide a timegate which will override the default timegate 
        Response code: 302 -> 200 

Calling an original resource (R1) that has a redirection (R2), (R1) has valid mementos

        mcurl.pl -I -L --debug --datetime "Thu, 23 July 2009 12:00:00 GMT" http://www.zeit.de/ 
        Expected results: it will do the content negotiation in the datetime dimension, R1 has valid mementos; so the result will be for R1 only. 
        Response code: 302 -> 200 

Calling an original resource (R1) that has a redirection (R2), (R1) does NOT have valid mementos

        mcurl.pl -I -L --debug --datetime "Thu, 23 July 2009 12:00:00 GMT" http://lanlsource.lanl.gov 
        Expected results: it will do the content negotiation in the datetime dimension, R1 doesn't have valid mementos; so the result will be for R2 only. 
        Response code: 302 -> 200 

Calling an original resource that has a timegate redirection

        mcurl.pl -I -L --debug --datetime "Mon, 23 July 2007 12:00:00 GMT" http://lanlsource.lanl.gov/hello 
        Expected results: it will do the content negotiation in the datetime dimension, the site will provide a timegate which will override the default timegate. The timegate /tg/ has a redirection to /ta/ 

Calling an original resource that has a timegate redirection

        mcurl.pl -I -L --debug --datetime "Sat, 23 July 2011 12:00:00 GMT" http://lanlsource.lanl.gov/hello 
        Expected results: it will do the content negotiation in the datetime dimension, the site will provide a timegate which will override the default timegate. The timegate /tg/ has a redirection to /ts/ 

Calling an original resource with Acceptable time period

        mcurl.pl -I -L --debug --datetime Thu, 23 July 2009 12:00:00 GMT; -P5MT5H;+P5MT6H' http://www.cs.odu.edu 
        Expected results: it will do the content negotiation in the datetime dimension with specified time period which has valid mementos, it uses the default timegate when required 
        Response code: 302 -> 200 

Calling an original resource with NOT Acceptable time period

        mcurl.pl -I -L --debug --datetime 'Thu, 23 July 2009 12:00:00 GMT; -P5MT5H;+P5MT6H' http://www.cs.odu.edu 
        Expected results: it will do the content negotiation in the datetime dimension with specified time period which does not have any valid mementos, it uses the default timegate when required 
        Response code: 406 

Calling an original resource with invalid Accept-datetime header

        mcurl.pl -I --debug --datetime 'Sun, 23 July xxxxxxxxxxxxxxxx' http://www.cnn.com 
        Response code: 400 

Override the discovered timegate with the specific one

        mcurl.pl -I -L --debug --datetime "Sat, 23 July 2011 12:00:00 GMT" --timegate 'http://mementoproxy.cs.odu.edu/aggr/timegate' --override http://lanlsource.lanl.gov/hello 

using the --replacedump switch to dump the replacement for the embedded resources to an external file for further analysis

        mcurl.pl -L --mode strict --datetime "Sat, 03 Dec 2010 12:00:00 GMT" --replacedump cnnreplace.txt http://www.cnn.com 

accessing the dbpedia archive

        mcurl.pl -L --mode strict --datetime "Sat, 03 Dec 2010 12:00:00 GMT" http://dbpedia.org/page/Brisbane
