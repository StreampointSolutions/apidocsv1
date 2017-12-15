# API Reference

API Text Goes Here

## Country

This is an object that represents the country information that is found in the registrant's contact information.

### Properties

Field | Type | Description
------| ---- | -----------
Code | string | Country Abbreviation
CountryID | integer | Unique Identifier
Name | string | Country Full Name
Order | integer | Country list is sorted using the order number

### Get List of Countries

> REST Example

``` csharp
public void GetCountryListExample()
{
    const string token = "TOKEN GOES HERE";
    const string baseUrl = "https://apirest.streampoint.com/v1/Personal.svc";
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

> The above command returns JSON structured like this:

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

> SOAP Example

``` csharp
public void GetCountryListExample()
{
    const string username = "Username";
    const string password = "Password";
    const string eventid = "Event Guid";

    var psc = new PersonalServiceClient();
    psc.ClientCredentials.UserName.UserName = eventid + "^" + username;
    psc.ClientCredentials.UserName.Password = password;

    Country[] countries = psc.GetCountryList();
}

```

Returns a list of all countries applicable to the event.


## Exhibitor

The exhibitor objects allow you to retrieve information associated with an exhibitor registration's details.  You can access their company contact information, their booth details and which industry category they belong to.

### Exhibitor Object

#### Properties

Field | Type | Description
------| ---- | -----------
Address1 | string | Address 1
Address2 | integer | Address 2
BoothNumber | string | booth number or booth code on the show floor
Category | string | exhibitor category Name
City | string | city of the exhibiting company
Country | string | country of the exhibiting company
Description | string | exhibiting company Description
Email | string | exhibiting company's main contact email
ExUID | guid | unique identifier of the exhibitor
Facebook | string | link to company's Facebook site
ImageUID | string | unique id for company logo file
LinkedIn | string | link to company's LinkedIn profile
Name | string | exhibiting company name
Phone | string | company phone number
Sponsor | boolean | indicates if exhibitor is also a sponsor
State | string | state or province of the exhibiting company
Twitter | string | company Twitter handle
Website | string | company website


### Get Exhibitors 

Returns a list of exhibitors, optionally filtered by passed parameters.

####Request Parameters
Field | Type | Description | Required
------|------|-------------|---------
searchNameNum | string | filter exhibitors by searching by name or number for passed value | false
searchDesc | string | filter exhibitors by searching description for passed value | false
category | string | category to filter exhibitors by, see GetExhibitorCategories() | false
provStateID | integer | province or state to filter exhibitors by, see GetProvStateList(Int32) | false
countryID | integer | Country to filter exhibitors by, see GetCountryList() | false
sponsor | boolean | If true only returns 'sponsor' exhibitors | false
startLetter | string | Filter based on the first letter of name | false

## Person
## Payment
## Seminar
## Speaker
## State / Province
