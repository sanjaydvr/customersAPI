# customersAPI
Customers API


Design Considerations

Customers API is designed to have minimum set of fields to complete a set of business functionlaties within customer domain and that can run on its
own independently.

Current design and implementation supports for the below mentioned business funcationlities

Common attributes to all the resources and its methods are:
  - api-request-id is required as mandatory header field for NFR specs that could be applied on to API Calls
  - implemented set of error handling just to demonstrate the error handling design spec and binding that onto run time without 
        a single of coding to handle errors and that could be extended for custom implementation.
  - common error model is defined and bind to each resource and its operations on the spec.
  
1.  Create new customer via POST call with the specific schema as payload defined in API specification customer.raml
      - Customer type defined on API specification is required in request body, without which API would throw error
            
2.  Retrieve multiple customer information through GET call by providing limit and Start query parametersquer
      - optional query parameters like, limit(number of items in the result) and start index of the respose contents to implement pagination
        retrieval operation.
      - sample link model on errorModel has been defined and could be extended onto other types(specially for retrieval operations) to include
        reference for previous, current and next available response contents.
       -if no limit and start query parameters are not supplied, then design spec has been defaulted to 1 for both the parameters.
       
3.  Retrieve single customer by providing {customerid} path parameters    
4.  Update single customer by providing {customerid} path parameters
5.  Delete a customer by providing {customerid} path parameters.
