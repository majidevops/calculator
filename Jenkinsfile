pipeline {
    agent any
    stages {
        
        stage("Compilation") {
            steps {
                sh "./gradlew compileJava"
                
            }
            
        }
        stage("test unitaire") {
steps {
sh "./gradlew test"
}
}
        stage("Code coverage") {
              steps {
                  sh "./gradlew jacocoTestReport"
               publishHTML (target: [
reportDir: 'build/reports/jacoco/test/html',
reportFiles: 'index.html',
reportName: "JaCoCo Report"
])
sh "./gradlew jacocoTestCoverageVerification"
}
}
stage("Static code analysis") {
      steps {
           sh "./gradlew checkstyleMain"
           }
        }
    }
                
}
