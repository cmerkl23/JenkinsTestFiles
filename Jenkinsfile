def Pythonprogram = "SimpleProg.py"
def Results = [0: 'Sunday', 1: "Monday", 2: "Tuesday", 3: "Wednesday", 4: "Thursday", 5: "Friday", 6: "Saturday", 7: "Not a valid day"]
def GivenResult = ""

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
        
        script {
          GivenResult = sh(script: "python ${params.Localworkspace}/${Pythonprogram} 0", returnStdout: true)

          echo "GivenResult: ${GivenResult}"
          echo "Results[0]: ${Results[0]}"

          assert GivenResult == "Sunday" : "GivenResult = ${GivenResult}, but should be Sunday"
        }
               
       
      }
      
    }

    stage('Deploy') {
      steps {
        echo "Deploy succeeded"
      }
    }

  }
  post {
    always {
        sh "sudo rm -r ${params.Localworkspace}"
    }
  }
}