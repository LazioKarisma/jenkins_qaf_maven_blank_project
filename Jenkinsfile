pipeline {
    agent any
  
  	tools { 
        maven 'maven-3.8.1'
        jdk 'jdk8' 
    }

    stages {
        stage('Build') {
            steps {
                // To run Maven on a Windows agent, use
                 bat 'mvn clean test'
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    //junit '**/target/surefire-reports/TEST-*.xml'
                    //archiveArtifacts 'target/*.jar'
					echo 'success'
					
			archiveArtifacts artifacts: 'dashboard.htm', onlyIfSuccessful: true
								
			emailext attachLog: true, attachmentsPattern: 'dashboard.htm',
			subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
          to: 'lazio_karisma@manulife.com'

publishHTML([allowMissing: false, alwaysLinkToLastBuild: true, includes: '**/*.html,**/*.css,**/*.png,**/*.jpg,**/*.giff', keepAll: false, reportDir: 'dashboard', reportFiles: 'dashboard.htm', reportName: 'HTML Report', reportTitles: 'HTML Report''])
          
                }
            }
        }
    }
}
