pipeline {
 agent {
  kubernetes {
   yaml '''
        spec:
        containers:
          - name: gradle
            image: gradle:6.3-jdk14 
        '''
     }
 }
 triggers {
    githubPush()
 }
 stages {
   stage('debug') {
    steps {
      echo env.GIT_BRANCH
      echo env.GIT_LOCAL_BRANCH 
     }
  }
  stage('feature') {
   when {
    expression {
     return env.GIT_BRANCH == "origin/feature"
    }
   }
   steps { 
     echo "I am a feature branch"
   }
  }
  stage('master') {
   when {
    expression {
     return env.GIT_BRANCH == "origin/master"
    }
   } 
   steps { 
   sh '''
      pwd 
      cat build.gradle 
      sed -i 's/minimum = 0.2/minimum = 0.1/g' build.gradle
      ./gradlew jacocoTestCoverageVerification 
      ./gradlew jacocoTestReport
      '''
      publishHTML(target: [
                    reportDir: 'build/reports/jacoco/test/html',
		    reportFiles: 'index.html',
		    reportName: "JaCoCo Report"])

     echo "I am a master branch"
    }
  }
  stage('playground') {
     when {
      expression {
        return env.GIT_BRANCH == "origin/playground"
        }
       }
       steps {
          echo "I am a playground branch"
       }
    }

 }
}

