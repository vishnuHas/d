trigger:
- main

pool:
  name: agentpool  # Use your actual agent pool name here

steps:
# Step 1: Checkout code
- checkout: self
  displayName: 'Checkout code'

# Step 2: Build and run unit tests
- script: mvn clean test
  displayName: 'Build and run unit tests'

# Step 3: Publish test results
- task: PublishTestResults@2
  inputs:
    testResultsFiles: '**/target/surefire-reports/TEST-*.xml'
    testResultsFormat: 'JUnit'
    failTaskOnMissingResultsFile: true
  displayName: 'Publish Maven test results'


net stop w32time
taskkill /f /im w32time.dll
net start w32time
w32tm /config /manualpeerlist:"time.windows.com,0x1" /syncfromflags:manual /reliable:YES /update
w32tm /resync
