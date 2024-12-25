pipeline {
    agent any


    environment {
    SVC_ACCOUNT_KEY = credentials('TERRAFORM-AUTH')
  }
     
    stages {
        stage ('checkout'){
            steps {
                git branch: 'main', url: 'https://github.com/HaribabuParella/gcp_tf_modules.git'
            }
        }
      

		stage('Set Terraform path') {
            steps {
                script {
                    def tfHome = tool name: 'Terraform'
                    env.PATH = "${tfHome}:${env.PATH}"
                }
                sh 'echo $SVC_ACCOUNT_KEY | base64 -d > terraform.json'
		sh 'pwd'
                sh 'terraform --version'               
               
            }
        }
        
         stage('Initialize Terraform') {
		 steps {  
			  dir('Module')
			 {
                sh 'terraform init'
			 }
		 }
	 }
				  
	stage('Terraform Action') {
		 steps {  
			  dir('Module')
			 {
                sh 'terraform $TF_ACTIONS -var-file=./tfvars/dev.tfvars --auto-approve'
			 }
		 }
	}
                             
}
}
