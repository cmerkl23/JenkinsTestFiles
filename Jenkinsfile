def Pythonprogram = "SimpleProg.py"
def Results = [
  -1: "Not a valid day",
  0: "Sunday",
  1: "Monday",
  2: "Tuesday",
  3: "Wednesday",
  4: "Thursday",
  5: "Friday",
  6: "Saturday",
  7: "Not a valid day"
  ]

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
        
        echo "return value python ${params.Sourcerepo}/${Pythonprogram} -1"
        sh "python ${params.Sourcerepo}/${Pythonprogram} -1"
        echo "return value ${Results[-1]}"

        Error(message: "Executing First Py failed") {
          sh "python ${params.Sourcerepo}/${Pythonprogram} -1" == Results[-1] 
        }
       
      }
    }

    stage('Deploy') {
      steps {
        echo "Deploy succeeded"
      }
    }

  }
}