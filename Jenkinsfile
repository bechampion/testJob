pipeline{
   agent any
   stages { 
   stage('Terraform Preparation') { // for display purposes
    step {
   def terraform = "https://releases.hashicorp.com/terraform/0.11.1/terraform_0.11.1_linux_amd64.zip?_ga=2.48146279.1348528623.1512638709-486120205.1512548428"
   echo 'Downloading Terraform'
   echo "Terraform Version ${tfVersion}"
   sh "wget ${terraform}"
   sh "unzip -o terraform_0.11.1_linux_amd64.zip?_ga=2.48146279.1348528623.1512638709-486120205.1512548428"
   sh "./terraform || true"
    }
   }
   stage('Terraform Plan') {
    echo 'terraform plan'
    input 'Terraform Apply??'
   }
   stage('Terraform Apply') {
   echo 'Results'
   ls = sh(returnStdout: true, script: 'ls /')
   if (ls.contains("tmp")){
       echo "Contains"
   }else { 
        echo "Doesn't contain"
   }
   echo "${ls}"
   
   }
}
}
