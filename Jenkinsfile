pipeline {
    agent any
  
  	tools { 
        maven 'maven_main'
        jdk 'jdk_main' 
    }

    stages {
        stage('Build') {
            steps {
                // To run Maven on a Windows agent, use
                 bat 'mvn clean test'
		    
		fileOperations([folderCopyOperation(destinationFolderPath: 'QmetryReport/dashboard', sourceFolderPath: 'dashboard')])
		fileOperations([folderCopyOperation(destinationFolderPath: 'QmetryReport/img', sourceFolderPath: 'img')])
		fileOperations([folderCopyOperation(destinationFolderPath: 'QmetryReport/test-results', sourceFolderPath: 'test-results')])
		fileOperations([fileCopyOperation(excludes: '', flattenFiles: false, includes: 'dashboard.htm', renameFiles: false, sourceCaptureExpression: '', targetLocation: 'QmetryReport', targetNameExpression: '')])
		//zip zipFile: 'report.zip', archive: false, dir: 'QmetryReport', overwrite: true	
            }

            post {
                
                success {
             		 publishHTML ([
					        allowMissing: false,
					        alwaysLinkToLastBuild: false,
					        keepAll: true,
					        reportDir: '',
					        reportFiles: 'dashboard.htm',
					        reportName: "Test Report"
					      ])
			
// 			archiveArtifacts artifacts: 'dashboard.htm', onlyIfSuccessful: true
// 			emailext mimeType: 'text/html', attachLog: false, attachmentsPattern: '',
// 			to: 'lazio_karisma@manulife.com',
//                 	body: '${FILE,path="templateBody.html"}',  
//                 	subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
			
			emailext mimeType: 'text/html', attachLog: false, attachmentsPattern: 'dashboard.htm',
                	to: 'lazio_karisma@manulife.com',
                	body: '${FILE,path="templateBody.html"}',       
                	subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
          
                }
            }
        }
    }
}
