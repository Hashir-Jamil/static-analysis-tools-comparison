-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Steps to Reproduce Running the Analysis Using Coverity

---

## 1. Sign In

Sign in through GitHub at [https://scan.coverity.com/](https://scan.coverity.com/)

---

## 2. Register a GitHub Project

- From the top menu, select **"My Dashboard"** to open the My Projects page.
- Click the orange button **"+ Add Project"**.
- On the registration page:
  - Click **"Register my GitHub project"**.
  - Click **"Reload repository list from GitHub"** to refresh the list.
  - Click on the desired GitHub repository you'd like to have analyzed.

---

## 3. Fill Out Required Project Information

- Select your **role** for the project. *(You must be an Owner or Contributor.)*
- Select the **primary programming language** of the project.
- Select the **project license**. *(Must be Open Source.)*
- Leave the rest as default.
- Click **"Submit"**. Coverity will review if the project meets Open-Source requirements.

---

## 4. Download Coverity Self-Build Tool

- From the project page, click **"Submit Build"**.
- Enter the **Project Version**.
- Click the red button **"Download Coverity Scan Self-Build"** for build instructions.
- On the right-hand side, select your **OS** to download the Coverity Build Tool.
- Download and extract the ZIP file.
- Add the `bin` directory to your `PATH`.

---

## 5. Submit a Build for Analysis

- In your terminal, navigate to your project's **local build directory**.
- *(Optional)* Run any cleanup steps.
- Run the Coverity Build Tool to build your project, which will create a `cov-int` directory:

### Java (Gradle):
```sh
cov-build --dir cov-int gradlew build -x test
```

### Java (Maven):
```sh
cov-build --dir cov-int mvn -DskipTests=true compile
```

- Zip the `cov-int` folder:
```sh
zip -r myproject.zip cov-int
```
*(Or use Windows zip utility)*

- Submit this zip file in the **"Upload Tar File"** field.

---

## 6. Analysis Queue

- The project will enter a queue to be analyzed.
- You will see your place in the queue.
- An email will be sent once the analysis is complete.

---

## 7. Review Results

- The results include:
  - Lines of code analyzed
  - Number of defects found
  - Defect density
- View bugs from the **Projects Page** by clicking **"View Defects"**.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Steps to Reproduce Running the Analysis Using Snyk

---

## 1. Open the Snyk Website

Go to [https://snyk.io/](https://snyk.io/)

---

## 2. Sign In

Sign into the website using your **GitHub** account.

---

## 3. Add Projects

- Click on the **"Add Projects"** button on the Snyk Dashboard.
- Click on the **"GitHub"** option.
- This will allow access to projects linked to your GitHub account.

---

## 4. Select Repositories

- Choose the repositories from the list linked to your GitHub account.
- The repositories must be:
  - Created by your GitHub account, **or**
  - Forked to your GitHub account.
- Click on the **"Add Selected Repositories"** button after selection.

---

## 5. Wait for Project Import

- You will be redirected to the **"Projects"** page.
- Wait approximately **5 minutes** for each repository to be imported and tested.
- Confirm that each repository appears in the **"Targets"** list.

---

## 6. View Detected Issues

- After import, issues will be displayed for each repository.
- Issues are categorized by severity:
  - `C` = Critical
  - `H` = High
  - `M` = Medium
  - `L` = Low
- Click the **"..."** on the right of any repository to view its individual report (see Step 9).

---

## 7. View Individual Repository Report

- Click on a repository to view its full report.
- A dropdown will show every file where an error was found.
- Each project includes a **"Code Analysis"** file with issues in the main programming language (e.g., `.java` or `.py`).

---

## 8. Explore Issues in a File

- Click a specific file to view its issues.
- Scroll to see each issue, including:
  - **Severity** (from Step 6)
  - **Name**
  - **Priority/Severity Score**
  - **Snyk Code** (reference to Snyk Documentation)
  - **Code Snippet** (highlighting the exact issue)
  - **Description**
  - **GitHub link** to issue location
  - **Documentation link** to learn about the issue and solutions

---

## 9. Export the Report

- Return to the **"Projects"** page.
- Click the **"..."** on the right of any repository to view its report.
- A breakdown of each issue and details will be shown.
- Click **"Download CSV"** to retrieve the raw data from Snyk.
- This raw data can be used for reporting and refining data collection.

---

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Steps to Reproduce Running the Analysis Using SonarCloud

---

## 1. Create a SonarCloud Account
- Visit: [https://www.sonarsource.com/products/sonarcloud/signup/](https://www.sonarsource.com/products/sonarcloud/signup/)

## 2. Create a New Organization
- Click on **Create new organization** (top right `+`).
- Select **create one manually**.
- Enter a **Name**.
- Choose the **Free plan**.
- Click **Create Organization**.
- (Optional) Invite other users to your organization.

## 3. Create a New Project
- Click **Analyze new project** (top right `+`).
- Choose **create a project manually**.
- Enter a **Display Name**.
- Leave remaining settings as default.
- Click **Next** and then **Create Project**.

## 4. Select Language and Build Tool
- Select **Manually**.
- For **Java**: Choose `Maven` or `Gradle`.
- For **Python**: Choose `Other`.

## 5. Install SonarScanner
- Download and unzip the [SonarScanner for Linux](https://docs.sonarcloud.io/advanced-setup/ci-based-analysis/sonarscanner/).
- Add the `bin` directory to the `PATH` environment variable:
  ```bash
  export PATH=<Path to bin dir>:$PATH
  ```

## 6. Set SONAR_TOKEN Environment Variable
```bash
export SONAR_TOKEN=<token value>
```

## 7. Configure Project for Analysis

### Java (Maven)
- Update `pom.xml`:
  ```xml
  <properties>
    <sonar.organization>[organization]</sonar.organization>
    <sonar.host.url>https://sonarcloud.io</sonar.host.url>
  </properties>
  ```

### Java (Gradle)
- Update `build.gradle`:
  ```groovy
  plugins {
    id "org.sonarqube" version "4.4.1.3373"
  }

  sonar {
    properties {
      property "sonar.projectKey", "[project key]"
      property "sonar.organization", "[organization]"
      property "sonar.host.url", "https://sonarcloud.io"
    }
  }
  ```

### Python
- No configuration changes needed.

## 8. Run the Scanner

### Java (Maven)
```bash
mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar \
  -Dsonar.projectKey=<project key> \
  -DskipTests \
  -Dsonar.scm.disabled=true
```

### Java (Gradle)
```bash
./gradlew sonar
```

### Python
```bash
sonar-scanner \
  -Dsonar.organization=<organization> \
  -Dsonar.projectKey=<project key> \
  -Dsonar.sources=. \
  -Dsonar.host.url=https://sonarcloud.io
```

## 9. Troubleshooting
- If errors occur, check:
  - Java JDK versions
  - Required plugins for Java projects

## 10. View Results
- Wait for the analysis to complete.
- Results will appear on the SonarCloud dashboard for the project.

## 11. Export Issue Results via API
- Use the [SonarCloud Web API](https://sonarcloud.io/web_api/api/issues/search?deprecated=false&section=params):
  ```
  https://sonarcloud.io/api/issues/search?componentKeys=<PROJECT_KEY>&ps=<TOTAL_ISSUES>&access_token=<PERSONAL_TOKEN>
  ```
  - **PROJECT_KEY**: Project name (from dashboard info tab)
  - **TOTAL_ISSUES**: Total number of security + reliability issues
  - **PERSONAL_TOKEN**: Your SonarCloud token

- Perform **5 separate GET requests** per scanned project to get all issues as a JSON list.
