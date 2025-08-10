#  Postman & Newman for API Testing

## Overview
**Postman** is a popular API testing tool that allows developers and QA engineers to test, document, and automate REST, SOAP, and GraphQL APIs.  
**Newman** is the command-line companion for Postman, enabling you to run Postman collections in CI/CD pipelines or automated environments.

---

## 1️⃣ Postman – Manual API Testing

### Key Features
- **User-Friendly Interface** – Create and organize API requests visually.
- **Supports Multiple Methods** – GET, POST, PUT, DELETE, PATCH, etc.
- **Environment Management** – Store and reuse variables.
- **Pre-Request & Test Scripts** – Add JavaScript code to run before or after requests.
- **Collection Runner** – Execute multiple requests in sequence.
- **Data-Driven Testing** – Run collections with external data (CSV/JSON).
- **Built-in Documentation** – Share API documentation with teams.

---

### Example: Creating a POST Request in Postman
1. Open Postman and click **New → HTTP Request**.
2. Choose **POST** method.
3. Set URL:  
   ```
   https://reqres.in/api/users
   ```
4. Add request body (JSON):
```json
{
  "name": "John Doe",
  "job": "QA Engineer"
}
```
5. Click **Send**.
6. Validate the response status `201 Created` and body.

---

### Example Test Script in Postman
```javascript
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});

pm.test("Name is correct", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql("John Doe");
});
```

---

## 2️⃣ Newman – CLI Runner for Postman Collections

### Why Use Newman?
- Run Postman collections without opening the Postman GUI.
- Perfect for **CI/CD integration** (Jenkins, GitHub Actions, GitLab CI).
- Supports **report generation** (HTML, JSON, CLI output).
- Works well with **data files** for data-driven testing.

---

### Installation
```bash
npm install -g newman
```

---

### Running a Collection
Export your collection from Postman (JSON format), then run:
```bash
newman run MyCollection.json
```

---

### Running with an Environment
```bash
newman run MyCollection.json -e MyEnvironment.json
```

---

### Data-Driven Testing with Newman
```bash
newman run MyCollection.json -d data.csv
```
Where `data.csv` might contain:
```csv
name,job
John,Tester
Alice,Developer
```

---

### Generating Reports
Install HTML reporter:
```bash
npm install -g newman-reporter-htmlextra
```
Run with HTML report:
```bash
newman run MyCollection.json -r htmlextra
```

---

## 3️⃣ Best Practices
- Use **environment variables** for URLs and authentication tokens.
- Keep collections organized in folders.
- Version control your Postman collections and environments in GitHub.
- Use **Pre-request scripts** for dynamic token generation.
- Validate both **status codes** and **response bodies** in your tests.
- Integrate Newman runs into your CI/CD pipeline for automated API checks.

---

## 📚 Resources
- [Postman Official Site](https://www.postman.com/)
- [Newman Documentation](https://github.com/postmanlabs/newman)
- [Postman Learning Center](https://learning.postman.com/)

---

💡 **Tip of the Day**:  
_"Manual API testing in Postman is great for exploration, but integrating Newman ensures those tests run automatically in every build."_  
