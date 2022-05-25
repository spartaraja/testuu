node {
   
        stage('Checkout') {
            bat "xcopy /E https://github.com/spartaraja/testuu /Y"
        }
        stage ('Package Stage') {
            bat './mvnw clean package'
        }
        
        stage('Sonar Scanner Coverage') {
            bat "./mvnw sonar:sonar -Dsonar.login=e8bbfb613f6f47cadee1e97ad7a516ef37130714 -Dsonar.host.url=http://localhost:9000"
        }
        stage ('Publish to Nexus') {
            nexusPublisher nexusInstanceId: 'nexus', nexusRepositoryId: 'pipeline_snapshot_test1', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: './target/gift-shop-api.war']],mavenCoordinate: [artifactId: 'sonar-maven-plugin', groupId: 'org.sonarsource.scanner.maven', packaging: 'war', version: '3.8.5']]]
        }

       
    
   
}
