pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
	agent none
      stages{
           stage('Checkout'){
              agent any
              steps{
		 echo 'cloning..'
                 git 'https://github.com/Sonal0409/DevOpsClassCodes.git'
              }
          }
          stage('Compile'){
              agent {label 'jenkins_slave'}
              steps{
                  echo 'compiling..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
              agent {label 'jenkins_slave'}
              steps{
		    
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
              agent {label 'jenkins_slave'}
              steps{
	         echo 'Testing'
                  sh 'mvn test'
              }
               post {
               success {
                   junit 'target/surefire-reports/*.xml'
               }
           }	
          }
          stage('Package'){
              agent any
              steps{
                  sh 'mvn package'
              }
          }
      }
}
