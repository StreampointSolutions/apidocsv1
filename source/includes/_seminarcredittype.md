# SeminarCreditType

An object that represents speaker session credit types.

## Properties

Field | Type | Description
------| ---- | -----------
CreditTypeUid | string | Unique ID
Name | string | Name of session credit type

## Get Seminar Credit Types

> REST Request Example

``` csharp
public void GetSeminarCreditTypesExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/speakers/GetSeminarCreditTypes";
	
    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<SeminarCreditType>));

    var results = (List<SeminarCreditType>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}

```

``` python
function getSeminarCreditTypesExample()
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const endpoint = "/speakers/GetSeminarCreditTypes";

	$pullRequest = curl_init(baseUrl . endpoint);
	curl_setopt($pullRequest, CURLOPT_HTTPGET, true);
	$header = array();
	$header[] = "Content-type: application/json";
	$header[] = "x-auth-token: " . token;

	curl_setopt($pullRequest, CURLOPT_HTTPHEADER, $header);
	curl_setopt($pullRequest, CURLOPT_FORBID_REUSE, true);
	curl_setopt($pullRequest, CURLOPT_TIMEOUT, 3600);
	//curl_setopt($pullRequest, CURLOPT_RETURNTRANSFER, true);

	$response = curl_exec($pullRequest);
	curl_close($pullRequest);

	//De-serialize the JSON data into useful objects
	$results = json_decode($response);

	//At this point results contains the data set
	print_r($results);
}
```

> REST Response Output

``` json
[
    {
        "CreditTypeUid": "5ed4548b-1175-4705-818e-499ec20d3ba4",
        "Name": "Business"
    },
    ...
]
```

Returns a list of all seminar credit types

### Returns
A list of `SeminarCreditType` objects