pipeline {
    agent any

    tools {
        // 'Ansible' harus sama dengan nama di Global Tool Configuration
        ansible 'Ansible'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Run Ansible Playbook') {
	    environment {
            ANSIBLE_HOST_KEY_CHECKING = 'False'
            }
            steps {
                script {
                    /* * 'jenkins-ssh-key' = ID Kunci SSH kita
                     * 'inventory' = Nama file inventory kita
                     * '-u aeris' = Username SSH di server target
                     */
                    ansiblePlaybook(
                        playbook: 'playbook.yml',
                        inventory: 'inventory',
                        credentialsId: 'jenkins-ssh-key',
                        extras: "-u aeris"
                    )
                }
            }
        }
    }
}
