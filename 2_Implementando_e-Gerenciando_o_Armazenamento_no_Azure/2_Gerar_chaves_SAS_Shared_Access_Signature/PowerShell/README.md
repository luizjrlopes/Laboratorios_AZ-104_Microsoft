# Lab 2.2.1 - Gerando chaves SAS em uma conta de armazenamento com PowerShell

## Instalando Azure PowerShell no PC Local

Usar o cmdlet **Install-Module** é o método de instalação preferencial para o módulo Az PowerShell. Instale o módulo Az apenas para o usuário atual. Este é o escopo de instalação recomendado. Esse método funciona da mesma forma nas plataformas Windows, macOS e Linux. Execute o seguinte comando de uma sessão do PowerShell:

### Abra o powershell como administrador

Execute o comando a seguir:


 **powershell** 
  ```powershell
   Install-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force
   ```

## Conectando ao Storage Accounts pelo powershell

Execute o comando a seguir:


 **powershell** 
  ```powershell
   Connect-AzAccount -TenantID <digite o ID do tenant>
   ```
 **Exemplo** 
  ```powershell
   Connect-AzAccount -TenantID 11a11a11-1aa1-a11a-11a1-1111a1111a11
   ```

Uma aba de navegador abrirá para que se possa fazer o login em sua conta. faça o login, fecha a tela e volte ao terminal do powershell.

**Obs:** O valor do Tenant ID é encontrado dentro do seu diretório do Azure AD no portal. Se não colocar o tenant ID pode ocorrer erro de autorização na hora de executar os cmdlets.

![image](../../../imagens/imagensTenantIDAAD.png)


## Criar uma conta de armazenamento

Uma conta de armazenamento é um recurso do Azure Resource Manager. O Resource Manager é o serviço de implantação e gerenciamento do Azure. Para obter mais informações, consulte [Visão geral do Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/overview) .
 
Cada recurso do Resource Manager, incluindo uma conta de armazenamento do Azure, deve pertencer a um grupo de recursos do Azure. Um grupo de recursos é um contêiner lógico para agrupar seus serviços do Azure. Ao criar uma conta de armazenamento, você tem a opção de criar um novo grupo de recursos ou usar um grupo de recursos existente. Este tutorial mostra como criar um novo grupo de recursos. Para criar uma conta de armazenamento v2 de uso geral com o PowerShell, primeiro crie um novo grupo de recursos chamando o comando **New-AzResourceGroup** :


Execute o comando a seguir:


 **powershell** 
  ```powershell
   $resourceGroup = "resource-group"
   $location = "location"
   New-AzResourceGroup -Name $resourceGroup -Location $location
   ```

Se você não tiver certeza de qual região especificar para o parâmetro **-Location**, poderá acessar uma lista de regiões com suporte para sua assinatura com o comando **Get-AzLocation** :

Execute o comando a seguir:


 **powershell** 
  ```powershell
   Get-AzLocation | select Location
   ```
Em seguida, crie uma conta de armazenamento. No exemplo abaixo iremos utilizar uma armazenamento do tipo **StorageV2** com sku **Standard** com armazenamento com redundância geográfica com acesso de leitura **(RA-GRS)** usando o comando **New-AzStorageAccount** . Lembre-se de que o nome da sua conta de armazenamento deve ser exclusivo no Azure, portanto, substitua o valor do espaço reservado **\<nomeunico>** pelo seu próprio valor exclusivo:

**Obs:** O nome da conta de armazenamento deve ter entre 3 e 24 caracteres e usar apenas números e letras minúsculas.


Execute o comando a seguir:

 **powershell** 
   ```powershell
   $resourceGroup = "<nome do grupo de recurso>"
   $name = "<nomeunico>"
   $location = "<região>"
   $skuName = "Standard_RAGRS"
   $kind = "StorageV2"

   New-AzStorageAccount -ResourceGroupName $resourceGroup -Name $name `
   -Location $location `
   -SkuName $skuName `
   -Kind $kind
   ```

**Obs:** Note que, caso haja segmentação do comando em múltiplas linhas deve-se colocar no final das linhas um acento craseado.

## Criar um container blob em uma conta de armazenamento com o powershell

### Criar contexto de conta

Execute o comando a seguir:


 **powershell** 
   ```powershell
   $resourceGroup = "<nome do grupo de recurso>"
   $storageAccountName = "<nome da conta de armazenamento criada>"

   $storageAcc=Get-AzStorageAccount -ResourceGroupName  $resourceGroup -Name  $storageAccountName
   $ctx=$storageAcc.Context
   ```
### Criar um container Blob

**powershell** 
   ```powershell
   $containerName= "<nome do container blob>"
   $container = New-AzStorageContainer -Name $containerName -Context $ctx
   ```

## Fazer upload de um arquivo para um container

No seu computador local crie uma pasta no diretório C: chamada “work”.

![image](../../../imagens/Lab1.4_pastaWork.png)

Dentro dessa pasta coloque uma imagem. Em seguida volte ao powershell execute os comandos abaixo:

**powershell** 
   ```powershell
   #A variavel $path deve receber o caminho da pasta do arquivo.
   #Caso queira usar um arquivo de uma pasta diferente do Lab, especifique corretamente o caminho da pasta.
   $path="C:\work\"
   $containerName = "<nome do container blob>"
   $filename= "<nome-da-imagem.jpg>"
   $file= $path + $filename
   Set-AzStorageBlobContent -File $file -Container $containerName -Context $ctx
   ```

## Gerar chave SAS


Para gerar uma chave SAS, é necessário que o usuário possua a permissão da função **"Storage Blob Data Contributor"**. Vamos conceder essa permissão.

### Dar permissão ao usuário

Para dar permissão a um usuário, precisamos do seu **ObjetctID**. Caso não tenha o **ObjetctID** do usuário execute os passo abaixo:

+ Primeiramente, conecte a conta do Azure AD

**powershell** 
   ```powershell
   $name = "storage-account-name"
   $resourceGroup = "resource-group"

   $account = Get-AzStorageAccount -ResourceGroupName $resourceGroup -Name $name
   $account.Location
   $account.Sku
   $account.Kind
   ```
 **powershell** 
  ```powershell
   Connect-AzureAD -TenantID <digite o ID do tenant>
   ```
 **Exemplo** 
  ```powershell
   Connect-AzureAD -TenantID 11a11a11-1aa1-a11a-11a1-1111a1111a11
   ```

**Obs:** O valor do Tenant ID é encontrado dentro do seu diretório do Azure AD no portal. Se não colocar o tenant ID pode ocorrer erro de autorização na hora de executar os cmdlets.

![image](../../../imagens/imagensTenantIDAAD.png)

Obtenha o ObjetctID, a partir do comando abaixo:

**powershell** 
  ```powershell
   Get-AzureADUser
   ```
**Obs:** Esse comando lista todos os usuários em seu diretório. Guarde o valor de seu **ObjetctID**, ele será necesssário na criação da função.

Agora assinalemos a função ao usuário.

Execute o comando a seguir:


 **powershell** 
   ```powershell
  
   $resourceGroup = "<nome do grupo de recurso>"
   $objectIdUser = "<valor do seu ObjetctID>"

   New-AzRoleAssignment -ResourceGroupName $resourceGroup -ObjectId $objectIdUser `
   -RoleDefinitionName "Storage Blob Data Contributor"
   ```

## Gerendo a chave SAS de um Blob

Para finalizar vamos gerar a chave para acessar o blob criado anteriormente via URL.

Execute o comando a seguir:


 **powershell** 
   ```powershell
   # A variável $StartTime deve receber a data de início da validade da chave.
   # A variável $EndTime deve receber a data de fim da validade da chave.
   $StartTime = Get-Date
   $EndTime = $startTime.AddDays(2)

   $containerName = "<nome do container blob>"
   $blobName= "<nome do blob>"
   New-AzStorageBlobSASToken -Context $ctx  -Container  $containerName  -Blob $blobName `
   -Permission racwd -StartTime $StartTime -ExpiryTime $EndTime -FullUri
   ```
Após esse comando um chave será gerada.

 **powershell** 
   ```
   https://<storage-account-name>.blob.core.windows.net/<container-name>/<blob-name>?sv=2020-08-04&st=2022-04-28T09%3A24%3A35Z&se=2022-04-30T09%3A24%3A35Z&sr=b&sp=racwdl&sig=iFTXKMYaZCdf1vz5SxFACJwhitZgJglKeP9WYpSxTL0%3D
   ```

Copie a chave e cole no navegador.
**Obs:** Note que ao colar a chave o arquivo não será visualizado no navegador e sim séra baixado para seu computador. Isso ocorre devido as propriedades da variável contexto na criação do container. 

## Deletar recursos do Laboratório.

Caso deseje deletar o grupo de recurso, execute o comando abaixo.

  **powershell** 
  ```powershell
    $resourceGroup = "<nome do grupo de recurso>"

   Remove-AzResourceGroup -Name $resourceGroup 
   ```

Quando se deleta o grupo de recursos, todos os recursos contidos nele são deletados. Ao fazer esse processo se certifique que todos o s recursos podem ser excluídos. Caso contrário, exclua-os individualmente.  

   

#### Revisão

Nesse laboratório, você aprendeu:

+ Instalar Módulo Azure PowerShell no PC Local
+ Conectar ao Storage Accounts pelo powershell
+ Criar uma conta de armazenamento
+ Criar um container blob em uma conta de armazenamento com o powershell
+ Fazer upload de um arquivo para um container
+ Gerar chave SAS de um Blob





#### Referências

+ https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create?tabs=azure-powershell#code-try-4
+ https://docs.microsoft.com/en-us/powershell/module/az.resources/new-azroleassignment?view=azps-7.5.0
+ https://docs.microsoft.com/en-us/powershell/module/az.storage/new-azstorageblobsastoken?view=azps-7.5.0


