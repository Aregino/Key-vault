## Criando Key Vault

### Criando com identidade gerenciada para um Workspace específico usando RBAC

#### 1. Acesse o portal do Azure e vá na opção "+" para criar um recurso:

![image](https://github.com/user-attachments/assets/1cc7a0ea-c377-4f9b-b7c2-a64692cd7035)

![image](https://github.com/user-attachments/assets/4cd2e7f0-219a-4a08-97e2-76884d9e4236)

#### 2. Preencha as informações básicas

- Preencha com as informações de acordo com sua assinatura e o grupo de recursos onde deseja criar o Key Vault.

![image](https://github.com/user-attachments/assets/c3b765e8-1892-4b3d-b5aa-85d9207b8922)

- Continue clicando em **Next** até chegar à revisão.

![image](https://github.com/user-attachments/assets/89667dc1-6408-4325-905c-bb62f9dc9bc2)

Clique em **Create**.

#### 3. Configurando permissões de acesso

- Adicione permissões para que o Synapse Workspace tenha acesso ao Key Vault.

![image](https://github.com/user-attachments/assets/1b9a7727-d049-4508-8477-374b743b6346)

Clique em **Add**, selecione as permissões adequadas:

![image](https://github.com/user-attachments/assets/a1d9133f-f7fe-4612-bf4a-dbef4bb58971)

- Agora já temos o Key Vault configurado com as permissões mínimas. O próximo passo é configurar o Workspace.

---

## Configurando o Synapse

#### 1. Criando o Linked Service para acessar o Key Vault

- No Synapse Workspace, vamos criar o **Linked Service** para acessar o Key Vault. Isso é como um "túnel" que só o Synapse pode acessar com as permissões corretas.

![image](https://github.com/user-attachments/assets/254d8ff3-a319-4745-b402-3e40855a3da3)

- Selecione o "+" e escolha a opção **Key Vault**.

![image](https://github.com/user-attachments/assets/311b7822-e42f-4537-be27-42174f1f29ad)

- Defina um nome para o **Linked Service**.
- Selecione sua assinatura e a identidade gerenciada.
- **Importante:** Teste a conexão. Se estiver tudo certo, o Synapse já terá acesso ao Key Vault criado.

---

## Criando um Secret no Key Vault

#### 1. Criando um Secret para testes

- Agora, no Key Vault, vá até a opção **Secrets** e clique em **Generate/Import** para criar um novo Secret.

![image](https://github.com/user-attachments/assets/9c87c95d-c9c4-43e5-93e3-3990d73a164a)

🚨 **Atenção:** Aqui é importante definir o que será armazenado no Secret, como um nome de usuário/senha, uma string JSON, ou uma string de conexão com banco de dados.

Vamos criar um JSON para ser usado com Spark e Dataflow:

```json
{
  "user": "user_exemplo",
  "pass": "123456"
}
```

- Dê um nome para seu Secret e crie um JSON simples como o exemplo acima. Feito isso, vamos fazer a chamada no notebook Spark.

#### 2. Usando o Secret no Notebook Spark

Crie um notebook Spark e execute o seguinte script:

```python
# Importando a biblioteca que dá acesso ao Key Vault
from notebookutils import mssparkutils
import json

# Função para buscar os valores do Key Vault
def get_acces():
    info_str = mssparkutils.credentials.getSecret("nomeDoCofre", "NomeSecret", "NomeLinkedService")
    # Converte a string JSON em um dicionário Python
    acesso = json.loads(info_str)
    # Obtém o usuário e senha
    user = acesso['user']
    password = acesso['pass']
    return user, password

# Chamada da função
user_pbi, password_pbi = get_acces()

# Agora você tem o usuário e a senha armazenados nas variáveis.
```

#### 3. Utilizando no Dataflow

- No Dataflow, você pode criar um novo Linked Service para conexões, como FTP.

![image](https://github.com/user-attachments/assets/95e64a3d-55f9-4afc-8189-6ce5475658fe)

- Em vez de usar um JSON, o Dataflow pode buscar diretamente a senha e aplicá-la ao serviço. Esse método é válido para vários tipos de conexões.

---

## 📚 Documentação

- [Key Vault](https://learn.microsoft.com/pt-br/azure/key-vault/general/basic-concepts)
- [MSSparkUtils](https://learn.microsoft.com/pt-br/fabric/data-engineering/microsoft-spark-utilities)
- [Visão Geral do Key Vault](https://learn.microsoft.com/pt-br/azure/key-vault/general/overview)

---
