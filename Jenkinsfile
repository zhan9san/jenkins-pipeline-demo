pipeline {
  agent none
  options {
    timeout(time: 1, unit: 'DAYS')
    disableConcurrentBuilds()
  }
  stages {
    stage("Init") {
      agent any
      steps {
        echo "Init"
      }
    }
    stage("Build App") {
      agent any
      steps { 
        echo "Build App"
      }
    }
    stage("Run App Security Scan") {
      agent any 
      steps {
        echo "Run App Security Scan"
      }
    }
    stage("Build and Register Image") {
      agent any
      steps {
        echo "Build and Register Image"
      }
    }
    stage("Deploy Image to Dev") {
      agent any
      steps {
        echo "Deploy Image to Dev"
      }
    }
    stage("Test App in Dev") {
      agent any
      steps {
        echo "Test App in Dev"
      }
    }
    stage("Deploy Image to Test") {
      agent any
      when { branch 'master' }
      steps {
        echo "Deploy Image to Test"
      }
    }
    stage("Test App in Test") {
      agent any
      when { branch 'master' }
      steps {
        echo "Test App in Test"
      }
    }
    stage("Proceed to prod?") {
      agent none
      when { branch 'master' }
      steps { proceedTo('prod') }
    }
    stage("Deploy Image to Prod") {
      agent any
      when { branch 'master' }
      steps {
        echo "Deploy Image to Prod"
      }
    }
  }
}

def proceedTo(environment) {
    def description = "Choose 'yes' if you want to deploy to this build to " + 
        "the ${environment} environment"
    def proceed = 'no'
    timeout(time: 4, unit: 'HOURS') {
        proceed = input message: "Do you want to deploy the changes to ${environment}?",
            parameters: [choice(name: "Deploy to ${environment}", choices: "no\nyes",
                description: description)]
        if (proceed == 'no') {
            error("User stopped pipeline execution")
        }
    }
}
