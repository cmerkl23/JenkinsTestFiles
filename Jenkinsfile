def Pythonprogram = "SimpleProg.py"
def Results = [0: 'Sunday', 1: "Monday", 2: "Tuesday", 3: "Wednesday", 4: "Thursday", 5: "Friday", 6: "Saturday", 7: "Not a valid day"]
def GivenResult = ""

pipeline {
 //gent {label 'JenkinsLowLevelPlattformWithPython'}
 agent {label 'any'}

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
          GivenResult = sh(script: "python ${params.Localworkspace}/${Pythonprogram} 0", returnStdout: true).trim()

          echo "GivenResult: ${GivenResult}"
          echo "Results[0]: ${Results[0]}"

          assert GivenResult == Results[0] : "GivenResult = ${GivenResult}, but should be ${Results[0]}"

          Results.each {key, val ->
                        GivenResult = sh(script: "python ${params.Localworkspace}/${Pythonprogram} ${key}", returnStdout: true).trim()
                        echo "GivenResult = ${GivenResult} <----> Expected result = ${val}"

                        assert GivenResult == val : "GivenResult = ${GivenResult}, but should be ${val}"
                       }



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