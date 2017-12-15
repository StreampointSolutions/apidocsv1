# SeminarTrack

An object that represents speaker session tracks.

## Properties

Field | Type | Description
------| ---- | -----------
Colour | string | color display of track
InvertText | boolean | sets text to white to be visible for dark backgrounds
Name | string | name of track
TrackUid | string | unique ID

## Get Seminar Tracks

> REST Request Example

``` csharp
public void GetSeminarTracksExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/speakers/GetSeminarTracks";

    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<SeminarTrack>));

    var results = (List<SeminarTrack>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}

```

``` python
function getSeminarCreditTracksExample()
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const endpoint = "/speakers/GetSeminarTracks";

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
        "Colour": "#70502D",
        "InvertText": true,
        "Name": "Benefits & Compensation",
        "TrackUid": "52e612e9-3ae7-e311-8eb4-1250568c0706"
    },
    ...
]
```

Returns a list of all seminar tracks

### Returns
A list of `SeminarTrack` objects