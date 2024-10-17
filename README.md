# Descrição Técnica
Este arquivo contém a descrição técnica do código main.tf e as alterações realizadas para melhorar a segurança e automatizar a instalação do Nginx.

## Análise Técnica

### Provedor e Variáveis
- **Provedor:** Define o provedor AWS e a região como `us-east-1`.
- **Variáveis:** Declara variáveis de string para o nome do projeto e do candidato, respectivamente, com valores padrão.

### Recursos Criados
- **Chave SSH:** Gera uma chave privada RSA e cria um par de chaves EC2 usando a chave pública gerada.
- **VPC e Sub-rede:** Cria uma VPC e uma sub-rede associada.
- **Internet Gateway e Tabela de Roteamento:** Cria um internet gateway e uma tabela de roteamento com uma rota padrão para o internet gateway.
- **Grupo de Segurança:** Cria um grupo de segurança permitindo tráfego SSH de entrada e todo o tráfego de saída.
- **Instância EC2:** Cria uma instância EC2 t2.micro utilizando a AMI Debian 12, associada à sub-rede e grupo de segurança configurados, e executa um script de usuário que realiza atualizações do sistema ao ser iniciada.
- **Outputs:** Fornece a chave privada gerada e o endereço IP público da instância EC2.

## Modificação e Melhoria do Código

### Melhoria de Segurança
- **Descrição Técnica:** Restringe o tráfego SSH para um IP específico em vez de "0.0.0.0/0". Adiciona regras para permitir tráfego HTTP (porta 80) e HTTPS (porta 443). Essas alterações aumentam a segurança contra acessos indesejados, permitindo apenas o tráfego necessário.
- **Resultado Esperado:** Maior segurança ao limitar o acesso SSH a um IP específico e permitindo apenas tráfego HTTP/HTTPS necessário para um servidor web.

### Automação da Instalação do Nginx
- **Descrição Técnica:** Modifica o script de usuário (`user_data`) da instância EC2 para instalar e iniciar o Nginx automaticamente após a criação da instância. Isso garante que o servidor web esteja pronto para uso imediatamente após a criação.
- **Resultado Esperado:** A instância EC2 estará configurada com o Nginx instalado e iniciado automaticamente, permitindo o acesso ao servidor web via HTTP/HTTPS.

## Instruções de Uso

### Pré-requisitos
- Terraform instalado
- Credenciais AWS configuradas

### Passos para Inicializar e Aplicar a Configuração Terraform

```sh
# Clone o repositório
# Navegue até o diretório contendo os arquivos Terraform

# Inicialize o Terraform
terraform init

# Visualize o plano de execução
terraform plan

# Aplique a configuração Terraform
terraform apply
