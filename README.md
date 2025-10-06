# AWS-CloudFormation ☁️

## Sumário
- [Descrição do Projeto](#descrição-do-projeto)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Como Utilizar](#como-utilizar)
- [Recursos Criados](#recursos-criados)
- [Comandos Úteis](#comandos-úteis)
- [Boas Práticas e Observações](#boas-práticas-e-observações)
- [Evidências](#evidências)
- [Licença](#licença)
- [Referências](#referências)

---

## 📘 Descrição do Projeto
Este repositório foi criado como parte do desafio da **Digital Innovation One (DIO)**, com o objetivo de aplicar os conceitos de **Infraestrutura como Código (IaC)** utilizando o **AWS CloudFormation**.  
Durante o laboratório, foi desenvolvida uma infraestrutura automatizada na AWS e documentado todo o processo de aprendizado, boas práticas e desafios enfrentados.

---

## 🧰 Tecnologias Utilizadas
- **AWS CloudFormation**
- **AWS Management Console**
- **AWS CLI**
- **YAML / JSON**
- **Git e GitHub**
- **Markdown**

---

## 🚀 Como Utilizar

### 1. Pré-requisitos
- Conta AWS ativa.
- AWS CLI instalado e configurado (`aws configure`).
- Par de chaves EC2 já criado na sua conta e região AWS.

### 2. Clone o repositório
```sh
git clone https://github.com/dinaellencutrim3/AWS-CloudFormation.git
cd AWS-CloudFormation
```

### 3. Valide o template CloudFormation
```sh
aws cloudformation validate-template --template-body file://template.yaml
```

### 4. Crie o stack
```sh
aws cloudformation create-stack \
  --stack-name stack-dinaellen \
  --template-body file://template.yaml \
  --parameters ParameterKey=KeyName,ParameterValue=<SEU_KEYNAME>
```
> Substitua `<SEU_KEYNAME>` pelo nome do seu par de chaves EC2 (veja em EC2 > Key Pairs).

### 5. Para deletar o stack (remover recursos e evitar custos):
```sh
aws cloudformation delete-stack --stack-name stack-dinaellen
```

---

## 🏗️ Recursos Criados

- **Bucket S3:** Armazenamento de dados do projeto.
- **Instância EC2:** Servidor virtual Linux.
- **Security Group:** Permite acesso SSH à instância EC2.
- **Tags:** Organização e identificação dos recursos criados.

Veja o template completo em [`template.yaml`](template.yaml).

---

## 🛠️ Comandos Úteis

- Validar template:  
  `aws cloudformation validate-template --template-body file://template.yaml`
- Criar stack:  
  `aws cloudformation create-stack --stack-name stack-dinaellen --template-body file://template.yaml --parameters ParameterKey=KeyName,ParameterValue=<SEU_KEYNAME>`
- Deletar stack:  
  `aws cloudformation delete-stack --stack-name stack-dinaellen`

---

## 💡 Boas Práticas e Observações

- **Sempre valide o template** antes de criar o stack.
- Use nomes únicos para buckets S3 para evitar conflitos.
- Restrinja o grupo de segurança para o seu IP público e não para 0.0.0.0/0.
- Remova recursos quando não estiverem mais em uso para evitar cobranças.
- Utilize parâmetros para tornar o template reutilizável.
- Documente o processo e os aprendizados para aprimorar seu portfólio.

---

## 📸 Evidências

As capturas de tela do processo estão disponíveis na pasta `evidencias/`.

---

## 📄 Licença

Este projeto está licenciado sob a licença MIT.

---

## 🔗 Referências

- [Documentação AWS CloudFormation](https://docs.aws.amazon.com/cloudformation/index.html)
- [Documentação AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)
- [Infraestrutura como Código (IaC) na AWS](https://aws.amazon.com/pt/devops/what-is-infrastructure-as-code/)
- [Guia de Boas Práticas CloudFormation](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/best-practices.html)
