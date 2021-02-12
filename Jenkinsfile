pipeline {
 agent {label 'JenkinsLowLevelPlattformWithPython'}

  stages {
    stage('Build') {
      steps {

        echo "try to mkdir ${params.Localworkspace}"
        sh "mkdir ${params.Localworkspace}"
        echo "${params.Localworkspace} has been created"
        
        echo "try to git clone ${params.Sourcerepo} ${params.Localworkspace}"
        sh "git clone ${params.Sourcerepo} ${params.Localworkspace}"
        echo "${params.Sourcerepo} has been cloned to ${params.Localworkspace}"
        
        
      }
    }

    stage('Test') {
      steps {
        warnError(message: "Executing First Py failed") {
          sh "python ~/PyScripts/SuccessFull.py"
        }

        warnError(message: "Second Py failed") {
          sh "python ~/PyScripts/Failed.py"
        }

        sh "python ~/PyScripts/SuccessFull.py"
      }
    }

    stage('Deploy') {
      steps {
        echo "Deploy succeeded"
      }
    }

  }
}