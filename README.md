# API Automation Testing
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
![Screenshot 2024-11-19 091419](https://github.com/user-attachments/assets/7dade5e8-2134-4c6b-95fd-9bb975f13827)

```
// Status Code Validation
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
    console.log("Status code is 200");
});

//Request Body Validation
pm.test("Request body validation", function () {
    let requestBody = pm.request.body.raw ? JSON.parse(pm.request.body.raw) : {};
    pm.expect(requestBody).to.have.property("id").that.is.a("number");
    pm.expect(requestBody).to.have.property("first_name").that.is.a("string").and.not.empty;
    pm.expect(requestBody).to.have.property("middle_name").that.is.a("string"); // Can be empty
    pm.expect(requestBody).to.have.property("last_name").that.is.a("string").and.not.empty;
    pm.expect(requestBody).to.have.property("date_of_birth").that.is.a("string").and.match(/^\d{2}-\d{2}-\d{4}$/);

    console.log("Request body is valid");
});

// Response Body Validation
pm.test("Response body validation", function () {
    const responseBody = pm.response.json();
    
    pm.expect(responseBody).to.have.property("id").that.is.a("number");
    pm.expect(responseBody).to.have.property("first_name").that.is.a("string").and.not.empty;
    pm.expect(responseBody).to.have.property("middle_name").that.is.a("string"); 
    pm.expect(responseBody).to.have.property("last_name").that.is.a("string").and.not.empty;
    pm.expect(responseBody).to.have.property("date_of_birth").that.is.a("string").and.match(/^\d{2}-\d{2}-\d{4}$/);

    console.log("Response body is valid");
});
```

# Negative Test cases
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
# Why use console.log() in Postman
In Postman, console.log() is used in scripts (Pre-request or Tests) to print messages or variable values to the Postman Console. It is a helpful tool for debugging, inspecting variables, and understanding the flow of your requests and responses. To view the output from console.log() in Postman, you need to open the Postman Console.
![Screenshot 2024-11-19 000454](https://github.com/user-attachments/assets/89379fd8-3365-4f9d-9d1f-2eb0ffbc9717)

# Running Tests
Run Tests in Postman
* Select the collection and click Run to execute the tests.
![Screenshot 2024-11-19 102136](https://github.com/user-attachments/assets/f9c16e39-3d75-496f-88ad-4c8ce4b9010f)
![Screenshot 2024-11-19 102219](https://github.com/user-attachments/assets/d8178e22-4523-4a24-9dbb-07393e038526)

Run Tests Using Newman
* Install Newman globally using npm:
```
npm install -g newman
```
* Open Postman and export the collection file (e.g., Api-Automation-Tests.postman_collection.json)
* Run the tests using the following command:
```
newman run Api-Automation-Testing.postman_collection.json
```
![Screenshot 2024-11-19 101925](https://github.com/user-attachments/assets/2eb5acb7-29a5-474b-9844-76710415715a)

# Monitors in Postman
* Set a timer to run all requests automatically every X hours/days/weeks
* Receive emails automatically for every error/failure in the tests.
* Automatically retest X times if a test fails.
* Set a maximum timeout for requests.
![Screenshot 2024-11-19 102817](https://github.com/user-attachments/assets/cc8e1f29-6899-41f0-9c6e-d40d1aff53d5)
![Screenshot 2024-11-19 103254](https://github.com/user-attachments/assets/5ede78aa-21ed-48d8-88f7-5cd23325bda8)
![Screenshot 2024-11-19 103224](https://github.com/user-attachments/assets/512fcccc-ddff-4426-b7a3-d210c7bab660)

# Automate with CI/CD
Integrate Jenkins with Postman
You can integrate Jenkins with Postman for automating API testing. This setup allows you to run Postman collections as part of a CI/CD pipeline.
* Open Postman and export the collection you want to test.
* Login to Jenkins.
* Click 'New Item' > name the project, and select "Freestyle Project"
* Then configure the Job, Under 'Build Steps', select Execute Windows batch command" (Windows).
* Add a script to execute the Postman collection using Newman.
![Screenshot 2024-11-19 104545](https://github.com/user-attachments/assets/4fb1e1c2-a110-4aa0-9ddd-691750c3f64c)

Integrate Jenkins with Postman
Integrating GitHub Actions with Postman allows you to automate the testing of your APIs directly from your GitHub repository.
* Create a GitHub Actions Workflow.
* Create a new file (e.g., postman.yml)
* Copy the YAML content from  Postman CLI Configuration page to set up the workflow
* Monitor the workflow execution under the Actions tab in your GitHub repository
![1](https://github.com/user-attachments/assets/ece4d90f-a803-4a92-a72a-55af95525a5a)
![2](https://github.com/user-attachments/assets/185f5a81-819e-4fc1-8409-2eb4733cc664)
![3](https://github.com/user-attachments/assets/c7a4194d-2498-4518-89bc-095ac97c214e)
![4](https://github.com/user-attachments/assets/fa1cae00-725c-43d3-9909-f400314829c8)
![5](https://github.com/user-attachments/assets/ffe318d4-4014-477c-8cd5-84bc810c0ec0)
