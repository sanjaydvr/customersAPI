# Customers API
Customers API


Design Considerations

Customers API is designed to have minimum set of fields to complete a set of business functionlaties within customer domain and that can run on its own independently.

Current design and implementation supports for the below mentioned business funcationlities

Common attributes to all the resources and its methods are:
  - api-request-id is required as mandatory header field for NFR specs that could be applied on to API Calls
  - implemented set of error handling just to demonstrate the error handling design spec and binding that onto run time without 
        a single of coding to handle errors and that could be extended for custom implementation.
  - common error model is defined and bind to each resource and its operations on the spec.
  - Basic Authentication is considered as security schemes(just to cover security aspects of the design, However we could add any
    standards available or extend to include custome security features)
  
1.  Create new customer via POST call with the specific schema as payload defined in API specification customer.raml
      - Customer type defined on API specification is required in request body, without which API would throw error
            
2.  Retrieve multiple customer information through GET call by providing limit and Start query parametersquer
      - optional query parameters like, limit(number of items in the result) and start index of the respose contents to implement               pagination retrieval operation.
      - sample link model on errorModel has been defined and could be extended onto other types(specially for retrieval operations) to            include reference for previous, current and next available response contents.
      - if no limit and start query parameters are not supplied, then design spec has been defaulted to 1 for both the parameters.
       
3.  Retrieve single customer by providing {customerid} path parameters    
4.  Update single customer by providing {customerid} path parameters
5.  Delete a customer by providing {customerid} path parameters.

Consumer usecase:

1. A consumer may periodically (every 5 minutes) consume the API to enable it (the consumer) to maintain a copy of the provider API's customers (the API represents the system of record)
    - We could apply Rate limiting policy on the API which is bind to specific client id or apiKey(in my case) to limit the number of       calls that are allowed to consume on this API. However I have implemented such policies on Apigee, but not implemented on Mule           specailly on API RAML specificaiton( I would definitely try to explore this given some time).
 
2. A mobile application used by customer service representatives that uses the API to retrieve and update the customers details
    - We could restrict the payload size and query parameters to handle less data volume across the network by adding policies around         JSON content validations and setting up different SLA for client id or apiKey which has provided to mobile consumers.


3. Simple extension of the API to support future resources such as orders and products
    - CustomersAPI specification has Order type defined and is not consumed on any of the operations and could be included in the             Customer type as an optional field so that we could extend customer object to have order details embedded within it.
    - We could make use of LinkModel to explicitley relate Customer and Order entities seperatley if required.
    - We could add new paths to the existing customer api to provide explicit access to orders which are related to customer through           relationhip features.

interesting' design decisions
  - Use of links(not done on all operatins on my version of deliverable) on each operation to implement/indicate/suggest consuming          applications about possible state navigations/transitions on resources and its relationships.
  - Implementation of the each operations on each path could be implemented on seperate flows on Anypoint studio so that any change to      specification can have minimum code change on the existing implementation.
  

NOTE: API implementation is using hard coded response for demonstration purpose.
