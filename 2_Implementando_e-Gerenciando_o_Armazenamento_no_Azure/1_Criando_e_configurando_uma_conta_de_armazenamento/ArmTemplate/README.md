# Lab 2.1.3 - Criando e configurando uma conta de armazenamento com Arm Template do Azure

## Preparando o ambiente para o Arm no PC local

Você pode usar o Azure PowerShell ou a CLI do Azure para implantar um modelo do Resource Manager. Nesse Lab iremos utilizar o PowerShell.

Caso não tenha o Azure PowerShell no PC Local siga os passos abaixo:

### Abra o powershell como administrador

Execute o comando a seguir:

 **powershell** 
  ```powershell
   Install-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force
   ```
**Obs:** Aguarde o fim das instalações. Pode demorar até 30 minutos dependendo da configuração do pc local.

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
 
Cada recurso do Resource Manager, incluindo uma conta de armazenamento do Azure, deve pertencer a um grupo de recursos do Azure. Um grupo de recursos é um contêiner lógico para agrupar seus serviços do Azure. Ao criar uma conta de armazenamento, você tem a opção de criar um novo grupo de recursos ou usar um grupo de recursos existente. Este tutorial mostra como criar um novo grupo de recursos. 


Execute o comando a seguir:


 **powershell** 
  ```powershell
   $resourceGroup = "<resource-group>"
   $location = "<location>"
   New-AzResourceGroup -Name $resourceGroup -Location $location
   ```
 
Em seguida, crie uma conta de armazenamento. 

Execute o comando a seguir:


 **powershell** 
   ```powershell
   $resourceGroup = "<resource-group>"

   New-AzResourceGroupDeployment -ResourceGroupName $resourceGroup -TemplateUri "https://raw.githubusercontent.com/luizjrlopes/Azure_Help/master/AZ-104/2_Implementando_e-Gerenciando_o_Armazenamento_no_Azure/1_Criando-e-configurando-uma-conta-de-armazenamento/ArmTemplate/template.json"

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
+ Criar uma conta de armazenamento utilizando ARM Template
+ Deletar uma conta de armazenamento




#### Referências

+ https://docs.microsoft.com/pt-br/azure/storage/common/storage-account-create?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json&tabs=template

 $resourceGroup = "testeFinal"
 $location = "westus"
 New-AzResourceGroup -Name $resourceGroup -Location $location