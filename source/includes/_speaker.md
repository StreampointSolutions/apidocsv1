# Speaker

This is an object that represents a speaker's profile.  

## Properties

Field | Type | Description
------| ---- | -----------
Bio | string | Contains the person's biographical information
Facebook | string | URL to the speaker's facebook page
Image | string | Image ID of the speaker's profile picture
LinkedIn | string | URL to the speaker's LinkedIn page
Seminars | list of `Seminar` objects | List of sessions the speaker is presenting
SpeakerUID | string | Speaker unique ID
SpeakerFiles | list of `SpeakerFile` objects | Speaker's presentation files
Twitter | string | Speaker's Twitter handle
Youtube | string | URL to YouTube video

## Get Speaker List

> REST Request Example

``` csharp
public void FilterSpeakerListExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/speakers/list";



    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;            
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<Speaker>));

    var results = (List<Speaker>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}

```

``` python
function filterSpeakerListExample() 
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const endpoint = "/speakers/list";

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
        "Bio": "Nancy Smith is from Denver, Colorado.  She founded her company, Ace Jets Inc, in 2010.",
        "Facebook": null,
        "Image": "27f23102-ac42-4a97-a019-a6ea15efb3fc",
        "LinkedIn": null,
        "Personal": {
            "Address1": null,
            "Address2": null,
            "AlternateEmail": null,
            "Association": "Ace Jet Inc",
            "BadgeID": null,
            "BadgeName": "Nancy",
            "City": "Denver",
            "ConfirmationNumber": "777777-159",
            "Country": "United States",
            "Email": null,
            "Fax": null,
            "FirstName": "Nancy",
            "Guests": null,
            "LastName": "Smith",
            "PPID": "38c4f85a-1375-4a14-b18d-ae3b925830dc",
            "Phone": "123-123-1234",
            "Prefix": "Ms.",
            "Profile": null,
            "ProvState": "Colorado",
            "RegType": {
                "Name": "Speaker",
                "RegtypeUID": "af4c3864-d9c0-4801-b329-1f5bc282b219"
            },
            "Seminars": null,
            "Title": "CEO",
            "Zip": null
        },
        "Seminars": [
            {
                "AlternateName": null,
                "CreditType": {
                    "CreditTypeUid": "45519abd-9e73-49fa-8a9f-c1f3433q53c2",
                    "Name": "Global"
                },
                "Description": "This session will cover entrepreneurial basics",
                "End": "/Date(1409091300000-0400)/",
                "Image": null,
                "Location": "Room: 205A",
                "Name": "Starting Your Own Business",
                "Qty": 0,
                "SeminarUid": "45e728fe-3eba-4cff-9eac-1da63da188aa",
                "ShortName": null,
                "Start": "/Date(1409086800000-0400)/",
                "Track": {
                    "Colour": "#E6108D",
                    "InvertText": true,
                    "Name": "Global",
                    "TrackUid": "57e362e9-3de7-e311-8eb4-0050568c0006"
                }
            }
        ],
        "SpeakerFiles": [
            {
                "FileName": "AceInc.pdf",
                "FileUID": "8e03ce8c-695d-4dea-bccc-500c3f674b34",
                "SeminarUID": "453728fe-3eba-4cff-9eac-1da63da188aa"
            }
        ],
        "SpeakerUID": "d31ea944-0ae8-e311-a4fc-005056a467e1",
        "Twitter": null,
        "Youtube": null
    },
    ...
]
```

Returns a list of speakers

### Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
keywords | string | keywords to search for | false
trackUid | string | filter on seminar track, see `GetSeminarTracks()` | false
typeUid | string | filter on seminar type | false
creditTypeUid | string | filter on seminar credit type, see `GetSeminarCreditTypes()`| false
date | string | filter on a date | false

### Returns
A filtered list `Speaker` objects

