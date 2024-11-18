# API-Automation-Testing
This repository contains a collection of automated API test scripts written to ensure the robustness of API endpoints. It includes tests for various HTTP methods such as GET, POST, PUT, and DELETE, focusing on validating response codes, body content, headers, and performance.
Postman collection created based on - https://thetestingworldapi.com/Help

# Technologies Used
* Postman: For writing and managing API tests.
* Newman: CLI tool to run Postman collections and integrate them into CI/CD pipelines.
* JavaScript (optional): For writing scripts to validate responses and handle dynamic data.
* CI/CD Integration (optional): Tools like Jenkins for continuous testing.

# Creating your first requests in Postman
This repository includes tests for the following scenarios:
* GET: Verifying if the endpoint returns the correct data.
* POST: Ensuring data is correctly created on the server.
* PUT: Testing updates to existing resources.
* DELETE: Ensuring resources can be deleted successfully.
  
![image 1](https://github.com/user-attachments/assets/ddca5151-2090-47e2-bc4e-869bbf7216c9)

# Positive Test cases
![Image 2](https://github.com/user-attachments/assets/28779a36-9242-49b6-9429-37835a1fc4ba)

# Negative Test casess
To test negative scenarios, you should use invalid or unexpected inputs, such as:
* Invalid endpoint: A non-existent or wrong URL path.
* Invalid headers: Missing or incorrect headers, such as Authorization or Content-Type.
* Invalid request body: Send malformed or incomplete JSON or XML data.
* Invalid query parameters: Incorrect or missing required parameters.
* Invalid authentication: Incorrect or expired tokens for APIs that require authentication.

![Screenshot 2024-11-18 235516](https://github.com/user-attachments/assets/6e6e0edb-0fc1-480d-9c47-3984f65e80dd)

Validate Response Code
Ensure that the response code matches the expected error status. Common HTTP status codes for negative tests include:
* 400 Bad Request: The server cannot process the request due to client error (e.g., invalid data).
* 401 Unauthorized: The client lacks valid authentication credentials.
* 403 Forbidden: The client does not have permission to access the resource.
* 404 Not Found: The endpoint or resource does not exist.
* 500 Internal Server Error: A general server-side error (often indicates unhandled cases).

Write Tests in Postman
```
pm.test("Status code is 500", function () {
    pm.response.to.have.status(500);
});

pm.test("Validate status code string", function () {
    pm.response.to.have.status("Internal Server Error");
});

pm.test("Validate the Error message", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.Message).to.eql("An error has occurred.");
});
```

# Running Tests
Run Tests in Postman
* Open Postman and load the collection file (e.g., API-Automation-Tests.postman_collection.json).
* Select the collection and click Run to execute the tests.

Run Tests Using Newman
* Install Newman globally using npm:
```
npm install -g newman
```
* Run the tests using the following command:
```
newman run Api-Automation-Testing.postman_collection.json
```

# Monitors in Postman
* Set a timer to run all requests automatically every X hours/days/weeks
* Receive emails automatically for every error/failure in the tests.
* Automatically retest X times if a test fails.
* Set a maximum timeout for requests.


