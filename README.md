# API-Automation-Testing
This repository contains a collection of automated API test scripts written to ensure the robustness of API endpoints. It includes tests for various HTTP methods such as GET, POST, PUT, and DELETE, focusing on validating response codes, body content, headers, and performance.
Postman collection created based on - https://thetestingworldapi.com/Help

# Technologies Used
* Postman: For writing and managing API tests.
* Newman: CLI tool to run Postman collections and integrate them into CI/CD pipelines.
* JavaScript (optional): For writing scripts to validate responses and handle dynamic data.
* CI/CD Integration (optional): Tools like Jenkins for continuous testing.

# Install Newman
 Install Newman globally using npm:
```
npm install -g newman
```
# Test Cases
This repository includes tests for the following scenarios:
* GET: Verifying if the endpoint returns the correct data.
* POST: Ensuring data is correctly created on the server.
* PUT: Testing updates to existing resources.
* DELETE: Ensuring resources can be deleted successfully.

Test cases
![Image 2](https://github.com/user-attachments/assets/28779a36-9242-49b6-9429-37835a1fc4ba)

Negative Tests: Handling invalid inputs and ensuring correct error codes are returned.
![image 1](https://github.com/user-attachments/assets/ddca5151-2090-47e2-bc4e-869bbf7216c9)  

# Running Tests
Run Tests in Postman
* Open Postman and load the collection file (e.g., API-Automation-Tests.postman_collection.json).
* Select the collection and click Run to execute the tests.

Run Tests Using Newman
* After cloning the repo, navigate to the folder containing the collection file.
* Run the tests using the following command:
```
newman run Api-Automation-Testing.postman_collection.json
```

# Monitors in Postman
* Set a timer to run all requests automatically every X hours/days/weeks
* Receive emails automatically for every error/failure in the tests.
* Automatically retest X times if a test fails.
* Set a maximum timeout for requests.


