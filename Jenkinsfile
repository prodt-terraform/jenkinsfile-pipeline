pipeline {
agent any
tools {
  terraform 'terraform'
}
options { ansiColor('xterm') } 
stages { 
   stage ('Checkout Repo') { 
     steps { 
       cleanWs()
       sh  'git clone https://github.com/prodt-terraform/ecs-fargate-task.git'
      }
      } 

stage ('Terraform version') { 
  steps {
   sh '''
    terraform --version
   ''' 
    }
    }
    
  stage ('Terraform init') { 
  steps {
   sh '''
   cd ecs-fargate-task/
   terraform init
   ''' 
   }
   }
  stage ('Terraform plan') { 
  steps {
   sh '''
   cd ecs-fargate-task/
   terraform plan -out=tfplan.out
   
   ''' 
   }
   }
 }
 }logstashSend failBuild: true, maxLines: 1000