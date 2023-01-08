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

/*stage ('Terraform version') { 
  steps {
   sh '''
    terraform --version
   ''' 
    }
    }
   */ 
  stage ('Terraform init') { 
  steps {
   sh '''
   cd ecs-fargate-task/
   terraform init
   ''' 
   }
   }
   /*
  stage ('Terraform plan') { 
  steps {
   sh '''
   cd ecs-fargate-task/
   terraform plan -out=tfplan.out
   terraform show -json tfplan.out
   ''' 
   }
   }
 */  
 stage ('Terraform apply') { 
  steps {
   sh '''
   cd ecs-fargate-task/
   //terraform apply --auto-approve
   terraform destroy --auto-approve
   ''' 
   }
        post { 
        always { 
            cleanWs()
         }
        }
       }
  }
}