# check
repositorio do desafio 
### **Passo 1: Análise Técnica do Código Terraform (Tarefa 1)**

#### 1.1. **Abrir o Arquivo `main.tf`**
- O arquivo `main.tf` define a criação de recursos na AWS, como VPC, Subnet, Security Group, Key Pair e Instância EC2. Esses recursos formam a infraestrutura básica necessária para rodar uma aplicação.

#### 1.2. **Descrição Técnica do Código**
- **VPC (Virtual Private Cloud)**: Criação de uma rede isolada onde os outros recursos estarão localizados, garantindo segurança e controle total sobre a rede.
- **Subnet**: Dentro da VPC, é criada uma subnet pública para garantir que a instância EC2 tenha acesso à Internet, permitindo a comunicação entre a instância e a AWS.
- **Security Group**: O Security Group é configurado para permitir o tráfego nas portas 22 (SSH) e 80 (HTTP), controlando o acesso à instância.
- **Key Pair**: O Key Pair é necessário para acessar a instância EC2 via SSH, garantindo que o login seja seguro.
- **Instância EC2**: Uma instância EC2 com Ubuntu será criada dentro da VPC, onde será instalado e configurado automaticamente o servidor web Nginx.

---

### **Passo 2: Modificação e Melhoria do Código Terraform (Tarefa 2)**

#### 2.1. **Melhoria de Segurança**
Para melhorar a segurança da infraestrutura, implementamos as seguintes melhorias:

1. **Limitar o Acesso SSH no Security Group**: Restrinja o acesso SSH (porta 22) apenas ao seu IP para garantir que apenas dispositivos específicos possam acessar a instância EC2 via SSH. Isso impede acessos não autorizados à sua máquina.

2. **Aplicação do Princípio de Menor Privilégio com IAM Roles**: Caso a instância EC2 precise acessar outros serviços AWS (como S3 ou RDS), foi criada uma role IAM com permissões mínimas necessárias para que a instância possa interagir com esses serviços, garantindo mais controle sobre o que pode ser acessado pela instância.

#### 2.2. **Automação da Instalação do Nginx**
Para automatizar a instalação e execução do servidor web Nginx, usamos o parâmetro `user_data`. Esse script é executado automaticamente na primeira inicialização da instância EC2, configurando o Nginx sem intervenção manual.
 
#### 2.3. **Outras Melhorias**
- **Definição de Variáveis**: Para tornar o código mais flexível e reutilizável, definimos variáveis como `instance_type`, `ami_id`, etc. Isso permite que você personalize facilmente o tipo de instância ou a AMI sem precisar alterar o código diretamente.
 

### **Passo 3: Documentação e Entrega**

#### 3.1. **Criação do README.md**

## Descrição Técnica

### VPC
A VPC cria uma rede isolada para os recursos da AWS, permitindo o controle total sobre a comunicação de rede e a criação de subnets, onde outros recursos serão alocados.

### Instância EC2
A instância EC2 é criada usando uma imagem Ubuntu. Após a criação, o Nginx é instalado automaticamente via script `user_data` para garantir que o servidor web esteja em funcionamento logo após a inicialização da máquina.

## Modificações Implementadas

### Melhorias de Segurança
- Restringimos o acesso SSH ao nosso IP específico, evitando que qualquer pessoa tente acessar a instância através de SSH.
- Foi implementada uma **IAM Role** com permissões mínimas necessárias para a instância EC2 acessar serviços AWS, seguindo o princípio de menor privilégio.

### Automação da Instalação do Nginx
- A instância EC2 é configurada automaticamente para instalar e iniciar o Nginx durante a inicialização, utilizando um script `user_data`.

### Outras Melhorias
- Definimos variáveis para o tipo de instância e outras configurações, permitindo fácil customização do código.
```

#### 3.2. **Comandos para Inicializar e Aplicar o Terraform**

```bash
# Clone o repositório:
git clone <URL_DO_REPOSITORIO>
cd <diretorio_do_repositorio>

# Inicialize o Terraform:
terraform init

# Planeje a infraestrutura:
terraform plan

# Aplique a infraestrutura:
terraform apply

# Para destruir a infraestrutura:
terraform destroy.

