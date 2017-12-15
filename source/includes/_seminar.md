# Seminar

A `Seminar` object in the Streampoint registration system can represent a product, session, workshop, ticket or anything that has a cost associated to it.

## Properties

Field | Type | Description
------| ---- | -----------
AlternateName | string | Alternate name for seminar
CreditType | `SeminarCreditType`  | credit type, used primarily for speaker sessions
Description | string | description of seminar
End | datetime | end time of the seminar
Image | string | image ID, used primarily for speaker profile images
LastModified | string | Date of when the seminar was last edited
Location | string | location of seminar(i.e. room, hall, venue)
Name | string | Name of seminar
Qty | integer | qty purchased or signed up for
Price | decimal | the price this seminar was registered for
SeminarUid | string | unique ID
ShortName | string | abbreviated version of the seminar name
Start | datetime | start time of the seminar
Track | `SeminarTrack` | seminar track, used primarily for speaker sessions

## Get All Seminars


> REST Request Example

``` csharp
public void GetAllSeminarsExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/seminars";
	
    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<Seminar>));

    var results = (List<Seminar>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}

```

``` python
function getAllSeminarsExample() 
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const endpoint = "/seminars";

	$pullRequest = curl_init(baseUrl . endpoint);
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
        "AlternateName": null,
        "CreditType": null,
        "Description": "",
        "End": "/Date(1409000400000-0400)/",
        "Image": null,
        "Location": "Hall B",
        "Name": "Monday Lunch",
		"Price": 20,
        "Qty": 0,
        "SeminarUid": "37c9e205-01er-4722-9072-7c3f9dc384b2",
        "ShortName": null,
        "Start": "/Date(1408995000000-0400)/",
        "Track": null
    },
    {
        "AlternateName": null,
        "CreditType": null,
        "Description": "",
        "End": "/Date(1409014800000-0400)/",
        "Image": null,
        "Location": "Hall E",
        "Name": "Attendee & Exhibitor Happy Hour",
		"Price": 25,
        "Qty": 0,
        "SeminarUid": "898213ef-a684-416d-9f7b-25f9c3c547ea",
        "ShortName": null,
        "Start": "/Date(1409011200000-0400)/",
        "Track": null
    },
    ...
]
```

Retrieves an entire list of seminars for the event.  Optionally, the list can be filtered by registration type.

### Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
regTypeUID | string | regtype unique ID field | false

### Returns
A list of `Seminar` objects


## Search Seminars

> REST Request Example

``` csharp
public void SearchSeminarsExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/seminar/search";


    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<Seminar>));

    var results = (List<Seminar>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}

```

``` python
function searchSeminarExample() 
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const endpoint = "/seminar/search";

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
{
        "AlternateName": "Collective Bargaining Issues",
        "CreditType": {
            "CreditTypeUid": "45519abd-9e73-4afa-7a2f-c1f3433cf3c2",
            "Name": "Global"
        },
        "Description": "This session will cover a wide range of laws that apply to the collective bargaining process.  ",
        "End": "/Date(1408918500000-0400)/",
        "Image": null,
        "Location": "Room: 1010A",
        "Name": "Collective Bargaining Issues: An International Perspective ",
        "Qty": 0,
        "SeminarUid": "07db01ae-f7b7-4723-8761-b9c7ce953235",
        "ShortName": CBI,
        "Start": "/Date(1408914000000-0400)/",
        "Track": {
            "Colour": "#E6108D",
            "InvertText": true,
            "Name": "Global",
            "TrackUid": "57e662e9-3de7-e321-8sb4-0151568c0306"
        }
    },
    ...
]
```

Get a list of seminars based on search criteria.

### Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
Keywords | string | keywords to search | false
datetime | string | date to filter on | false
TrackUID | string | track to filter on, see `GetSeminarTracks()` | false
CreditTypeUID | string | credit type to filter on, see `GetSeminarCreditTypes()` | false


### Returns
A list of `Seminar` objects
