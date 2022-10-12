pipeline{
agent any
 tools {
        maven 'Maven 3.8.6'
        jdk 'default'
    }
environment{
dockerhub = credentials('dockerHub')
}
stages{
stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
stage('build image'){
when{
branch 'main'
}
steps{
sh 'docker build -t intraedge/demo .'
}
}
stage("pushing to dockerhub"){
when{
branch 'main'
}
steps{
sh 'docker tag intraedge/demo divyadronavalli/divyapractise'
sh 'echo $dockerhub PSW | docker login -u dockerhub USR --password-stdin'
sh 'docker push divyadronavalli/divyapractise'
}
}
}
}
