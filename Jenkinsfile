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
   stage('Approval') {
      steps {
        script {
          def userInput = input(id: 'confirm', message: 'Apply Terraform?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
        }
      }
    }
 
 
  stage ('Terraform apply') { 
     steps {
        sh '''
   cd ecs-fargate-task/
   terraform apply "tfplan.out"
   
   ''' 
       }
    }
}
}
 //logstashSend failBuild: true, maxLines: 10000