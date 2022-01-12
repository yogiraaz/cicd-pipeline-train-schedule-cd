pipeline {
    agent any
    stages {
        stage('DeployToStaging') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    sshPublisher(
                        failOnError: true,
                        continueOnError: false,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'staging',
                                sshCredentials: [
                                    username: "$USERNAME",
                                    encryptedPassphrase: "$USERPASS"
                                ], 
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: '/root/scripts/onboard_agent.sh',
                                        remoteDirectory: '/home/deploy/',
                                        execCommand: 'sudo sh /home/deploy/onboard_agent.sh'
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
    }
}
