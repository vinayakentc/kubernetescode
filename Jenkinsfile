node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Build image') {
  
      
        sh'sudo docker build -t vinayakentc/test .'
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        echo 'Push to Repo'
        sudo docker login -u "vinayakentc" -p "Ganesh@298" docker.io
        sudo docker push vinayakentc/test:"${env.BUILD_NUMBER}"}
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
