pipeline{
   agent any
   stages{
        stage('Checkout') {
           steps{
            git url: 'https://github.com/spartaraja/testuu.git'
        }
        }
        stage ('Package Stage') {
           steps{
            bat 'mvn clean package'
        }
        }
        
        stage('Sonar Scanner Coverage') {
           steps{
            bat 'mvn sonar:sonar -Dsonar.login=e8bbfb613f6f47cadee1e97ad7a516ef37130714 -Dsonar.host.url=http://localhost:9000'
        }
        }
        stage ('Publish to Nexus') {
           steps{
            nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'pipeline_snapshot_test1', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: './target/gift-shop-api.war']],mavenCoordinate: [artifactId: 'sonar-maven-plugin', groupId: 'org.sonarsource.scanner.maven', packaging: 'war', version: '3.8.5']]]
        }

        }
    
   }
}
