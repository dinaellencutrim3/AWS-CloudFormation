# AWS-CloudFormation
# ☁️ Desafio DIO - Automação de Infraestrutura com AWS CloudFormation

## 📘 Descrição do Projeto
Este repositório foi criado como parte do desafio da **Digital Innovation One (DIO)**, com o objetivo de aplicar os conceitos de **Infraestrutura como Código (IaC)** utilizando o **AWS CloudFormation**.  
Durante o laboratório, foi desenvolvida uma infraestrutura automatizada na AWS e documentado todo o processo de aprendizado, boas práticas e desafios enfrentados.

---

## 🎯 Objetivos do Desafio
- Aplicar os conhecimentos adquiridos sobre CloudFormation em um ambiente prático.  
- Automatizar a criação e o gerenciamento de recursos na AWS.  
- Documentar o processo técnico de forma clara e organizada.  
- Utilizar o GitHub como ferramenta de portfólio técnico e versionamento.

---

## 🧰 Tecnologias e Ferramentas Utilizadas
- **AWS CloudFormation**
- **AWS Management Console**
- **AWS CLI**
- **YAML / JSON**
- **Git e GitHub**
- **Markdown**

---

## ⚙️ Etapas Realizadas
1. Configuração inicial do ambiente AWS CLI.  
2. Criação do template CloudFormation (`template.yaml`) com os recursos desejados.  
3. Validação e execução do stack pelo console e pela CLI.  
4. Testes e ajustes de parâmetros e permissões.  
5. Registro dos insights e boas práticas observadas.

---

## 💡 Insights e Aprendizados
Durante o desenvolvimento deste desafio, foi possível compreender melhor:
- A importância do **CloudFormation** para padronizar e automatizar a infraestrutura.  
- Como a **Infraestrutura como Código (IaC)** facilita o versionamento e a reprodutibilidade de ambientes.  
- A relevância do **controle de acesso e segurança** na criação de stacks.  
- O uso do **GitHub** como ferramenta de documentação técnica e portfólio profissional.

---

## 📸 Evidências do Projeto
As capturas de tela do processo estão disponíveis na pasta:

AWSTemplateFormatVersion: '2010-09-09'
Description: Template para criar um bucket S3

Resources:
  MeuBucketS3:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: meu-bucket-dinaellen-cloudformation
# Notas do Desafio AWS CloudFormation

## Comandos úteis
- aws cloudformation validate-template --template-body file://template.yaml
- aws cloudformation create-stack --stack-name stack-dinaellen --template-body file://template.yaml
- aws cloudformation delete-stack --stack-name stack-dinaellen

## Observações
- Sempre validar o template antes de criar o stack.
- Usar nomes únicos para buckets S3.
AWSTemplateFormatVersion: '2010-09-09'
Description: >
  Template CloudFormation - Desafio DIO
  Infraestrutura simples contendo um Bucket S3 e uma Instância EC2.

# ========================
# 🔹 PARÂMETROS
# ========================
Parameters:
  KeyName:
    Description: Nome do par de chaves EC2 existente na sua conta AWS
    Type: AWS::EC2::KeyPair::KeyName
    ConstraintDescription: O par de chaves deve existir na região selecionada.

  InstanceType:
    Description: Tipo da instância EC2
    Type: String
    Default: t2.micro
    AllowedValues:
      - t2.micro
      - t2.small
      - t3.micro
      - t3.small
    ConstraintDescription: Deve ser um tipo de instância EC2 válido.

# ========================
# 🔹 RECURSOS
# ========================
Resources:

  # ------------------------
  # Bucket S3 para armazenar dados
  # ------------------------
  S3BucketDinaellen:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: dinaellen-cloudformation-bucket
      Tags:
        - Key: Projeto
          Value: Desafio-DIO
        - Key: CriadoPor
          Value: Dinaellen Cutrim

  # ------------------------
  # Grupo de segurança para EC2
  # ------------------------
  EC2SecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Permitir acesso SSH (porta 22)
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
      Tags:
        - Key: Projeto
          Value: Desafio-DIO

  # ------------------------
  # Instância EC2
  # ------------------------
  EC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: !Ref InstanceType
      KeyName: !Ref KeyName
      ImageId: ami-0c55b159cbfafe1f0  # Amazon Linux 2 (região us-east-1)
      SecurityGroupIds:
        - !Ref EC2SecurityGroup
      Tags:
        - Key: Name
          Value: EC2-Dinaellen
        - Key: Projeto
          Value: Desafio-DIO

# ========================
# 🔹 SAÍDAS
# ========================
Outputs:
  BucketName:
    Description: Nome do bucket S3 criado
    Value: !Ref S3BucketDinaellen

  EC2InstanceId:
    Description: ID da instância EC2 criada
    Value: !Ref EC2Instance






