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

