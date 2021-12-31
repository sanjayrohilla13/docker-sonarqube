# docker-sonarqube
This repo is for running the SonarQube 9.2.4 in Docker Container
Initial requirements
    Because SonarQube uses an embedded Elasticsearch, make sure that your Docker host configuration complies with the Elasticsearch production mode requirements and File Descriptors configuration
        a. Run the below commands in the host machine
            sysctl -w vm.max_map_count=262144
            sysctl -w fs.file-max=65536
            ulimit -n 65536
            ulimit -u 4096
        b. Check the postgresql version supported by the required sonarqube version.
            In our case for SonarQube 9.2.4, postgres 12 is supported
        c. seccomp_profile.json file for security options

Running the Sonarqube cluster
    1. Bring up the service
        a. move in to the directory where the docker-compose.yml file is stored and run the below command:
            docker-compose up -d
    2. Checking logs for the service 
            docker-compose logs --follow
            * It will show the logs as and when they are generated.
            * Ctrl+c can be used to come out  of the logging mode.
    3. Bring down the service
        a. move in to the directory where the docker-compose.yml file is stored and run the below command:
            docker-compose down
    4. Accessing the SonarQube Service
        http://localhost:9000
    
Scanning the code
    1. Open the SonarQube Service with http://localhost:9000 or http://ipaddress:9000
    2. Create a project and a key using manually option -> Entering the Project Display  
       name and Project Key -> Setup
        
    How do you want to analyze your repository?
    1. Select Local
    2. Enter a Generate a token by entering a name for the token
        Enter <sanjay> -> click generate -> save this token 
        1367d39943ac34850b8826f00b8932956704d74a 
    3. Click continue
    4. Select your project type for running the analysis on your project
        e.g. Maven, Gradle, .NET, Other
    5. Select your os from where you are triggering your analysis
        e.g. Linux, Windows and MacOS
        <Linux>
        a. Download and unzip the Scanner for Linux
        Visit the https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/ for downloading the latest version of Scanner, and add the bin directory to the PATH environment variable

        b. Execute the Scanner
        Running a SonarQube analysis is straighforward. You just need to execute the following commands in your project's folder.
        sonar-scanner \
        -Dsonar.projectKey=Project-1 \
        -Dsonar.sources=. \
        -Dsonar.host.url=http://192.168.1.108:9000 \
        -Dsonar.login=1367d39943ac34850b8826f00b8932956704d74a

        c. If your analysis is successful, this page will automatically refresh in a few moments.

        d. We can see our results on the Sonarqube portal
        <Windows>
        a. Download and unzip the Scanner for Windows
        Visit the https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/ for downloading the latest version of Scanner, and and add the bin directory to the %PATH% environment variable

        b. Execute the Scanner
        Running a SonarQube analysis is straighforward. You just need to execute the following commands in your project's folder.
        sonar-scanner.bat -D"sonar.projectKey=Project-1" -D"sonar.sources=." -D"sonar.host.url=http://192.168.1.108:9000" -D"sonar.login=1367d39943ac34850b8826f00b8932956704d74a"

        c. If your analysis is successful, this page will automatically refresh in a few moments.

        d. We can see our results on the Sonarqube portal        


