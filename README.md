<div align="center" style="font-family: Arial, sans-serif; font-size: 20px; line-height: 1.5;">

# 🌟 **Curso Dpcn-EDN** 🌟
# 🌟 Solutions Architect Associate  🌟

###
<a href="https://escoladanuvem.org"><a href="https://aws.amazon.com/pt/?nc2=h_lg">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/93/Amazon_Web_Services_Logo.svg/2560px-Amazon_Web_Services_Logo.svg.png" width="180" alt="AWS Logo">
</a>
<img src="https://miro.medium.com/v2/resize:fit:512/0*81xCYukT_2jKzxgJ.png" width="80" alt="AWS Logo">- <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSBfRQV8LLwGpQciyGQ2drjckBDVvZCECVdzA&s" width="80" alt="AWS Logo">-<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ47Ji1yhUawSLNBXPp8UERlP7nKo3d1f2EKw&s" width="80" alt="AWS Logo">- 
    <img src="https://github.com/HalleyVeras/Escola_da_Nuvem/blob/main/Documentos/download%20(4)_processed.png?raw=true" width="210" alt="Second Image">
</a>
</div>


# 🏗️ Laboratório 6: Auto Scaling e Load Balancing na AWS

**Turma:** Dpcn 07  
**Aluno:** Halley Veras 
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

📸 **Print da VPC padrão:** 
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/vpc_painel.jpg?raw=true">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/vpc_resourcemap.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/vpc_copiado.jpg?raw=true" width="400" alt="AWS Logo">-



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

📸 **Print do Security Group:** 

<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/create_security_group_01_basic%20details.jpg?raw=true">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/create_security_group_02_inboundRoules.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/create_security_group_03_outbound_padr%C3%A3o.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos1/create_security_group_04_sucess.jpg?raw=true" width="400" alt="AWS Logo">-

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

📸 **Print do Launch Template:** 

<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos2/create_templates_01_painel.jpg?raw=true">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos2/create_templates_02_description.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos2/create_templates_03_applicationandImages.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos2/create_templates_04_instacetype.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos2/create_templates_05_keypair.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos2/create_templates_06_networkSettings.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos2/create_templates_07_advaceddetails.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos2/create_templates_08_sucess.jpg?raw=true" width="400" alt="AWS Logo">-

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

📸 **Print do Auto Scaling Group e Load Balancer:** 

<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_01.jpg?raw=true">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_02_chooselaunchtemplate.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_03_Network.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_04_Integrate.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_05_Integrate.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_06_createtargetgroup.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_07_healthchecks.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_08_configuregroup.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_09_addnotification.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_10_addtags.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_11_Review.jpg?raw=true" width="400" alt="AWS Logo">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/create_autoscaling_12_Review.jpg?raw=true" width="400" alt="AWS Logo">-

---

### 5️⃣ Testando o Ambiente

1. Copie o **DNS do Load Balancer** e acesse pelo navegador.
2. Atualize a página e veja que a instância EC2 muda (balanceamento funcionando!).
3. Monitore o **Auto Scaling Group** e verifique a criação automática de novas instâncias.

📸 **Print do Teste:**
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/task_01.jpg?raw=true">-
<img src="https://github.com/HalleyVeras/Laboratorio6_CursoDpcn_EDN/blob/main/arquivos3/task_02.jpg?raw=true">-

---

🔎 **Dúvidas ou melhorias? Compartilhe suas experiências!** 🚀

#AWS #CloudComputing #AutoScaling #LoadBalancing
