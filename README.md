
## Criando Key Vualt

### Criando com identidade gerencias para um workspaces específico usando RBAC.


#### 1. Acessar o portal Azure  na opção "+"  Create Recurso:

 ![image](https://github.com/user-attachments/assets/1cc7a0ea-c377-4f9b-b7c2-a64692cd7035)

 ![image](https://github.com/user-attachments/assets/4cd2e7f0-219a-4a08-97e2-76884d9e4236)


#### 3. Nas informações básicas 

- ![image](https://github.com/user-attachments/assets/c3b765e8-1892-4b3d-b5aa-85d9207b8922)


- Preenecher com as informações básicas de acordo com sua assinatura e o grupo de recuros que deseja criar o cofre 

- ![image](https://github.com/user-attachments/assets/84c92358-243e-49b2-aaab-5f232eefca73)

- Clicar em next até apresentar a revisão 

![image](https://github.com/user-attachments/assets/89667dc1-6408-4325-905c-bb62f9dc9bc2)

Clicar em create.



#### 4. Permissão de acesso :

![image](https://github.com/user-attachments/assets/1b9a7727-d049-4508-8477-374b743b6346)

Clique e add, pois vamos adicionar as permissões para que o Synapse Workspace tenha acesso 
![image](https://github.com/user-attachments/assets/a1d9133f-f7fe-4612-bf4a-dbef4bb58971)

![image](https://github.com/user-attachments/assets/bfc56bbb-78cd-4f6d-874e-32e11225075c)

![image](https://github.com/user-attachments/assets/72bfd847-24d8-465e-a82e-64367f05b02e)

- Nesse ponto ja temos o Key Vualt e as configurações minimas. Agora pecisamos configurar o Workspace 


#### 4. Configurando o Synapse :

- No Synapse Workspace Vamos criar o Linked de Service para acessar o cofre. É uma especie de túneo em que somente o Synapse pode acesar de acordo com sua permissão.

![image](https://github.com/user-attachments/assets/254d8ff3-a319-4745-b402-3e40855a3da3)
