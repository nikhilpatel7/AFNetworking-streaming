# AFNetworking+streaming
[![Version](https://img.shields.io/cocoapods/v/AFNetworking+streaming.svg?style=flat)](http://cocoadocs.org/docsets/AFNetworking+streaming)
[![License](https://img.shields.io/cocoapods/l/AFNetworking+streaming.svg?style=flat)](http://cocoadocs.org/docsets/AFNetworking+streaming)
[![Platform](https://img.shields.io/cocoapods/p/AFNetworking+streaming.svg?style=flat)](http://cocoadocs.org/docsets/AFNetworking+streaming)

## Why
There are two reasons you might want to stream data instead of loading it all and then parsing the complete set - (a) low memory usage and (b) speed to first item.

In my case it was speed to first item - I had a problem where there was a large dataset that came down slowly so I wanted a way to display the first few items while the rest were still arriving.

My other condition was that I didn't want to modify AFNetowrking to get this to work :) 

## Example
There's an example in the Example folder - open and run Demo.xcworkspace and it should show a list of names. Very exciting.

Take a look at the only view controller in the app and it should become more interesting :| It reads in an array of JSON (see example.json in the project) and parses it as it arrives (using SBJson's stream parsing).

Basically, use `DWHTTPStreamSessionManager` instead of `AFHTTPSessionManager` - it's a direct subclass so everything will work as normal. The only changes are the addition of the GET:parameters:data:success:failure method. This performs exactly the same request as the usual GET method but instead of returning the parsed data   in it's success block it returns each chunk as it arrives.

## TODO
This isn't as efficient as it could be because of the 'don't modify AFNetworking' constraint. `DWHTTPStreamSessionManager` doesn't allow AFNetworking to build up the entire data set but AFNetworking doesn't know that so it still tries to serialize the response and pass it back to the success block. It's a tiny inefficiency and is hidden from you by `DWHTTPStreamSessionManager`. I couldn't find a way to remove it without modifying AFNetworking :(

## Installation
AFNetworking+streaming is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

    pod "AFNetworking+streaming"

## Author
Sam Dean, deanWombourne@gmail.com

## License
AFNetworking+streaming is available under the MIT license. See the LICENSE file for more info.