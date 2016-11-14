---
title:  "Printing Alamofire.Request debugDescription on a breakpoint"
description: How to get a well-formatted cURL command representing the Request that can be run directly in Terminal.
## date: 2016-11-14
---


💡 Little tip for debugging network requests: you can get a `cURL` statement for the request and execute that in the _Terminal_. (you probably knew this already)

However, you might've noticed that when you simply set a breakpoint on the line after creating the request, and then from the Xcode console `print request.debugDescription` you cannot execute the cURL command—it has way to many backslashes in them. 😑

The solution, thanks to [a helpful tip from jshier][jshier], is to run the same command as an _expression_ (e). Now, we _do_ get a cURL statement that is ready to be copy-pasted into Terminal!

``` bash
✅(lldb) e print(request.debugDescription)
$ curl -i \
    -X POST \
    -H "User-Agent: Test/nl.reapply (1.0; iOS 10.1.0)" \
    -H "Accept-Encoding: gzip;q=1.0, compress;q=0.5" \
    -H "Authorization: Basic base64OleOleOleeeeOleeOlee" \
    -H "Accept-Language: en-US;q=1.0" \
    -H "Content-Type: application/json" \
    -d "{\"operation\":\"read\","type\":\"double_rainbow\"}" \
    "https://reapply.nl/test"
```

***

## No need to read on…

For the sake of completeness, and for those of you who are googling for this problem, this is what would have happened instead.

Say, we have a breakpoint at:

``` swift
request.validate().responseJSON { response in
…
```
Then from console, we would try to extract a cURL command:

``` bash
🚫(lldb) print request.debugDescription
(String) $R1 = "$ curl -i \\\n\t-X POST \\\n\t-H \"User-Agent: Test/nl.reapply (1.0; iOS 10.1.0)\" \\\n\t-H \"Accept-Encoding: gzip;q=1.0, compress;q=0.5\" \\\n\t-H \"Authorization: Basic base64OleOleOleeeeOleeOlee\" \\\n\t-H \"Accept-Language: en-US;q=1.0\" \\\n\t-H \"Content-Type: application/json\" \\\n\t-d \"{\\\"operation\\\":\\\"read\\\",,\\\"type\\\":\\\"double_rainbow\\\"}\" \\\n\t\"https://reapply.nl/test\""
```
Holy sh—t escaping galore!

Still, assuming the escaping is correct, we should be able to copy-paste that into Terminal and see what the request returns: 

``` bash
$ curl -i \\\n\t-X POST \\\n\t-H \"User-Agent: Test/nl.reapply (1.0; iOS 10.1.0)\" \\\n\t-H \"Accept-Encoding: gzip;q=1.0, compress;q=0.5\" \\\n\t-H \"Authorization: Basic base64OleOleOleeeeOleeOlee\" \\\n\t-H \"Accept-Language: en-US;q=1.0\" \\\n\t-H \"Content-Type: application/json\" \\\n\t-d \"{\\\"operation\\\":\\\"read\\\",,\\\"type\\\":\\\"double_rainbow\\\"}\" \\\n\t\"https://reapply.nl/test\"
-bash: syntax error near unexpected token `('
```
Apparently not …and after escaping those brackets, still no luck:

``` bash
$ curl -i \\\n\t-X POST \\\n\t-H \"User-Agent: Test/nl.reapply \(1.0; iOS 10.1.0\)\" \\\n\t-H \"Accept-Encoding: gzip;q=1.0, compress;q=0.5\" \\\n\t-H \"Authorization: Basic base64OleOleOleeeeOleeOlee\" \\\n\t-H \"Accept-Language: en-US;q=1.0\" \\\n\t-H \"Content-Type: application/json\" \\\n\t-d \"{\\\"operation\\\":\\\"read\\\",,\\\"type\\\":\\\"double_rainbow\\\"}\" \\\n\t\"https://reapply.nl/test\"
curl: (6) Could not resolve host: \nt-X
curl: (6) Could not resolve host: POST
…
```

Ok, if we don't want to start replacing all escaped characters here, this is pretty much end-of-the-line.

***

Note that placing the `print request.debugDescription` line inside the code base will also return properly formatted output. This oldscool style of debugging is something we try to avoid, as it has the potential to slip into our commits and clutter our code base.

Perhaps a future version of Alamofire and/or Xcode won't have this problem.

[jshier]: https://github.com/Alamofire/Alamofire/issues/1712#issuecomment-255560370

