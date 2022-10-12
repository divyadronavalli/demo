pipeline{
agent any
tools {
maven 'maven'
jdk 'Java'
}
environment{
dockerhub = credentials('dockerHub')
}
stages{
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
