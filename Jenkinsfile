pipeline {
  agent any
  stages {
    stage('angular-docker') {
       steps {
          git 'https://github.com/crunchy-devops/angular-realworld-example-app.git'
          sh "docker build -t nodejs-realworld ."
       }
    }
    stage('angular-web'){
      steps {
        script {
           def set_container = sh(script: '''CONTAINER_NAME="web"
                                             OLD="$(docker ps --all --quiet --filter=name="$CONTAINER_NAME")"
                                             if [ -n "$OLD" ]; then
                                               docker rm -f $OLD
                                             fi
                                             docker run -d -it --name web -p 4200:4200 nodejs-realworld '''
                                   )
        }
      }
    }
  }
}
