## To post a new employee

`$ curl -X POST localhost:8080/employees -H 'Content-type:application/json' -d '{"name": "Samwise Gamgee", "role": "gardener"}'`

## To alter the user

`$ curl -X PUT localhost:8080/employees/3 -H 'Content-type:application/json' -d '{"name": "Samwise Gamgee", "role": "ring bearer"}'`

## To delete the user

`curl -X DELETE localhost:8080/employees/3`

This by itself is not restful. 


```
I am getting frustrated by the number of people calling 
any HTTP-based interface a REST API. 
Today’s example is the SocialSite REST API.
That is RPC (Remote Procedure Call).
It screams RPC. 
There is so much coupling on display that it should be given an X rating.

What needs to be done to make the REST architectural style clear 
on the notion that hypertext is a constraint? 
In other words, if the engine of application state (and hence the API) 
is not being driven by hypertext, then it cannot be RESTful 
and cannot be a REST API. 
Period. 
Is there some broken manual somewhere that needs to be fixed?
```

It must be self-describing - HATEOAS. 

Then need to change the return types from `Employee` to `Resource<Employee>`

Rules of REST:

- You can always add columns to a database, but never take away. This will ensure you don't break clients.
    - i.e. if we want to split `name` into `firstName` and `lastName` - leave `name` in there!
    - We can use the `firstName` and `lastName` from the database to construct the `name`.
    
```$xslt
{
  "id": 1,
  "firstName": "Bilbo",
  "lastName": "Baggins",
  "role": "burglar",
  "name": "Bilbo Baggins",
  "_links": {
    "self": {
      "href": "http://localhost:8080/employees/1"
    },
    "employees": {
      "href": "http://localhost:8080/employees"
    }
  }
}
```    

## Use HATEOUS to decouple state-based actions from the payload of the data.

Pass valid links, rather than the data itself. I'e instead of handing IN_PROGRESS, handle
enum the options available to anything IN_PROGRESS - like Cancel or Complete.

This naturally reduces coupling between client and server..

 


    
