# 🏗️ Laboratório 6: Auto Scaling e Load Balancing na AWS

## 📌 Objetivos
Este laboratório ensina como configurar um ambiente web altamente disponível e escalável na **AWS**, utilizando:

✅ **Auto Scaling Groups** – Para gerenciar automaticamente o número de instâncias EC2 conforme a demanda.
✅ **Launch Templates** – Para definir as configurações das instâncias EC2.
✅ **Application Load Balancer** – Para distribuir o tráfego de entrada de maneira inteligente.

---

## 🔧 Pré-requisitos
- Conta AWS ativa
- Permissões IAM: `AmazonEC2FullAccess`, `AmazonEC2AutoScalingFullAccess`, `ElasticLoadBalancingFullAccess`
- Navegador Web

---

## 🚀 Passo a Passo

### 1️⃣ Configuração da VPC
1. Acesse o **Console AWS** e selecione a região `us-east-1`.
2. No menu de pesquisa, digite **VPC** e selecione o serviço.
3. Verifique a **VPC padrão** (`Default VPC = Yes`).
4. Anote o **ID da VPC** (`vpc-xxxxxxxxxxxxxxxxx`).
5. Verifique as **subnets** disponíveis e anote os IDs (`subnet-xxxxxxxxxxxxxxxxx`).

📸 **Print da VPC padrão:** _(Insira o print aqui)_

---

### 2️⃣ Criar um Security Group
1. Acesse **EC2 > Security Groups**.
2. Crie um novo Security Group:
   - **Nome:** `SG-Lab-SeuNome`
   - **Descrição:** HTTP, HTTPS, SSH
   - **VPC:** VPC padrão
   - **Inbound Rules:**
     - HTTP: `0.0.0.0/0`
     - HTTPS: `0.0.0.0/0`
3. Salve as configurações.

📸 **Print do Security Group:** _(Insira o print aqui)_

---

### 3️⃣ Criar um Launch Template
1. Acesse **EC2 > Launch Templates**.
2. Crie um novo **Launch Template** com as configurações:
   - **Nome:** `LT-SeuNome`
   - **AMI:** Amazon Linux 2
   - **Tipo de Instância:** `t2.micro`
   - **Security Group:** `SG-Lab-SeuNome`
   - **User Data:**
     ```bash
     #!/bin/bash
     yum update -y
     yum install -y httpd
     systemctl start httpd
     systemctl enable httpd
     echo "<h1>Servidor Web - Instância: $(hostname -f)</h1>" > /var/www/html/index.html
     ```
3. Salve e crie o template.

📸 **Print do Launch Template:** _(Insira o print aqui)_

---

### 4️⃣ Criar um Auto Scaling Group
1. Acesse **EC2 > Auto Scaling Groups**.
2. Crie um novo **Auto Scaling Group**:
   - **Nome:** `ASG-SeuNome`
   - **Launch Template:** `LT-SeuNome`
   - **VPC:** Selecione a VPC padrão
   - **Subnets:** Escolha pelo menos duas públicas
   - **Capacidade Inicial:** `2`, **Mínima:** `2`, **Máxima:** `4`
   - **Attach to a Load Balancer:** Selecione **Application Load Balancer**
   - **Health Check:** Ativar **Elastic Load Balancer health check**
3. Finalize a criação.

📸 **Print do Auto Scaling Group:** _(Insira o print aqui)_

---

### 5️⃣ Criar um Application Load Balancer
1. Acesse **EC2 > Load Balancers**.
2. Crie um **Application Load Balancer**:
   - **Nome:** `ALB-SeuNome`
   - **Tipo:** Internet-facing
   - **Security Group:** `SG-Lab-SeuNome`
   - **Listeners:** HTTP (porta 80)
   - **Target Group:** Criar um novo target group e adicionar as instâncias do Auto Scaling Group
3. Finalize a configuração.

📸 **Print do Load Balancer:** _(Insira o print aqui)_

---

### 6️⃣ Testando o Ambiente
1. Copie o **DNS do Load Balancer** e acesse pelo navegador.
2. Atualize a página e veja que a instância EC2 muda (balanceamento funcionando!).
3. Monitore o **Auto Scaling Group** e verifique a criação automática de novas instâncias.

📸 **Print do Teste:** _(Insira o print aqui)_

---

## 📌 Conclusão
Parabéns! 🎉 Agora você tem um ambiente web **altamente disponível e escalável** na AWS. Você aprendeu a:
- Criar e configurar um **Auto Scaling Group**
- Utilizar **Launch Templates** para gerenciar instâncias
- Configurar um **Application Load Balancer** para distribuir tráfego
- Testar e validar a escalabilidade da aplicação

🔎 **Dúvidas ou melhorias? Compartilhe suas experiências!** 🚀

#AWS #CloudComputing #AutoScaling #LoadBalancing
