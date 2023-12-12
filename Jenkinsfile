
pipeline {
    agent any

    tools {
       
        maven "maven"
    }

    parameters { 
        string(name: 'BRANCH', defaultValue: 'master', description: '') 
    }

    stages {
        stage('Build') {
            steps {
                
                git 'https://github.com/the-mad1/simple-maven-project-with-tests'
                git checkout ${params.BRANCH}

                // Run Maven on a Unix agent.
                // sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
