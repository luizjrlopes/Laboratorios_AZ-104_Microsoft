# Lab 2.1.1 - Criando e configurando uma conta de armazenamento com PowerShell

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
   $resourceGroup = "<resource-group>"
   $location = "<location>"
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

## Obter informações de configuração da conta de armazenamento

### Obter o ID do recurso para uma conta de armazenamento

Cada recurso do Azure Resource Manager tem uma ID de recurso associada que o identifica exclusivamente. Certas operações exigem que você forneça o ID do recurso. Você pode obter a ID do recurso para uma conta de armazenamento usando o portal do Azure, PowerShell ou CLI do Azure.


Execute o comando a seguir:


 **powershell** 
   ```powershell
   $name = "storage-account-name"
   $resourceGroup = "resource-group"

   Remove-AzStorageAccount -Name $name -ResourceGroupName $resourceGroup
   (Get-AzStorageAccount -ResourceGroupName $resourceGroup -Name $name).Id
   ```

**saída** 
   ```
/subscriptions/11a11a11-1aa1-a11a-11a1-1111a1111a11/resourceGroups/resource-group/providers/Microsoft.Storage/storageAccounts/storage-account-name
   ```

O valor do ID está representado pelo campo “11a11a11-1aa1-a11a-11a1-1111a1111a1”

### Obtenha o tipo de conta, local ou SKU de replicação para uma conta de armazenamento

O tipo de conta, local e SKU de replicação são algumas das propriedades disponíveis em uma conta de armazenamento. Você pode usar o portal do Azure, PowerShell ou CLI do Azure para exibir esses valores.

Execute o comando a seguir:


 **powershell** 
   ```powershell
   $name = "storage-account-name"
   $resourceGroup = "resource-group"

   $account = Get-AzStorageAccount -ResourceGroupName $resourceGroup -Name $name
   $account.Location
   $account.Sku
   $account.Kind
   ```

## Atualizar uma conta de armazenamento

Para fins de verificação iremos criar uma conta **general-purpose v1**.

Execute o comando a seguir:


 **powershell** 
   ```powershell
   $resourceGroup = "nome do grupo de recurso"
   $name = "nomeunico"
   $location = "região"
   $skuName = "Standard_RAGRS"
   $kind = "Storage"

   New-AzStorageAccount -ResourceGroupName $resourceGroup -Name $name `
   -Location $location `
   -SkuName $skuName `
   -Kind $kind
   ```


Após a criação vamos atualizar a conta. Antes vamos verificar se foi criado como  **general-purpose v1**

Execute o comando a seguir:


 **powershell** 
   ```powershell
   $name = "storage-account-name"
   $resourceGroup = "resource-group"

   $account = Get-AzStorageAccount -ResourceGroupName $resourceGroup -Name $name
   $account.Location
   $account.Sku
   $account.Kind
   ```



Para atualizar uma conta **general-purpose v1** para **general-purpose v2** usando o PowerShell, primeiro atualize o PowerShell para usar a versão mais recente do módulo **Az.Storage**.

Execute o comando a seguir:


 **powershell** 
   ```powershell
   Update-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force
   ```

Execute o comando a seguir para atualizar a conta, substituindo o nome do grupo de recursos, o nome da conta de armazenamento e o nível de acesso à conta desejado.


 **powershell** 
   ```powershell
   $name = "storage-account-name"
   $resourceGroup = "resource-group"
   $accessTier = "Hot/Cool"

   Set-AzStorageAccount -ResourceGroupName $resourceGroup -Name $name -UpgradeToStorageV2 -AccessTier $accessTier
   ```

Verifique se a mudança de tipo ocorreu.

 **powershell** 
   ```powershell
   $name = "storage-account-name"
   $resourceGroup = "resource-group"

   $account = Get-AzStorageAccount -ResourceGroupName $resourceGroup -Name $name
   $account.Location
   $account.Sku
   $account.Kind
   ```


## Deletar uma conta de armazenamento

A exclusão de uma conta de armazenamento exclui a conta inteira, incluindo todos os dados da conta. Certifique-se de fazer backup de todos os dados que deseja salvar antes de excluir a conta.
 
Sob certas circunstâncias, uma conta de armazenamento excluída pode ser recuperada, mas a recuperação não é garantida. Para obter mais informações, consulte  [Recuperar uma conta de armazenamento excluída](https://docs.microsoft.com/en-us/azure/storage/common/storage-account-recover) .
 
Se você tentar excluir uma conta de armazenamento associada a uma máquina virtual do Azure, poderá receber um erro sobre a conta de armazenamento ainda estar em uso. Para obter ajuda para solucionar esse erro, consulte  [Solucionar erros ao excluir contas de armazenamento](https://docs.microsoft.com/en-us/troubleshoot/azure/virtual-machines/storage-resource-deletion-errors) .


Para excluir a conta de armazenamento, execute o comando a seguir:


 **powershell** 
  ```powershell
   $name = "storage-account-name"
   $resourceGroup = "resource-group"

   Remove-AzStorageAccount -Name $name -ResourceGroupName $resourceGroup
   ```

Caso deseje deletar o grupo de recurso, execute o comando abaixo.

  **powershell** 
  ```powershell
   $resourceGroup = "<resource-group>"

   Remove-AzResourceGroup -Name $resourceGroup 
   ```

Quando se deleta o grupo de recursos, todos os recursos contidos nele são deletados. Ao fazer esse processo se certifique que todos o s recursos podem ser excluídos. Caso contrário, exclua-os individualmente.  

   

#### Revisão

Nesse laboratório, você aprendeu:

+ Instalar Módulo Azure PowerShell no PC Local
+ Conectar ao Storage Accounts pelo powershell
+ Criar uma conta de armazenamento
+ Obter informações de configuração da conta de armazenamento
+ Atualizar uma conta de armazenamento
+ Deletar uma conta de armazenamento




#### Referências

+ https://docs.microsoft.com/en-us/azure/storage/common/storage-account-create?tabs=azure-powershell#code-try-4
+ https://docs.microsoft.com/pt-br/azure/storage/common/storage-account-get-info?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json&tabs=powershell

