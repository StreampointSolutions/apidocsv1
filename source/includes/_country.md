# Country

The country field that is found in the registrant's personal address information.

## Properties

Field | Type | Description
------| ---- | -----------
Code | string | Country abbreviation
CountryID | integer | Unique identifier
Name | string | Country full name
Order | integer | Order in which to appear in the country list

## <a name="GetCountryList"></a>Get List of Countries

> REST Request Example

``` csharp
public void GetCountryListExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/event/countries";



    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<Country>));

    var results = (List<Country>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
	
	
}

```

``` python
function getCountryListExample() 
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const dataPullEndpoint = "/event/countries";

	$pullRequest = curl_init(baseUrl . dataPullEndpoint); 
	curl_setopt($pullRequest, CURLOPT_HTTPGET, true);
	$header = array();
	$header[] = "Content-type: application/json";
	$header[] = "x-auth-token: " . token;

	curl_setopt($pullRequest, CURLOPT_HTTPHEADER, $header);
	curl_setopt($pullRequest, CURLOPT_FORBID_REUSE, true);
	curl_setopt($pullRequest, CURLOPT_TIMEOUT, 3600);
	curl_setopt($pullRequest, CURLOPT_RETURNTRANSFER, true);

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
        "Code": "US",
        "CountryID": 2,
        "Name": "United States",
        "Order": 10
    },
    {
        "Code": "CA",
        "CountryID": 1,
        "Name": "Canada",
        "Order": 20
    }

]
```



There are some Streampoint objects and methods that reference countries based on the unique id rather than name.  Use this method for retrieving the entire look up list of an event's country options.


### Returns
A list of `Country` objects