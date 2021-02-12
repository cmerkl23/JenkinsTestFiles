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
        
        //echo "return value python ${params.Localworkspace}/${Pythonprogram} 0"
        //sh "python ${params.Localworkspace}/${Pythonprogram} 0"
        //echo "return value ${Results[0]}"

        def ret = sh(script: 'uname', returnStdout: true)
        //println ret
        //GivenResult = sh(script: "python ${params.Localworkspace}/${Pythonprogram} 0", returnStdout: true).trim()
        //warnError(message: "Executing First Py failed") {
        //  assert GivenResult == Results[0] 
        //}
       
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