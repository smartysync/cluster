pipeline {
  agent any
  parameters {
    string(name: "CELL_NUMBER", defaultValue: "1", description: "Integration. Number of cells to deploy")
  }
  stages {
    stage("Retrieve build environment") {
      steps {
        script {
          GIT_COMMIT_MESSAGE = sh(returnStdout: true, script: "git rev-list --format=%B --max-count=1 ${GIT_COMMIT}").trim()
        }
      }
    }
    stage("Integration tests") {
      steps {
        script {
          build job: "integration/master", parameters: [
            text(name: "COMMIT_MESSAGE", value: GIT_COMMIT_MESSAGE),
            string(name: "CLUSTER_PR", value: CHANGE_ID),
            string(name: "CELL_NUMBER", value: CELL_NUMBER)
          ]
        }
      }
    }
  }
}