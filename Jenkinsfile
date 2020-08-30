
pipeline{
  agent any 
  tools{
     maven "Maven3"
     }
  stages{
     stage('gitSCM'){
      steps{
        echo 'Start of gitSCM step'
        git changelog: false, credentialsId: 'git credentials', poll: false, url: 'https://github.com/mgujjula/spring3-mvc-maven-xml-hello-world.git'
      }
      }
	  stage ('Initialize') {
        steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
      }
      stage('build'){
      steps{
        sh 'mvn -f pom.xml clean package'
      }
    }
    stage('deploy'){
      steps{
        deploy adapters: [tomcat8(credentialsId: 'tomcat_credentials', path: '', url: 'http://ec2-13-126-29-117.ap-south-1.compute.amazonaws.com:8181/')], contextPath: 'hello_world_pipeline', onFailure: false, war: '**/target/*.war'
      }
    }
  }
}

 
