<span data-ttu-id="8cf18-101">Criar um [arquivo de autenticação](../java-sdk-azure-authenticate.md#mgmt-file) e exportar uma variável de ambiente `AZURE_AUTH_LOCATION` na linha de comando com o caminho completo para o arquivo.</span><span class="sxs-lookup"><span data-stu-id="8cf18-101">Create an [authentication file](../java-sdk-azure-authenticate.md#mgmt-file) and export an environment variable `AZURE_AUTH_LOCATION` on the command line with the full path to the file.</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

<span data-ttu-id="8cf18-102">O arquivo de autenticação é usado para configurar o objeto `Azure` do ponto de entrada objeto usado pelas bibliotecas de gerenciamento para definir, criar e configurar os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8cf18-102">The authentication file is used to configure the entry point `Azure` object used by the management libraries to define, create, and configure Azure resources.</span></span>

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

<span data-ttu-id="8cf18-103">[Saiba mais](../java-sdk-azure-authenticate.md#mgmt-auth) sobre as opções de autenticação ao usar as bibliotecas de gerenciamento do Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="8cf18-103">[Learn more](../java-sdk-azure-authenticate.md#mgmt-auth) about authentication options when using the Azure management libraries for Java.</span></span>