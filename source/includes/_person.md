# Person

This is an object that represents a single registrant.

## Properties

Field | Type | Description
------| ---- | -----------
Address1 | string | Street address, P.O. box
Address2 | string | Apartment, suite, unit, floor etc.
AlternateEmail | string | Secondary email address
Association | string | Company / Organization
BadgeID | string | An optional field that can be displayed on a badge
BadgeName | string | An optional field that can be displayed on a badge
City | string | Address city
ConfirmationNumber | string | Person's unique identifier
Country | string | Address country
Demographics | list of `Question` objects | List of all demographic answer data
Email | string | Primary email address
Fax | string | Fax number
FirstName | string | First name
Guests | list of `Person` objects | List of all guests registered under this person
LastName | string | Last name
LastModified | string | Date of when personal information was last edited
Membershipcode | string | Membership ID if applicable
Payments | list of `Payment` objects | List of all payment transactions
Phone | string | Phone
PPID | string | Person's unique identifier in the form of a guid.  It is used in referencing payment information.
Prefix | string | Prefix
ProvState | string | Province or State if applicable
Questions | list of question answer values | List of all question and answer data (legacy field)
RegType | `RegistrationType` object | A person's registration type
Seminars | list of `Seminar` objects | A list of sessions, workshops or products registered by the person
Tags | list of tag values | A list of status tags assigned to the person
Title | string | Job title
Zip | string | Address zip

## Authenticate Person

> REST Request Example

``` csharp
public void AutenticatePersonExample()
{
	const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string authenticatePersonEndpoint = "/login/authenticatePerson";
	string username = "testuser123@test.streampoint.com";
    string password = "Password123";
    string eventGuid = "1E55D1E7-7714-4A2B-B9D1-A2C0DBA97D07";
	
	var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + authenticatePersonEndpoint + "?username="+ username +"&password=" + password + "&eventGUIDin=" + eventGuid);
	pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 500000;
    pullRequest.Headers.Add("x-auth-token", token);
	
	
}
```

``` python
function authenticatePersonExample()
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const authenticatePersonEndpoint = "/login/authenticatePerson";

	const username = "testuser123@test.streampoint.com";
	const password = "Password123";
	const eventGuid = "1E55D1E7-7714-4A2B-B9D1-A2C0DBA97D07";

	$pullRequest = curl_init(baseUrl . authenticatePersonEndpoint . "?username=" . username  . "&password=" . password . "&eventGUIDin=" . eventGuid);
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
{
	"ConfirmationId":"1234567-987",
	"FirstName":"John",
	"IsAuthenticated":true,
	"LastName":"Smith",
	"ReturnMessage":"success",
	"UserEmail":"testuser123@test.streampoint.com"
}

```

Authenticates if the person has a valid registration account in the Streampoint system.

### Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
usernname | string | Streampoint user account email | true
password | string | Streampoint  user account password| true
eventguid | string | Event ID field in the Streampoint registration system | true



### Returns
Field | Type | Description 
------|------|-------------
ConfirmationId | string | Person's unique identifier
FirstName | string | First name of the person
IsAuthenticated | boolean | true or false if the person was successfully authenticated
LastName | string | Last name of the person
ReturnMessage | string | If authenticated is true - "success", if false - "unable to validate user"
UserEmail | string | The person's account email

## Authenticate Person By Unique Code

> REST Request Example

``` csharp
public void AutenticatePersonByUniqueCodeExample()
{
	const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string authenticatePersonEndpoint = "/login/authenticatePersonByUniqueCode";
	string uniqueCode = "XXXXXXXXXXXX";
    string eventGuid = "1E55D1E7-7714-4A2B-B9D1-A2C0DBA97D07";
	
	var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + authenticatePersonEndpoint + "?uniqueCode="+ uniqueCode + "&eventGUIDin=" + eventGuid);
	pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 500000;
    pullRequest.Headers.Add("x-auth-token", token);
	
}
```

``` python
function authenticatePersonByUniqueCodeExample()
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";

	const authenticatePersonEndpoint = "/login/authenticatePersonByUniqueCode";
	const eventGuid = "47B47D89-07B3-493E-9DB6-FF19C62D486C";
	const uniqueCode = "BRUMEAW3OF5J";

	$pullRequest = curl_init(baseUrl . authenticatePersonEndpoint . "?uniqueCode=" . uniqueCode  . "&eventGUIDin=" . eventGuid);
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
	"ConfirmationId":"1234567-987",
	"FirstName":"John",
	"IsAuthenticated":true,
	"LastName":"Smith",
	"ReturnMessage":"success",
	"UserEmail":""
}

```
Authenticates if the person has a valid registration account in the Streampoint system.

### Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
uniqueCode | string | Streampoint assigned unique code | true
eventguid | string | Event ID field in the Streampoint registration system | true

### Returns
Field | Type | Description 
------|------|-------------
ConfirmationId | string | Person's unique identifier
FirstName | string | First name of the person
IsAuthenticated | boolean | true or false if the person was successfully authenticated
LastName | string | Last name of the person
ReturnMessage | string | If authenticated is true - "success", if false - "unable to validate user"
UserEmail | string | The person's account email if applicable


## Export Registrants

> REST Request Example

``` csharp
public void ExportRegistrantsExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/dataExport/registrants";

    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    //This can take some time for shows with a large number of registrants...
    pullRequest.Timeout = 3600000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<Person>));

    var results = (List<Person>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}
```

``` python
function exportRegistrantsExample() 
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const endpoint = "/dataExport/registrants";

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
		"Address1": "100 Address St.",
		"Address2": "Unit 55",
		"AlternateEmail": "altsmith@test.streampoint.com",
		"Association": "Streampoint Solutions",
		"BadgeID": "",
		"BadgeName": null,
		"City": "Denver",
		"ConfirmationNumber": "72973-347",
		"Country": "United States",
		"Demographics": [
							 {
								"QuestionAnswer": "Yes",
								"QuestionName": "Are you a Member",
								"UniqueId": "formMemberNo"
							 },
							 {
								"QuestionAnswer": "No",
								"QuestionName": "Are you a Student",
								"UniqueId": "formStudent"
							 },
							 {
								"QuestionAnswer": "No",
								"QuestionName": "Are you an Alumni Member",
								"UniqueId": "formAlumni"
							 },
							 {
								"QuestionAnswer": "Direct Mail",
								"QuestionName": "How did you hear about us",
								"UniqueId": "formHearAboutUs"
							 },
							 {
								"QuestionAnswer": "True",
								"QuestionName": "I agree to the terms and conditions",
								"UniqueId": "formChkBoxAgreement"
							 }
						],
		"Email": "smith@test.streampoint.com",
		"Fax": "123-123-1234",
		"FirstName": "John",
		"Guests": null,
		"LastName": "Smith",
		"Membershipcode": "123456789",
		"PPID": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
		"Payments": [
						 {
							"Amount": 25,
							"AuthNum": "152833",
							"CCType": "Visa",
							"CheckNumber": null,
							"DateChequeReceived": null,
							"DateOnCheque": null,
							"DateTimeStamp": "/Date(1461254419483-0400)/",
							"Last4": "1111",
							"Message": null,
							"Name": "John Smith",
							"OrderID": "1234 - 13801",
							"PPIDCommittedBy": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PPIDFrom": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PPIDTo": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PaymentId": 13801,
							"PaymentType": {
											 "AdminActive": true,
											 "Name": "Credit Card",
											 "PaymentTypeId": 1,
											 "PublicActive": true
											},
							"Status": "CC Approved"
						 },
						 {
							"Amount": 10,
							"AuthNum": "389655",
							"CCType": "Visa",
							"CheckNumber": null,
							"DateChequeReceived": null,
							"DateOnCheque": null,
							"DateTimeStamp": "/Date(1461254907460-0400)/",
							"Last4": "1111",
							"Message": null,
							"Name": "John Smith",
							"OrderID": "1234 - 13802",
							"PPIDCommittedBy": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PPIDFrom": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PPIDTo": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PaymentId": 13802,
							"PaymentType": {
											 "AdminActive": true,
											 "Name": "Credit Card",
											 "PaymentTypeId": 1,
											 "PublicActive": true
											},
							"Status": "CC Approved"
						 }
						],
		"Phone": "123-123-1234",
		"Prefix": "Mr.",
		"Profile": null,
		"ProvState": "Colorado ",
		"Questions": [
						 {
						"Key": "Are you a Member",
						"Value": "Yes"
						 },
						 {
						"Key": "Are you an Alumni Member",
						"Value": "No"
						 },
						 {
						"Key": "Are you a Student",
						"Value": "No"
						 },
						 {
						"Key": "How did you hear about us",
						"Value": "Direct Mail"
						 },
						 {
						"Key": "I agree to the terms and conditions",
						"Value": "True"
						 }
					],
		"RegType": {
					 "Name": "Attendee Member",
					 "RegtypeUID": "d21b5256-47e7-4fa0-8375-696ead8b8534"
					},
		"Seminars": [
					 {
						"AlternateName": "Registration 101",
						"CreditType": null,
						"Description": "Course on registration basics",
						"End": "/Date(1483160400000-0500)/",
						"Image": null,
						"Location": null,
						"Name": "Introduction to Registration 101",
						"Price": 109,
						"Qty": 1,
						"SeminarUid": "17d709eb-391a-428d-bde4-b676d78ae2b8",
						"ShortName": "",
						"Start": "/Date(1404187200000-0400)/",
						"Track": null
					 },
					 {
						"AlternateName": "Onsite Registration Workshop",
						"CreditType": null,
						"Description": "Workshop covering various onsite registration solutions",
						"End": "/Date(1463227200000-0400)/",
						"Image": null,
						"Location": null,
						"Name": "Onsite Registration Workshop",
						"Price": 20,
						"Qty": 1,
						"SeminarUid": "77c6a016-c936-416f-bc29-d9a9e334fe04",
						"ShortName": "",
						"Start": "/Date(1463223600000-0400)/",
						"Track": null
					 },
					 {
						"AlternateName": "Attendee Conference Kit",
						"CreditType": null,
						"Description": "Program Kit filled with resource materials",
						"End": "/Date(1483160400000-0500)/",
						"Image": null,
						"Location": null,
						"Name": "Attendee Conference Kit",
						"Price": 15,
						"Qty": 1,
						"SeminarUid": "96fc7962-977b-4fec-9b5c-1a6efc3c5200",
						"ShortName": "",
						"Start": "/Date(1404187200000-0400)/",
						"Track": null
					 }
					],
		"Tags": [
				 {
					"Key": "Stuffed Status",
					"Value": "Not Stuffed"
				 },
				 {
					"Key": "Print Status",
					"Value": "Not Printed"
				 },
				 {
					"Key": "Present Status",
					"Value": "Not Present"
				 },
				 {
					"Key": "Mat Status",
					"Value": "Not Picked Up"
				 },
				 {
					"Key": "Active Status",
					"Value": "Active"
				 },
				 {
					"Key": "Payment Status",
					"Value": "Partial Payment"
				 },
				 {
					"Key": "Reg Status",
					"Value": "Finished"
				 },
				 {
					"Key": "Language Status",
					"Value": "English"
				 },
				 {
					"Key": "Batch",
					"Value": "Unreconciled"
				 },
				 {
					"Key": "Source",
					"Value": "Attendee"
				 }
				],
		"Title": "Sales Associate",
		"Zip": "11111"
	}
]
```

Returns a list of registants based on optional filters.  If no filters are specified, all registrations in the current event will be returned.  This is essentially a full export of registration data.

### Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
requirePaid | boolean | if true, only paid registrants are returned | false
requireActive | boolean | if true, only active registrants are returned | false
requireComplete | boolean | if true, only complete registrants are returned | false
startDate | string | if passed, only registrants since this date are returned | false

### Returns
A list of `Person` objects


## Export Registrants Paged
> REST Request Example

``` csharp
public void ExportRegistrantsPagedExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/dataExport/registrantsPaged";
	
	//this will return the first 100 records
	string parameters = "?page=1&pageSize=100";
	
    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint + parameters);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    //This can take some time for shows with a large number of registrants...
    pullRequest.Timeout = 3600000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(List<Person>));

    var results = (List<Person>)ser.ReadObject(reader.BaseStream);
    //At this point results contains the data set
}
```

``` python
function exportRegistrantsPagedExample() 
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const endpoint = "/dataExport/registrantsPaged";

	//this will return the first 100 records
	const parameters = "?page=1&pageSize=100";

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
		"Address1": "100 Address St.",
		"Address2": "Unit 55",
		"AlternateEmail": "altsmith@test.streampoint.com",
		"Association": "Streampoint Solutions",
		"BadgeID": "",
		"BadgeName": null,
		"City": "Denver",
		"ConfirmationNumber": "72973-347",
		"Country": "United States",
		"Demographics": [
							 {
								"QuestionAnswer": "Yes",
								"QuestionName": "Are you a Member",
								"UniqueId": "formMemberNo"
							 },
							 {
								"QuestionAnswer": "No",
								"QuestionName": "Are you a Student",
								"UniqueId": "formStudent"
							 },
							 {
								"QuestionAnswer": "No",
								"QuestionName": "Are you an Alumni Member",
								"UniqueId": "formAlumni"
							 },
							 {
								"QuestionAnswer": "Direct Mail",
								"QuestionName": "How did you hear about us",
								"UniqueId": "formHearAboutUs"
							 },
							 {
								"QuestionAnswer": "True",
								"QuestionName": "I agree to the terms and conditions",
								"UniqueId": "formChkBoxAgreement"
							 }
						],
		"Email": "smith@test.streampoint.com",
		"Fax": "123-123-1234",
		"FirstName": "John",
		"Guests": null,
		"LastName": "Smith",
		"Membershipcode": "123456789",
		"PPID": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
		"Payments": [
						 {
							"Amount": 25,
							"AuthNum": "152833",
							"CCType": "Visa",
							"CheckNumber": null,
							"DateChequeReceived": null,
							"DateOnCheque": null,
							"DateTimeStamp": "/Date(1461254419483-0400)/",
							"Last4": "1111",
							"Message": null,
							"Name": "John Smith",
							"OrderID": "1234 - 13801",
							"PPIDCommittedBy": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PPIDFrom": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PPIDTo": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PaymentId": 13801,
							"PaymentType": {
											 "AdminActive": true,
											 "Name": "Credit Card",
											 "PaymentTypeId": 1,
											 "PublicActive": true
											},
							"Status": "CC Approved"
						 },
						 {
							"Amount": 10,
							"AuthNum": "389655",
							"CCType": "Visa",
							"CheckNumber": null,
							"DateChequeReceived": null,
							"DateOnCheque": null,
							"DateTimeStamp": "/Date(1461254907460-0400)/",
							"Last4": "1111",
							"Message": null,
							"Name": "John Smith",
							"OrderID": "1234 - 13802",
							"PPIDCommittedBy": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PPIDFrom": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PPIDTo": "9c76dfab-96e2-4b41-8415-ca621d9c401e",
							"PaymentId": 13802,
							"PaymentType": {
											 "AdminActive": true,
											 "Name": "Credit Card",
											 "PaymentTypeId": 1,
											 "PublicActive": true
											},
							"Status": "CC Approved"
						 }
						],
		"Phone": "123-123-1234",
		"Prefix": "Mr.",
		"Profile": null,
		"ProvState": "Colorado ",
		"Questions": [
						 {
						"Key": "Are you a Member",
						"Value": "Yes"
						 },
						 {
						"Key": "Are you an Alumni Member",
						"Value": "No"
						 },
						 {
						"Key": "Are you a Student",
						"Value": "No"
						 },
						 {
						"Key": "How did you hear about us",
						"Value": "Direct Mail"
						 },
						 {
						"Key": "I agree to the terms and conditions",
						"Value": "True"
						 }
					],
		"RegType": {
					 "Name": "Attendee Member",
					 "RegtypeUID": "d21b5256-47e7-4fa0-8375-696ead8b8534"
					},
		"Seminars": [
					 {
						"AlternateName": "Registration 101",
						"CreditType": null,
						"Description": "Course on registration basics",
						"End": "/Date(1483160400000-0500)/",
						"Image": null,
						"Location": null,
						"Name": "Introduction to Registration 101",
						"Price": 109,
						"Qty": 1,
						"SeminarUid": "17d709eb-391a-428d-bde4-b676d78ae2b8",
						"ShortName": "",
						"Start": "/Date(1404187200000-0400)/",
						"Track": null
					 },
					 {
						"AlternateName": "Onsite Registration Workshop",
						"CreditType": null,
						"Description": "Workshop covering various onsite registration solutions",
						"End": "/Date(1463227200000-0400)/",
						"Image": null,
						"Location": null,
						"Name": "Onsite Registration Workshop",
						"Price": 20,
						"Qty": 1,
						"SeminarUid": "77c6a016-c936-416f-bc29-d9a9e334fe04",
						"ShortName": "",
						"Start": "/Date(1463223600000-0400)/",
						"Track": null
					 },
					 {
						"AlternateName": "Attendee Conference Kit",
						"CreditType": null,
						"Description": "Program Kit filled with resource materials",
						"End": "/Date(1483160400000-0500)/",
						"Image": null,
						"Location": null,
						"Name": "Attendee Conference Kit",
						"Price": 15,
						"Qty": 1,
						"SeminarUid": "96fc7962-977b-4fec-9b5c-1a6efc3c5200",
						"ShortName": "",
						"Start": "/Date(1404187200000-0400)/",
						"Track": null
					 }
					],
		"Tags": [
				 {
					"Key": "Stuffed Status",
					"Value": "Not Stuffed"
				 },
				 {
					"Key": "Print Status",
					"Value": "Not Printed"
				 },
				 {
					"Key": "Present Status",
					"Value": "Not Present"
				 },
				 {
					"Key": "Mat Status",
					"Value": "Not Picked Up"
				 },
				 {
					"Key": "Active Status",
					"Value": "Active"
				 },
				 {
					"Key": "Payment Status",
					"Value": "Partial Payment"
				 },
				 {
					"Key": "Reg Status",
					"Value": "Finished"
				 },
				 {
					"Key": "Language Status",
					"Value": "English"
				 },
				 {
					"Key": "Batch",
					"Value": "Unreconciled"
				 },
				 {
					"Key": "Source",
					"Value": "Attendee"
				 }
				],
		"Title": "Sales Associate",
		"Zip": "11111"
	}
]
```
Returns a list of registants based on paging parameters.  It operates like the Export Registrants method, but with the ability to set the number of records returned and the page number.

### Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
page | string | page number on the set of records returned, the larger the page size the fewer page numbers you will need to iterate through | true
pageSize | string | the number of records returned per call | true
requirePaid | boolean | if true, only paid registrants are returned | false
requireActive | boolean | if true, only active registrants are returned | false
requireComplete | boolean | if true, only complete registrants are returned | false
startDate | string | if passed, only registrants since this date are returned | false

### Returns
A list of `Person` objects based on the size of the page and the page number.


## Get Person By ConfirmationId

> REST Request Example

``` csharp
public void GetPersonByConfirmationIdExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
    const string dataPullEndpoint = "/people/GetPersonByConfirmationId";
    string parameters = "?confirmationId=99999123";

    var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint + parameters);

    pullRequest.Method = "GET";
    pullRequest.ContentType = "application/json";
    pullRequest.KeepAlive = false;
    pullRequest.Timeout = 50000;
    pullRequest.Headers.Add("x-auth-token", token);

    var pullResponse = (HttpWebResponse)pullRequest.GetResponse();
    var reader = new StreamReader(pullResponse.GetResponseStream(), Encoding.UTF8);

    //De-serialize the JSON data into useful objects

    var ser = new DataContractJsonSerializer(typeof(Person));

    var results = (Person)ser.ReadObject(reader.BaseStream);
    //At this point results contains the person, if the confrimation Id was valid.
}
```

``` python
function getPersonByConfirmationIdExample()
{
	const token = "TOKEN GOES HERE";
	const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
	const endpoint = "/people/GetPersonByConfirmationId";

	const parameters = "?confirmationId=99999123";

	$pullRequest = curl_init(baseUrl . endpoint . parameters);
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
{
    "Address1": "987 S. Michigan Ave",
    "Address2": "Suite 1001",
    "AlternateEmail": "",
    "Association": "Streampoint Solutions",
    "BadgeID": "",
    "BadgeName": "John",
    "City": "Chicago",
    "ConfirmationNumber": "99999-123",
    "Country": "United States",
	"Demographics": null,
    "Email": "john.test@streampoint.com",
    "Fax": "",
    "FirstName": "John",
    "Guests": null,
    "LastName": "Smith",
	"Membershipcode": "",
    "PPID": "3f23427f-a093-468c-s818-19dd4cee3994",
	"Payment": null,
    "Phone": "789-456-1234",
    "Prefix": "",
    "Profile": null,
    "ProvState": "Illinois",
	"Questions": null,
    "RegType": {
				 "Name": "Student Member",
				 "RegtypeUID": "b21b55496-47e7-4fa0-8375-696ead8b8534"
				},
    "Seminars": null,
    "Title": "",
    "Zip": "11111"
}
```

Returns an individual registration record based on their confirmationId.

### Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
confirmationId | string | the registrant's confirmation ID | true

<aside class="notice">
Note: The confirmationId is in the format xxxxxx-yyy.  As a request parameter, ensure you remove the dash (i.e. 99999-123 becomes 99999123).
</aside>


### Returns
A `Person` object



