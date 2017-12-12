pipeline{
   agent any
   //agent {
    //docker { image 'node:7-alpine' }
   //}
   environment { 
   terraform = "https://releases.hashicorp.com/terraform/0.11.1/terraform_0.11.1_linux_amd64.zip?_ga=2.48146279.1348528623.1512638709-486120205.1512548428"
}
   stages { 
   stage('Terraform Preparation') { // for display purposes
    steps {
      echo 'Downloading Terraform'
      echo "Terraform Version ${tfVersion}"
      sh "wget ${terraform}"
      sh "unzip -o terraform_0.11.1_linux_amd64.zip?_ga=2.48146279.1348528623.1512638709-486120205.1512548428"
      sh "./terraform || true"
    }
   }
   stage('Terraform Plan') {
    steps {
      echo 'terraform plan'
      input 'Terraform Apply??'
      wrap([$class: 'VaultBuildWrapper', configuration: vaultConfiguration(), vaultSecrets : vaultSecrets()]){
      sh "echo ${env.testing} > /tmp/secret"
      echo "${env.PATH}"
      }
    }
   }
  }
}
def vaultConfiguration() {
    return [$class: 'VaultConfiguration',vaultUrl: 'http://127.0.0.1:8200', vaultCredentialId:'vault-token']
}
def vaultSecrets() { 
   return [[$class: 'VaultSecret', path: 'secret/hello', secretValues: [[$class: 'VaultSecretValue', envVar: 'testing', vaultKey: 'value'],]]]
}

