node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }
	stage('compile'){
	
	sh '''
	  mvn compile
	'''
	
	
	}
	
	stage('package'){
	
	sh '''
	  mvn package
	'''
	
	
	}
       stage('SonarCoverageResults'){
	
	sh '''
	  mvn clean verify sonar:sonar -Dsonar.projectKey=taxibooking -Dsonar.host.url=http://44.204.40.27:9000 -Dsonar.login=sqp_f8fc9d38a65a267b21059b7e1e6ca8f68c342fb3
	'''
	
	
	}
	stage('SendingToNexus'){
	
	sh '''
	  
          curl -v -u admin:admin123 --upload-file /var/lib/jenkins/workspace/project1/target/*.war http://44.204.40.27:8081/nexus/content/repositories/myrepo
	'''
	
	
	}
       stage('DockerBuild'){
	
	app = docker.build("devopsvmr/11pm")
	
	
	}
       stage('DockerPush'){
	
	docker.withRegistry('https://registry.hub.docker.com', 'dockercred') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
      
             }
	
	
	}
  /*stage('ConnectingToEKS'){
	
	sh '''
	  aws eks update-kubeconfig --region us-east-1 --name sample-ekscluster
	  kubectl get nodes

	'''
	
	
	
	}*/
   
  }
