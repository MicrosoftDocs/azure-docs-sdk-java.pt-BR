Criar um [arquivo de autenticação](../java-sdk-azure-authenticate.md#mgmt-file) e exportar uma variável de ambiente `AZURE_AUTH_LOCATION` na linha de comando com o caminho completo para o arquivo.

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

O arquivo de autenticação é usado para configurar o objeto `Azure` do ponto de entrada objeto usado pelas bibliotecas de gerenciamento para definir, criar e configurar os recursos do Azure.

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

[Saiba mais](../java-sdk-azure-authenticate.md#mgmt-auth) sobre as opções de autenticação ao usar as bibliotecas de gerenciamento do Azure para Java.