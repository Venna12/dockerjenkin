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
	  mvn clean verify sonar:sonar -Dsonar.projectKey=srikanth -Dsonar.host.url=http://3.82.92.225:9001 -Dsonar.login=sqp_51a6dbf886c173f84ca532f2675ddc88d790ee81
	'''
	
	
	}
	stage('SendingToNexus'){
	
	sh '''
	  
          curl -v -u admin:admin123 --upload-file /var/lib/jenkins/workspace/srikanth/target/*.war http://3.82.92.225:8081/nexus/content/repositories/srikanth
	'''
	
	
	}
       stage('DockerBuild'){
	
	app = docker.build("devopsvmr/sri")
	
	
	}
       stage('DockerPush'){
	
	docker.withRegistry('https://registry.hub.docker.com', 'dockercred') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
      
             }
	
	
	}
   /*stage('ConnectingToEKS'){
	
	sh '''
	  aws eks update-kubeconfig --region us-east-1 --name eksdemo
	  kubectl get nodes

	'''
	
	
	
	}*/
   
  }
