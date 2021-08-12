### FloppySend SMS API ( New Version )

FloppySend's SMS API is well-defined software interface which enables code to send short messages via a SMS Gateway. Use our simple SMS APIs to integrate SMS text messaging with your already existing business applications and systems. 

Request Types
 - GET: If the request is get method you need to append params as query string inside the params section
 - POST: If request is post method you need to append params as x-www-form-urlencoded inside the body of the request

```
https://api.floppy.ai/sms
```
```
{
    X-api-key:"Your x-api-key" (string required)
    X-Secret-Hash:"Your x-secret-hash" 
    (string required if added from dashboard)
}
```
You can get your X-Api-Key And X-Secret-Hash from your [account setting](https://app.floppysend.com/) page in Api Keys section

#### Parameters
  | Parameter | Type | Required | Description |
  | --------- | ---- | -------- | ----------- |
  | To | String | Yes | number/numbers sending to |
  | From | String | Yes | sender which will appear to the user |
  | Dcs | String | Yes | if message contains unicode: 8, if message doenst contain unicode: 0 |
  | Text | String | Yes | message body |
  | Sched | String | Optional | iso format |

#### SMS API Responses
```JSON
{
    "Result": "Success",
    "Datainfo": 
    [
        {
            "Status": "Sent",
            "ID": "Response_Id",
            "Error_Code": "0",
            "Error_Desc": "0"
        }
    ]
}
```

#### SMS API Code Sample

```PHP
//PHP

<?php

$curl = curl_init();
curl_setopt_array($curl, array(
    CURLOPT_URL => 'https://api.floppy.ai/sms',
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_ENCODING => '',
    CURLOPT_MAXREDIRS => 10,
    CURLOPT_TIMEOUT => 0,
    CURLOPT_FOLLOWLOCATION => true,
    CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
    CURLOPT_CUSTOMREQUEST => 'POST',
    CURLOPT_POSTFIELDS =>
    'to={to_number}&from={sender}&dcs={dcs}&text={message_body}&sched=2021-07-02T11%3A16%3A28',
    CURLOPT_HTTPHEADER => array(
    'x-api-key: "Your x-api-key"',
    'Content-Type: application/x-www-form-urlencoded'
                                ),
    ));
$response = curl_exec($curl);
curl_close($curl);
echo $response;
```

```ruby
//Ruby

require "uri"
require "net/http"
url = URI("https://api.floppy.ai/sms")
https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true
request = Net::HTTP::Post.new(url)
request["x-api-key"] = "Your x-api-key"
request["Content-Type"] = "application/x-www-form-urlencoded"
request.body =
"to={to_number}&from={sender}&dcs={dcs}&text={message_body}&sched=2021-07-02T11%3A16%3A28"
response = https.request(request)
puts response.read_body
```

```Java
//JAVA

//The OkHttpClient is an external package, you need to install it before making the request, 
//And don't forget to add user permission for the internet inside "\MyApplication\app\src\main\AndroidManifest.xml"
//Also, you need to add required dependencies inside "MyApplication\app\build.gradle"

OkHttpClient client = new OkHttpClient().newBuilder()
.build();
MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");
RequestBody body = RequestBody.create(mediaType,
"to={to_number}&from={sender}&dcs={dcs}&text={message_body}&sched=2021-07-02T11:16:28");
Request request = new Request.Builder()
.url("https://api.floppy.ai/sms")
.method("POST", body)
.addHeader("x-api-key", "Your x-api-key")
.addHeader("Content-Type", "application/x-www-form-urlencoded")
.build();
Response response = client.newCall(request).execute();
```

```C#
//C#

var client = new RestClient("https://api.floppy.ai/sms");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("x-api-key", "Your x-api-key");
request.AddHeader("Content-Type", "application/x-www-form-urlencoded");
request.AddParameter("to", "{to_number}");
request.AddParameter("from", "{sender}");
request.AddParameter("dcs", "{dcs}");
request.AddParameter("text", "{message_body}");
request.AddParameter("sched", "2021-07-02T11:16:28");
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

```JavaScript
//NodeJs
//Make sure to import Axios and install npm packages before doing the request

var axios = require('axios');
var qs = require('qs');
var data = qs.stringify({
    'to': 'TO-NUMBER',
    'from': 'FROM-SENDER',
    'dcs': '0',
    'text': 'MESSAGE-BODY',
    'sched': 'Time-IsoFormat'
});
var config = {
    method: 'post',
    url: 'https://api.floppy.ai/sms',
    headers: {
        'x-api-key': 'YOUR-API-KEY',
        'Content-Type': 'application/x-www-form-urlencoded'
    },
    data: data
};

axios(config)
    .then(function (response) {
        console.log(JSON.stringify(response.data));
    })
    .catch(function (error) {
        console.log(error);
    });
```
