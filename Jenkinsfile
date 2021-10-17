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

