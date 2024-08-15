pipeline{
    agent{
        label 'AGENT-1'
    }

    options{
        timeout(time: 45, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    parameters{
        string(name: 'appVersion', defaultValue: '1.0.0', description: 'Which Version to Deploy?')
    }

    environment{
        def appVersion = ""
        def nexusUrl = "nexus.harshadevops.site:8081"
    }

    stages{
        stage('Print the Application Version'){
            steps{
                sh """
                    echo "Application Version: ${params.appVersion}"
                """
            }
        }
        stage('Init'){
            steps{
                sh """
                    terraform init -reconfigure
                """
            }
        }
        stage('Plan'){
            steps{
                sh """
                    terraform plan -var="app_version=${params.appVersion}"
                """
            }
        }
        stage('Apply'){
            steps{
                sh """
                    terraform apply -var="app_version=${params.appVersion}" -auto-approve
                """
            }
        }
    }
}