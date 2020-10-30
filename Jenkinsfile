pipeline{
        agent any
        stages{
            stage('clone git file'){
                steps{
                    sh 'if [! -d "chaperootodo_client"]
                        then 
                          git clone https://gitlab.com/qacdevops/chaperootodo_client
                        fi'
                }
            }
            stage('install docker'){
                steps{
                    sh 'curl https://get.docker.com | sudo bash'
                    sh 'sudo usermod -ag docker jenkins'
                    sh 'sudo apt update'
                    sh 'sudo apt install -y curl jq'
                    sh 'version=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r ".tag_name")'
                    sh 'sudo curl -L "https://github.com/docker/compose/releases/download/${version}/docker-compose-$(uname -s)-$(uname -m)" -o/usr/local/bin/docker-compose'
                    sh 'sudo chmod +x /usr/local/bin/docker-compose
                    }
                }
            stage('deploy application'){
                steps{
                    sh "sudo docker-compose pull && sudo -E DB_PASSWORD=${DB_PASSWORD} docker-compose up -d.
                }
            }
        }    
}
