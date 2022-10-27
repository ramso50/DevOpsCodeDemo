pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
	agent Agent1
      stages{
           stage('Checkout'){
              agent {label 'jenkins_slave'}
              steps{
		 echo 'cloning..'
                 git 'https://github.com/ramso50/DevOpsCodeDemo.git'
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
