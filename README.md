# API Sample Test

## Getting Started

This project requires a newer version of Node. Don't forget to install the NPM packages afterwards.

You should change the name of the ```.env.example``` file to ```.env```.

Run ```node app.js``` to get things started. Hopefully the project should start without any errors.

## Explanations

The actual task will be explained separately.

This is a very simple project that pulls data from HubSpot's CRM API. It pulls and processes company and contact data from HubSpot but does not insert it into the database.

In HubSpot, contacts can be part of companies. HubSpot calls this relationship an association. That is, a contact has an association with a company. We make a separate call when processing contacts to fetch this association data.

The Domain model is a record signifying a HockeyStack customer. You shouldn't worry about the actual implementation of it. The only important property is the ```hubspot```object in ```integrations```. This is how we know which HubSpot instance to connect to.

The implementation of the server and the ```server.js``` is not important for this project.

Every data source in this project was created for test purposes. If any request takes more than 5 seconds to execute, there is something wrong with the implementation.

## Debrief on Current Implementation

### 1. Documentation and References
The project lacks detailed documentation regarding the API being integrated. To improve clarity and assist future developers, it's recommended to:
- Include references to the relevant API documentation.
- Example: [HubSpot API Documentation](https://developers.hubspot.com/beta-docs/guides/api/crm/associations/associations-v3#retrieve-associations).

---

### 2. Testing Database
- The testing database does not provide a robust environment for validating functionality.  
- The API is only returning older contact data, with no recent entries available.
- This limitation makes it difficult to test and validate features thoroughly.
- Populate the database with recent and diverse data would facilitate comprehensive testing.

---

## 3. Endpoint Issues
The `/crm/v3/associations/MEETINGS/CONTACTS/batch/read` endpoint is not returning associated contacts.  
- The endpoint appears to be configured correctly based on the documentation (https://developers.hubspot.com/beta-docs/guides/api/crm/associations/associations-v3#retrieve-associations).
- The lack of results might be related to the testing database not containing recent data.

---

## 4. Further Investigation
To ensure full functionality:
- Perform a deeper analysis of the integrated API.
- Test all endpoints with a properly populated testing environment containing recent data.

---

## 5. Transition to TypeScript
Switching from JavaScript to TypeScript is recommended to:
- Improve type safety.
- Enhance code organization.
- Reduce the likelihood of runtime errors.

---

## 6. Scaling Considerations
- Implement a **message broker** system (e.g., RabbitMQ, Kafka) to enable parallel processing.
- This will allow the service to efficiently handle large batches of data while maintaining performance.

---

## 7. Enhanced Logging System
The current logging system could be upgraded to provide better observability.  
- Integrate with tools like **Datadog** to:
  - Improve visibility into service operations.
  - Identify and debug issues faster.
  - Monitor performance metrics in real-time.
