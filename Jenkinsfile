node('docker'){
  stage('Poll'){
    checkout sum
  }
  stage('Build&Unit test'){
    sh 'mvn clean verify -DskipITs=true';
    junit '**/target/surfire-reports/TEST-*.xml';
    archive 'target/*.jar'
  }
  stage('Static Code Analysis'){
    sh 'mvn clean verify sonar:sonar -Dsonar.projectName=example-project-Dsonar.projectkey=example-project -Dsonar.projectVersion=$BUILD_NUMBER';
  }
  stage('Integration Test'){
    sh 'mvn clean verify Dsurefire.skip=true';
    junit '**/target/faildafe-reports/TEST-*.xml'
    archive 'target/*.jar'
  }
  stage('Publish'){
    def server = Artifactory.sever 'Default Atrtifactory Server'
    def uploadSpec = """{
      "files":[
      {
        "pattern": "target/hellow-0.0.1.war",
        "target":"example-project/${BUILD_NUMBER}/",
        "props":"Integration-Tested=Yes;Performance-Tested=No"
       }
      ]
    }"""
    server.upload(uploadSpec)
  }
}

        
      
      
      sh 'mvn clean verify Dsurefire.skip=true';
    junit '**/target/faildafe-reports/TEST-*.xml'
    archive 'target/*.jar'
  }
  
  
}
