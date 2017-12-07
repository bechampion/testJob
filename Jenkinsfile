pipeline{
   agent any
   environment { 
   configuration = wrap([$class: 'VaultConfiguration',
       vaultUrl: 'http://my-very-other-vault-url.com',
       vaultCredentialId: 'my-vault-cred-id'])
   secrets = wrap([
   [$class: 'VaultSecret', path: 'secret/testing', secretValues: [
   [$class: 'VaultSecretValue', envVar: 'testing', vaultKey: 'value_one'],
   ]]])
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
      wrap([$class: 'VaultBuildWrapper', configuration: configuration, vaultSecrets: secrets]) {
      echo '1'
      }
    }
   }
  }
}
