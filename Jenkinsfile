stage('DeployToStaging') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    sshPublisher(
                        failOnError: true,
                        continueOnError: false,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'staging', ## server name referencce 
                                sshCredentials: [
                                    username: "$USERNAME",
                                    encryptedPassphrase: "$USERPASS"
                                ], 
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: '/root/scripts/onboard_agent.sh',
                                        remoteDirectory: '/tmp',
                                        execCommand: 'sudo sh /root/scripts/onboard_agent.sh  > ./onboard.txt && sudo su omsagent -c 'python2 /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py' > ./checkconfig.txt'
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
