# HTTP and JSON

As of v1.12.0, you can now make HTTP requests from Squirrel scripts.
HTTP requests allow you to query online APIs, send, retrieve data and
much more.

This is particularly useful for custom APIs you might want to build for
your servers, for instance if you want to wrap a database with an API so
that your servers can save player stats.

!!! warning

For security reasons, private network hosts, such as `localhost` or
`192.168.1.106` are blocked by default, meaning you cannot make HTTP
requests to them. This includes a blanket ban on IPv6 hosts.

You are also limited to `HTTP` and `HTTPS` for protocols. Any other
protocols will prevent the request from being made.
::::

## Launch Arguments

There are a few launch arguments you may use to bypass some of the
limitations, or outright disable HTTP requests.

These should be applied to your client or server\'s launch commandline.

  ------------------------ -------------------------------------------------------------------------------------------------------------------
  Name                     Description
  `-allowlocalhttp`        Disables private network checks for HTTP requests, allowing any IPv4 and IPv6 host to be used.
  `-disablehttprequests`   Disables HTTP requests. Any attempts at making requests will fail.
  `-disablehttpssl`        Disables SSL verifications, useful when the host\'s SSL certificate is invalid, and insecure HTTP cannot be used.
  ------------------------ -------------------------------------------------------------------------------------------------------------------

  : Launch Arguments

## HTTP API

This section documents all the available functions, structs and enums
used to make HTTP request in Squirrel scripts.

!!! warning

HTTP requests are multithreaded, as such they will run in the background
until completion, whether successful or failed. Be mindful of how many
requests you make at a time, as you may potentially get ratelimited or
blacklisted by the remote host. Use the callbacks to execute code when a
request has completed.
::::

### Data

The HTTP system uses a few enums and structs for requests and their
callbacks.

# httpapi_enums_httpmethod

> Contains the different allowed methods for a HTTP request. Please
> work.
>
> > Uses the `GET` HTTP method for the request.
>
> > Uses the `POST` HTTP method for the request.
>
> > Uses the `HEAD` HTTP method for the request.
>
> > Uses the `PUT` HTTP method for the request.
>
> > Uses the `DELETE` HTTP method for the request.
>
> > Uses the `PATCH` HTTP method for the request.
>
> > Uses the `OPTIONS` HTTP method for the request.

# httpapi_structs_httprequest

> Contains the settings for a HTTP request. This is used for the more
> flexible `NSHttpRequest` function.
>
> > HTTP method used for this HTTP request.
>
> > Base URL of this HTTP request.
>
> > Headers used for this HTTP request. Some may get overridden or
> > ignored.
>
> > Query parameters for this HTTP request.
>
> > The content type of this HTTP request. Defaults to application/json
> > & UTF-8 charset.
>
> > The body of this HTTP request. If set, will override
> > queryParameters.
>
> > The timeout for this HTTP request in seconds. Clamped between 1 and
> > 60.
>
> > If set, the override to use for the User-Agent header.

!!! warning

Only `POST` requests can send a body to the remote end. You may only
choose to send a body, or query parameters. Having both will give
priority to the body and clear the parameters.
::::

# httpapi_structs_httprequestresponse

> Contains the response from the remote host for a successful HTTP
> request.
>
> > The status code returned by the remote the call was made to.
>
> > The body of the response.
>
> > The raw headers returned by the remote.
>
> > A key -\> values table of headers returned by the remote.

# httpapi_structs_httprequestfailure

> Contains the failure code and message when Northstar fails to make a
> HTTP request.
>
> > The status code returned by the remote the call was made to.
>
> > The reason why this HTTP request failed.

### Functions

!!! warning

Your mod needs to be load priority 1 or above to use `HttpRequest` and
`HttpRequestResponse` in your script.
::::

# httpapi_funcs_nshttprequest
:::

> Launches a HTTP request with the given request data. This function is
> async, and the provided callbacks will be called when it is completed,
> if any.
>
> **Parameters:**
>
> -   `HttpRequest requestParameters` - The parameters to use for this
>     request.
> -   `[OPTIONAL] void functionref( HttpRequestResponse ) onSuccess` -
>     The callback to execute if the request is successful.
> -   `[OPTIONAL] void functionref( HttpRequestFailure ) onFailure` -
>     The callback to execute if the request has failed.
>
> **Returns:**
>
> -   Whether or not the request has been successfully started.
>
> **Example:**
>
> Below is a working example of an HTTP request for a mod.
>
> As you can see, you can either use named functions for the callbacks,
> or create lambdas. Lambdas are particularly useful as they let you
> capture local variables of the functions to re-use later such as
> `callback` in this example.
>
> ``` 
> HttpRequest request
> request.method = HttpRequestMethod.GET
> request.url = "https://my.spyglass.api/sanctions/get_by_id"
> request.queryParameters[ "id" ] <- [ id.tostring() ]
>
> void functionref( HttpRequestResponse ) onSuccess = void function ( HttpRequestResponse response ) : ( callback )
> {
>     SpyglassApi_OnQuerySanctionByIdSuccessful( response, callback )
> }
>
> void functionref( HttpRequestFailure ) onFailure = void function ( HttpRequestFailure failure ) : ( callback )
> {
>     SpyglassApi_OnQuerySanctionByIdFailed( failure, callback )
> }
>
> return NSHttpRequest( request, onSuccess, onFailure )
> ```

# httpapi_funcs_nshttpget

> Launches an HTTP GET request at the specified URL with the given query
> parameters. Shortcut wrapper of NSHttpRequest(). This function is
> async, and the provided callbacks will be called when it is completed,
> if any.
>
> **Parameters:**
>
> -   `string url` - The url to make the HTTP request at.
> -   `[OPTIONAL] table< string, array< string > > queryParameters` - A
>     table of key value parameters to insert in the url.
> -   `[OPTIONAL] void functionref( HttpRequestResponse ) onSuccess` -
>     The callback to execute if the request is successful.
> -   `[OPTIONAL] void functionref( HttpRequestFailure ) onFailure` -
>     The callback to execute if the request has failed.
>
> **Returns:**
>
> -   Whether or not the request has been successfully started.
>
> **Example:**
>
> This is the same example as NSHttpRequest()\'s example. However, it
> uses this function instead.
>
> ``` 
> table<string, array<string> > params
> params[ "id" ] <- [ id.tostring() ]
>
> void functionref( HttpRequestResponse ) onSuccess = void function ( HttpRequestResponse response ) : ( callback )
> {
>     SpyglassApi_OnQuerySanctionByIdSuccessful( response, callback )
> }
>
> void functionref( HttpRequestFailure ) onFailure = void function ( HttpRequestFailure failure ) : ( callback )
> {
>     SpyglassApi_OnQuerySanctionByIdFailed( failure, callback )
> }
>
> return NSHttpGet( "https://my.spyglass.api/sanctions/get_by_id", params, onSuccess, onFailure )
> ```

# httpapi_funcs_nshttppostquery

> Launches an HTTP POST request at the specified URL with the given
> query parameters. Shortcut wrapper of NSHttpRequest(). This function
> is async, and the provided callbacks will be called when it is
> completed, if any.
>
> **Parameters:**
>
> -   `string url` - The url to make the HTTP request at.
> -   `[OPTIONAL] table< string, array< string > > queryParameters` - A
>     table of key value parameters to insert in the url.
> -   `[OPTIONAL] void functionref( HttpRequestResponse ) onSuccess` -
>     The callback to execute if the request is successful.
> -   `[OPTIONAL] void functionref( HttpRequestFailure ) onFailure` -
>     The callback to execute if the request has failed.
>
> **Returns:**
>
> -   Whether or not the request has been successfully started.

# httpapi_funcs_nshttppostbody

> Launches an HTTP POST request at the specified URL with the given
> body. Shortcut wrapper of NSHttpRequest(). This function is async, and
> the provided callbacks will be called when it is completed, if any.
>
> This is the more interesting POST function, as you can use it to
> convert a table into JSON and \"POST\" it to the remote server.
>
> **Parameters:**
>
> -   `string url` - The url to make the HTTP request at.
> -   `string body` - The body to send with the request. Expects JSON by
>     default.
> -   `[OPTIONAL] void functionref( HttpRequestResponse ) onSuccess` -
>     The callback to execute if the request is successful.
> -   `[OPTIONAL] void functionref( HttpRequestFailure ) onFailure` -
>     The callback to execute if the request has failed.
>
> **Returns:**
>
> -   Whether or not the request has been successfully started.
>
> **Example:**
>
> In this example, we\'ll convert a table to JSON, and send it over to a
> web API.
>
> ``` 
> table myData = {}
> myData[ "uid" ] <- player.GetUID()
> myData[ "username" ] <- player.GetPlayerName()
> myData[ "isBot" ] <- player.IsBot().tostring()
>
> string json = EncodeJSON( myData )
> if ( NSHttpPostBody( "https://api.stats.tf/player/connect", json ) )
> {
>     printt( "Successfully attempted to upload player connection stats to API." )
> } 
> ```

# httpapi_funcs_nsissuccesshtppcode

> Checks whether or not the given HTTP status code is considered a
> \"success\" code.
>
> This is true for status codes between 200 and 299.
>
> **Parameters:**
>
> -   `int statusCode` - The status code to verify.
>
> **Returns:**
>
> -   Whether or not the given status code is considered successful.

## JSON API {#json_overview}

!!! warning

The JSON parser currently supports the following types for values:
`string`, `integer`, `float`, `bool`, `table`, and `array`.

Tables and arrays can only hold supported types. Unsupported types will
be ignored. Keys can only be strings.

The JSON parser currently does not support keys holding `null` values,
and simply won\'t include them in decoded tables or encoded JSON
strings.
::::

#json_funcs_decodejson

> Converts a JSON string to a Squirrel table.
>
> **Parameters:**
>
> -   `string json` - The JSON string to decode into a table.
> -   `[OPTIONAL] bool fatalParseErrors` - Whether or not parsing errors
>     should throw a fatal script error. Default to false.
>
> **Returns:**
>
> -   The table decoded from the JSON string on success, or an empty
>     table `{}` on parse failure (if fatalParseErrors is false).

# json_funcs_encodejson

> Converts a Squirrel table to a JSON string.
>
> **Parameters:**
>
> -   `table data` - The table to encode to a JSON string.
>
> **Returns:**
>
> -   The JSON string parsed from the Squirrel table.

Paired with `/reference/northstar/httprequests` , this allows you to send and retrieve JSON data from
external sources.
