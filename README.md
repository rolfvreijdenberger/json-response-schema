# jsend-json-schema
Json-schema(s) and extended schemas for the JSend format for structured json responses for applications. 

This repository also contains an extension on the JSend format to address the lack of structure and information in the response data with status 'fail'. Specifically, it specifies an array of objects containing at least a 'message' key and an optional 'code' and 'field' key. More information can be found in the schema jsend-extend-json-schema.json. 

This repository also contains a non-JSend related schema for RESTful responses for failed/error responses. REST architecture is about getting resources. JSEND actually does not send a resource back in case of 'status':'succes', but an envelope around a resource, by enforcing it to be wrapped in a 'data' key. 
API's should specify how they return their resource itself without an imposed structure. Therefore, it makes more sense to use a structured response for failures/errors only, and have the [HTTP status code specify a succes(200)](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#2xx_Success), [failure (which is a client error 4xx)](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#4xx_Client_Error) or [error(which is a server error 5xx)](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#5xx_Server_Error). More information can be found in the schema rest-fail-response-json-schema.json. 

Client code can iterate over the array to:
- aggregate the messages for display to a user or debugging
- check if there is a mapping for input fields, making a smart GUI or widget possible (validation)
- check if there are codes, which could be used for translations or mappings to text that can be presented to a user


The JSend specification can be found at https://labs.omniti.com/labs/jsend/wiki

from the jsend page: "Put simply, JSend is a specification that lays down some rules for how JSON responses from web servers should be formatted. JSend focuses on application-level (as opposed to protocol- or transport-level) messaging which makes it ideal for use in REST-style applications and APIs."

example of extended format for JSEND.
```json
{
  "status": "fail",
  "data": [
    {
      "message": "invalid combination of postalcode/housenumber",
      "code": 123
    },
    {
      "message": "I did not like your input header"
    },
    {
      "message": "could not authenticate for user 'zorro'",
      "code": 1
    },
    {
      "message": "telephone number does not have ten digits",
      "code": "1123",
      "field": "mobile_phone"
    },
    {
      "message": "telephone number does not have ten digits",
      "code": "1123",
      "field": "customer.postal_address.mobile_phone"
    }
  ]
}
```

example for the RESTful schema for failures only
```json
{
  "messages": [
    {
      "message": "telephone number does not have 10 digits",
      "field": "telephone_number"
    },
    {
      "message": "telephone number does not have 10 digits",
      "field": "customer.postal_address.telephone_number",
      "code": 123
    },
    {
      "message": "invalid headers sent"
    },
    {
      "message": "handling node: 10.0.0.1",
      "type": "debug"
    }
  ]
}
```

