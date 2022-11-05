def snykCliBaseName(){
    if (isUnix()) {
        def uname = sh script: 'uname', returnStdout: true
        if (uname.startsWith("Darwin")) {
            return "snyk-macos"
        } else {
            return "snyk-linux"
        }
    } else {
        return "snyk-win.exe"
    }
}
    
pipeline {
  agent any 
     
        
  tools {
    maven 'maven'
  }
        
  environment {
    Snyk = 'Snyk'
    Trivy = 'Trivy'
    Audit = 'Audit'
  }
  
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                  
            ''' 
      }
    } 
    
     
 stage ('Check-Git-Secrets') {
      steps {
        sh 'sudo chmod 666 /var/run/docker.sock'
        //sh 'sudo docker run raphaelareya/gitleaks:latest -r https://github.com/securitis/CICD.git'       
        //sh 'rm trufflehog || true'
        //sh 'docker run gesellix/trufflehog --json https://github.com/cehkunal/webapp.git > trufflehog'
        //sh 'cat trufflehog'
      }
    }  
         
   stage ('Container Scan') {
       steps {
              sh 'echo Container Scan'
            //sh 'docker run aquasec/trivy:0.18.3 vulnerables/phpldapadmin-remote-dump'
            //sh 'docker run aquasec/trivy:0.18.3 repo https://github.com/securitis/CICD.git'
            //sh 'docker run aquasec/trivy:0.18.3 image vulnerables/web-dvwa:latest'
             }
             } 
  stage ('Snyk Jar Scann') {
     steps {
              snykSecurity failOnError: false, failOnIssues: false, organisation: 'securitis', severity: 'high', snykInstallation: 'snyk', snykTokenId: 'snykid', additionalArguments: '--target-dir=/var/lib/jenkins/workspace/WebGoatPipeline --all-projects --scan-all-unmanaged --detection-depth=4'
             //snykSecurity failOnError: false, failOnIssues: false, organisation: 'securitis', projectName: 'CICDSelf', severity: 'high', snykInstallation: 'snyk', snykTokenId: 'snykid', additionalArguments: '--target-dir=/var/lib/jenkins/workspace/SelfCICD'
             //snykSecurity failOnError: false, failOnIssues: false, organisation: 'securitis', projectName: 'CICDSelf', severity: 'high', snykInstallation: 'sny', snykTokenId: 'snykid', targetFile: '/var/lib/jenkins/workspace/SelfCICD'
             //sh 'snykSecurity failOnError: false, failOnIssues: false, organisation: 'self', projectName: 'CICDSelf', severity: 'high', snykTokenId: 'snykid', targetFile: '/var/lib/jenkins/workspace/SelfCICD''     
            //sh 'snykSecurity failOnError: false, failOnIssues: false, organisation: 'self', projectName: 'CICDSelf', severity: 'high', snykInstallation: 'snyk', snykTokenId: 'snykid', targetFile: '/var/lib/jenkins/workspace/SelfCICD''
         
       }
    }
 
    
    
  stage ('Snyk Dependency Scan') {
     steps {
          snykSecurity failOnError: false, failOnIssues: false, organisation: 'securitis', snykInstallation: 'snyk', snykTokenId: 'snykid', additionalArguments: '--target-dir=/var/lib/jenkins/workspace/WebGoatPipeline --all-projects --detection-depth=4'   
       //snykSecurity failOnError: false, failOnIssues: false, organisation: 'securitis', severity: 'high', snykInstallation: 'snyk', snykTokenId: 'snykid', additionalArguments: '--target-dir=/var/lib/jenkins/workspace/SelfCICD --all-projects --detection-depth=4'
             //snykSecurity failOnError: false, failOnIssues: false, organisation: 'securitis', projectName: 'CICDSelf', severity: 'high', snykInstallation: 'snyk', snykTokenId: 'snykid', additionalArguments: '--target-dir=/var/lib/jenkins/workspace/SelfCICD'
             //snykSecurity failOnError: false, failOnIssues: false, organisation: 'securitis', projectName: 'CICDSelf', severity: 'high', snykInstallation: 'sny', snykTokenId: 'snykid', targetFile: '/var/lib/jenkins/workspace/SelfCICD'
             //sh 'snykSecurity failOnError: false, failOnIssues: false, organisation: 'self', projectName: 'CICDSelf', severity: 'high', snykTokenId: 'snykid', targetFile: '/var/lib/jenkins/workspace/SelfCICD''     
            //sh 'snykSecurity failOnError: false, failOnIssues: false, organisation: 'self', projectName: 'CICDSelf', severity: 'high', snykInstallation: 'snyk', snykTokenId: 'snykid', targetFile: '/var/lib/jenkins/workspace/SelfCICD''
          
       }
    }
      
  stage ('Snyk SAST Scan') {
     steps {
             snykSecurity failOnError: false, failOnIssues: false, organisation: 'securitis', snykInstallation: 'snyk', snykTokenId: 'snykid', additionalArguments: '--target-dir=/var/lib/jenkins/workspace/WebGoatPipeline --code'
             //snykSecurity failOnError: false, failOnIssues: false, organisation: 'securitis', projectName: 'CICDSelf', severity: 'high', snykInstallation: 'snyk', snykTokenId: 'snykid', additionalArguments: '--target-dir=/var/lib/jenkins/workspace/SelfCICD'
             //snykSecurity failOnError: false, failOnIssues: false, organisation: 'securitis', projectName: 'CICDSelf', severity: 'high', snykInstallation: 'sny', snykTokenId: 'snykid', targetFile: '/var/lib/jenkins/workspace/SelfCICD'
             //sh 'snykSecurity failOnError: false, failOnIssues: false, organisation: 'self', projectName: 'CICDSelf', severity: 'high', snykTokenId: 'snykid', targetFile: '/var/lib/jenkins/workspace/SelfCICD''     
            //sh 'snykSecurity failOnError: false, failOnIssues: false, organisation: 'self', projectName: 'CICDSelf', severity: 'high', snykInstallation: 'snyk', snykTokenId: 'snykid', targetFile: '/var/lib/jenkins/workspace/SelfCICD''
          
       }
    }
   
         // Install the Snyk CLI by downloading a binary. For more information, check:
        // https://docs.snyk.io/snyk-cli/install-the-snyk-cli
        stage('Install snyk CLI') {
            steps {
                script {
                    def basename = snykCliBaseName()

                    if (isUnix()) {
                        sh("curl -O -s -L https://static.snyk.io/cli/latest/$basename")
                        sh("curl -O -s -L https://static.snyk.io/cli/latest/${basename}.sha256")
                        //sh("shasum -c ${basename}.sha256")
                        sh("chmod +x $basename && mv $basename ./snyk")
                    } else {
                        throw "Not implemented."
                    }
                }
            }
        }
    
 /*   stage('Snyk Container') {
      steps {
           catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
            sh './snyk auth 0da82457-fa1a-497f-a81d-71dc8dc0a11a'   
            sh './snyk container test sebsnyk/juice-shop --file=Dockerfile --sarif-file-output=results-container.sarif'
           }
            recordIssues tool: sarif(name: 'Snyk Container', id: 'snyk-container', pattern: 'results-container.sarif')
           }
   } */
   
   
   stage ('Build') {
      steps {
      //sh 'mvn clean package'
        sh 'mvn clean install'
     }
    }
 

    stage ('Deploy') {
     steps {
            sh 'chmod +777  /var/lib/jenkins/workspace/SnykDemo'
            sh 'sudo cp -r /var/lib/jenkins/workspace/SnykDemo /var/www/SnykDemo/html' 
            //sh 'chmod +777 /var/lib/jenkins/workspace/CICD/target/WebApp'
            //sh 'ls /var/www/html'
            //sh 'sudo cp -r /var/lib/jenkins/OWASP-Dependency-Check/reports /var/www/html'
       }
    }
     
    
    
 
    
  }
} 



