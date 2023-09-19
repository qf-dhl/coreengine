pipeline {
    agent {label 'maven-label'}

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                 checkout   scm

                // Run Maven on a Unix agent.
                // sh "mvn -Dmaven.test.failure.ignore=true -s settings.xml clean deploy sonar:sonar \
                //     -Dsonar.projectKey=coreengine \
                //     -Dsonar.host.url=http://3.129.244.8:9000 \
                //     -Dsonar.login=sqp_b9c9c598d6a7a55cc1e093dc4bf93c49ac85fc02"
                // sh "mvn clean verify sonar:sonar \
                //     -Dsonar.projectKey=coreengine \
                //     -Dsonar.host.url=http://3.129.244.8:9000 \
                //     -Dsonar.login=sqp_b9c9c598d6a7a55cc1e093dc4bf93c49ac85fc02"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
                sh "mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=testorggfcfg_coreengine"
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
