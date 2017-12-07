pipeline{
   agent any
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
      wrap([$class: 'VaultBuildWrapper', configuration:  [$class: 'VaultConfiguration',
       vaultUrl: 'http://127.0.0.1:8200',
       vaultCredentialId: 'cd71e714-d5e3-761d-393a-4ae127513b7e'], vaultSecrets :  [
   [$class: 'VaultSecret', path: 'secret/testing', secretValues: [
   [$class: 'VaultSecretValue', envVar: 'testing', vaultKey: 'value_one'],
   ]]]]) { 
      echo '1'
      }
    }
   }
  }
}
