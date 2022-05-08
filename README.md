# Mulesoft Tracing Module Integration
Tracing module enables you to enhance your logs by adding, removing, and clearing all variables from the logging context for a given Mule event. It also enables you to modify the correlation ID during flow execution.
# Uses Of Tracing Module
* Clear all the logging variables from the event logging context.
* Remove a logging variable from logging context.
* Set logging variables to logging context.
* Modify the correlation ID during flow execution

# Steps to run application
 * Clone the repo
 * Run the application
 * Hit the below curl and verify the logs. 
 ```bash
curl --location --request POST 'http://localhost:8081/trace' \
--header 'Content-Type: application/json' \
--data-raw '{
    "orderId": 548102842,
    "customerId": "ARG-12934",
    "items": [
        "CP-123",
        "CP-452"
    ]
}'
```
 
