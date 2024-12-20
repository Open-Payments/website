# Messages API
[![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Open-Payments/messages-api)

The Messages API is designed to parse and validate financial payment messages. This API supports the FedNow & ISO20022 format, applying validation rules from the official XSD schema files. The API is available for both public and private use, with a ready-to-deploy Docker image available on Docker Hub.

- **Repository**: [Open Payments Messages API](https://github.com/Open-Payments/messages-api)
- **API Documentation**: [Postman Collection](https://www.postman.com/openpaymentsapi/open-payments/overview)

---

## API Endpoint:

`POST /validate`

## Description:

This endpoint accepts an XML payment message, identifies the message format (e.g., pacs.008, pacs.009), and performs the following actions:
1. **Parsing**: Converts the XML payment message into an internal object model.
2. **Validation**: Applies schema-based validation using the FedNow XSD files.
3. **Response**: Converts the parsed message into a JSON object and returns it as the API response.

---
#### **Additional Features:**

- **Automatic Format Detection**: The API identifies the message type automatically, so no need to specify the format in the request.
- **XSD Validation**: Applies validation rules as defined by the FedNow XSD files.
- **JSON Conversion**: Converts valid XML messages to JSON format, making it easier to consume by modern applications.

---

### API Documentation and Try Out
Explore the full API documentation and **try out the Validate API** using the Postman Collection. Postman allows you to test the API directly in your browser:

- **Postman Collection**: [Open Payments Postman Collection](https://www.postman.com/openpaymentsapi/open-payments/overview)
- **Try it out**: You can use Postman’s “Run in Postman” button to directly test the API instance and see how it works with real data.

---