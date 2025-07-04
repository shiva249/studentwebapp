node {

def mavenHome = tool name: 'maven3.9.10'

stage('checkout'){
git branch: 'main', credentialsId: '0a89335a-904f-4a4f-b935-f56f411a5f00', url: 'https://github.com/shiva249/studentwebapp.git'
}
stage('build'){
sh "${mavenHome}/bin/mvn clean package"
}
stage('Publish JaCoCo Report') {
        jacoco execPattern: '**/target/jacoco.exec',
               classPattern: '**/target/classes',
               sourcePattern: '**/src/main/java',
               inclusionPattern: '**/*.class',
               exclusionPattern: '**/test/**'

        jacoco changeBuildStatus: true,
               minimumInstructionCoverage: '80',
               minimumBranchCoverage: '80',
               minimumComplexityCoverage: '80',
               minimumLineCoverage: '80',
               minimumMethodCoverage: '80',
               minimumClassCoverage: '80'
    }
stage('deployment') {

sshagent(['248ed6ab-bf8c-457f-b053-7527cecdb360']) {
sh "scp -o StrictHostKeyChecking=no  target/students.war ec2-user@54.219.11.253:/opt/apache-tomcat-9.0.106/webapps/"
}
}
}
