pipeline {
    agent none
    environment {
        JBOSS_CREDENTIALS = credentials('jboss-credentials')
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'maven:3.8.8-eclipse-temurin-17-alpine'
                }
            }            
            steps {
                sh 'mvn clean package -B -ntp -DskipTests'
            }
        }
        stage('Deploy with jboss-cli.sh') {
            agent any
            steps {
                sshagent (credentials: ['debian-private-key']){
                    // tener encuenta jboss se encuentra instalado
                    // ip 54.190.196.47 , es la ip del host debian
                    sh '''
                        pwd
                        ls -la
                        env | sort

                        scp -o StrictHostKeyChecking=no target/applicationPetstore.war admin@54.190.196.47:/home/admin
                        ssh admin@54.190.196.47 "~/jboss-eap-7.4/bin/jboss-cli.sh --user=$JBOSS_CREDENTIALS_USR --password=$JBOSS_CREDENTIALS_PSW -c --command='undeploy applicationPetstore.war'"
                        ssh admin@54.190.196.47 "~/jboss-eap-7.4/bin/jboss-cli.sh --user=$JBOSS_CREDENTIALS_USR --password=$JBOSS_CREDENTIALS_PSW -c --command='deploy /home/admin/applicationPetstore.war'"
                        ssh admin@54.190.196.47 'rm -f /home/admin/applicationPetstore.war'
                    '''
                }
            }
        }
        // stage('Deploy with Ansible') {
        //     agent {
        //         docker {
        //             image 'quay.io/ansible/ansible-runner:stable-2.12-latest'
        //             args '-u root'
        //         }
        //     }
        //     environment {
        //         ANSIBLE_HOST_KEY_CHECKING = "False"
        //     }
        //     options { skipDefaultCheckout() }
        //     steps {
        //         dir('ansible'){
        //             sshagent (credentials: ['debian-private-key']){
        //                 sh 'env | sort'

        //                 // sh 'pip install --upgrade ansible'
        //                 // sh 'ansible --version'
        //                 // sh 'ansible-galaxy --version'
        //                 // sh 'ansible-galaxy collection install community.general'
                       
        //                 sh 'ansible-playbook -i hosts deploy_jboss.yml'
        //             }
        //         }
        //     }
        // }

    }
}