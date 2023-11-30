pipeline {
    agent any
    triggers {
    pollSCM('* * * * *')
    }
    
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
stage("Analyse statique du code") {
      steps {
           sh "./gradlew checkstyleMain"
           publishHTML (target: [
           reportDir: 'build/reports/checkstyle/',
           reportFiles: 'main.html',
           reportName: "Checkstyle Report"
])
           }
        }
    }
   post {
        always {
            emailext (
                subject: "Notification de construction Jenkins",
                body: "La construction Jenkins est ${currentBuild.result}",
                to: "majidlearning7@gmail.com",
            )
        }
    }             
}
