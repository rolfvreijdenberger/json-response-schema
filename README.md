# jsend-json-schema
Json-schema(s) and extended schemas for the JSend format for structured json responses for applications. 

The JSend specification can be found at https://labs.omniti.com/labs/jsend/wiki

from the jsend page: "Put simply, JSend is a specification that lays down some rules for how JSON responses from web servers should be formatted. JSend focuses on application-level (as opposed to protocol- or transport-level) messaging which makes it ideal for use in REST-style applications and APIs."

This repository also contains an extension on the JSend format to address the lack of structure and information in the response data with status 'fail'. Specifically, it specifies an array of objects containing at least a 'message' key and an optional 'code' and 'field' key. More information can be found in the schema itself. 


example of extended format
```json
{
  "status": "fail",
  "data": [
    {
      "message": "invalid combination of postcode huisnummer",
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
'''

