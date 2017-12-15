# ProvState

This is an object that represents the province / state information that is found in the registrant's personal contact information.

## Properties

Field | Type | Description
------| ---- | -----------
CountryID | integer | ID of the country the province or state belongs to
Name | string | Name of Province or State
Order | integer | Order ID field for sorting
ProvStateID | integer | Unique Identifier

## Get List of Provinces / States

> REST Request Example

``` csharp
public void GetProvStateListExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/event/provstates";

    string parameters = "?country=" + 2;

    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint + parameters);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<ProvState>));

    var results = (List<ProvState>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}}

```

``` python
function getProvStateListExample() 
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const endpoint = "/event/provstates";

	const parameters = "?country=0";

	$pullRequest = curl_init(baseUrl . endpoint . parameters);
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
        "CountryID": 2,
        "Name": "Illinois",
        "Order": 50,
        "ProvStateID": 33
    },
	{
        "CountryID": 2,
        "Name": "Indiana ",
        "Order": 60,
        "ProvStateID": 34
    }

    
]
```

There are some Streampoint objects and methods that reference province and states based on the unique ID rather than name.  Use this method for getting the entire list of IDs and names used for this event.  The country ID is a requested parameter, if you need that list of IDs, they can be retrieved using this [method](#GetCountryList).

### Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
countryID | integer | country ID field | true

### Returns
A list of `ProvState` objects
