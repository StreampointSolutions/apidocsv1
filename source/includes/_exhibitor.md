# Exhibitor

The exhibitor objects allow you to retrieve information associated with an exhibitor's registration details.  You can access their company contact information, their booth details and which industry category they belong to.

## Properties

Field | Type | Description
------| ---- | -----------
Address1 | string | Address 1 of the exhibiting company
Address2 | string | Address 2 of the exhibiting company
BoothNumber | string | booth number or booth code on the show floor
Category | string | exhibitor category name
City | string | city of the exhibiting company
Country | string | country name of the exhibiting company
Description | string | exhibiting company description
Email | string | exhibiting company's main contact email address
ExUID | guid | unique identifier of the exhibitor
Facebook | string | link to company's Facebook site
ImageUID | string | unique id for company logo file
LinkedIn | string | link to company's LinkedIn profile
Name | string | exhibiting company name
Phone | string | company phone number
Sponsor | boolean | indicates if exhibitor is also a sponsor
State | string | state or province of the exhibiting company
Twitter | string | company Twitter handle
Website | string | company website url


## Get Exhibitors 

> REST Request Example

``` csharp
public void GetExhibitorsExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/exhibitors/list";

    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<Exhibitor>));

    var results = (List<Exhibitor>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}
```

``` python
function getExhibitorListExample() 
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const dataPullEndpoint = "/exhibitors/list";

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


> REST Response Output in JSON

``` json
[
    {
        "Address1": null,
        "Address2": null,
        "BoothNumber": "200",
        "Category": "HR Management Consultants",
        "City": null,
        "Country": null,
        "Description": "National experts in 360 degree feedback, employee engagement, and leadership development, 3D Group supports organizations of all sizes with flexible, easy-to-use assessment solutions. Whether using our Leadership Navigator® suite of 360 Degree Feedback surveys or customized tools, our consultants tailor every solution to fit the unique needs of each client.",
        "Email": null,
        "ExUID": "3196c857-e4b1-40e3-a97b-26849751f408",
        "Facebook": null,
        "ImageUID": "227D69C8-6fD1-4928-9240-971239E6E34E",
        "LinkedIn": null,
        "Name": "3D Group",
        "Phone": null,
        "Sponsor": false,
        "State": null,
        "Twitter": null,
        "Website": "http://www.3dgroup.net"
    },
    {
        "Address1": null,
        "Address2": null,
        "BoothNumber": "312",
        "Category": "Recruiting, Staffing & Search",
        "City": null,
        "Country": null,
        "Description": "ADP’s Talent Acquisition Solutions offers companies the most comprehensive talent acquisition services in the industry.  Our client teams have extensive experience delivering recruitment process outsourcing, AIRS® recruiter training, background screening, substance abuse testing, I-9/E-verify services, and other recruitment technology.  For more information visit www.adp.com.",
        "Email": null,
        "ExUID": "d2380ee2-e34b-47f4-ab52-01b1d1165da3",
        "Facebook": null,
        "ImageUID": "26DACC3F-FCB1-404A-A97D-7079A2195C6D",
        "LinkedIn": null,
        "Name": "ADP",
        "Phone": null,
        "Sponsor": false,
        "State": null,
        "Twitter": null,
        "Website": "http://www.adp.com/RPO"
    }
 
]
```

Returns a list of exhibitors, optionally filtered by request parameters.


### Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
searchNameNum | string | filter exhibitors by searching by name or number | false
searchDesc | string | filter exhibitors by searching description  | false
category | string | category to filter exhibitors by, see `GetExhibitorCategories()` | false
provStateID | integer | province or state id to filter exhibitors by, see `GetProvStateList()` | false
countryID | integer | country id to filter exhibitors by, see `GetCountryList()` | false
sponsor | boolean | if true only returns exhibitors who are also sponsors | false
startLetter | string | filter based on the first letter of name | false

### Returns
A list of `Exhibitor` objects



## Get Exhibitor Details

> REST Request Example

``` csharp
public void GetExhibitorDetailsExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/exhibitors/details";

    string parameters = "?exUID=" + "631F3D72-0C4D-4992-83DC-94E0C2D54911";

    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint + parameters);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<Exhibitor>));

    var results = (List<Exhibitor>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}
```

``` python
function getExhibitorDetailsExample() 
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const dataPullEndpoint = "/exhibitors/details";

	const parameters = "?exUID=" . "fe6eb536-bc1b-407f-a2c5-180c1aff02b2";

	$pullRequest = curl_init(baseUrl . dataPullEndpoint . parameters); 
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

> REST Response Output in JSON

``` json
{
    "Address1": "2000 Powell St.",
    "Address2": "Suite 970",
    "BoothNumber": "200",
    "Category": "HR Management Consultants",
    "City": "Emeryville",
    "Country": "United States",
    "Description": "National experts in 360 degree feedback, employee engagement, and leadership development, 3D Group supports organizations of all sizes with flexible, easy-to-use assessment solutions. Whether using our Leadership Navigator® suite of 360 Degree Feedback surveys or customized tools, our consultants tailor every solution to fit the unique needs of each client.",
    "Email": "hidden@hidden.com",
    "ExUID": "631F3D72-0C4D-4992-83DC-94E0C2D54911",
    "Facebook": "https://www.facebook.com/360feedback",
    "ImageUID": "227D69C8-67D1-4928-9240-971239E6E34E",
    "LinkedIn": "http://www.linkedin.com/company/3d-group",
    "Name": "3D Group",
    "Phone": "333-333-3333",
    "Sponsor": false,
    "State": "California ",
    "Twitter": "https://twitter.com/3DGroup",
    "Website": "http://www.3dgroup.net"
}
```


Returns information about a specific exhibitor.  

###Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
ExUID | string | Exhibitor unique id | true

###Returns
An `Exhibitor` object

## Get Exhibitor Categories

> REST Request Example

``` csharp
public void GetExhibitorCategoriesExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/exhibitors/categories";

    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<ExhibitorCategory>));

    var results = (List<ExhibitorCategory>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}
```

``` python
function getExhibitorCategoriesExample()
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const dataPullEndpoint = "/exhibitors/categories";

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

> REST Response Output in JSON

``` json
[
    {
        "CategoryUID": "6dde2169-9d25-4591-9c47-be77b364f84a",
        "Name": "Advertising & Promotional Products"
    }
]
```


Exhibiting companies may often be grouped or assigned into categories.  If applicable, you can retrieve the complete list of categories for the event.

###Returns
A list of exhibitor booth categories


