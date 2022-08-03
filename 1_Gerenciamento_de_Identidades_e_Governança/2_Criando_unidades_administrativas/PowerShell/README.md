# Lab 1.2 - Criando unidades administrativas usando o powershell

## Instalando PowerShell para Azure AD no PC Local

### Abra o powershell como administrador

Execute o comando a seguir:


 **powershell** 
  ```powershell
   Install-Module AzureAD
   ```

### Conectando ao Azure AD pelo powershell

Execute o comando a seguir:


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


### Criando unidades administrativas com o PowerShell

Utilização(Pré-requisitos)
+ Licença Azure AD Premium P1 ou P2 para cada administrador de unidade administrativa
+ Licenças gratuitas do Azure AD para membros da unidade administrativa
+ Administrador de função privilegiada ou administrador global
+ Módulo Azure AD ao usar o PowerShell


Para criar estrutura da unidade, execute o comando a seguir:


 **powershell** 
  ```powershell
   $displayName = "Nome da sua unidade"
   $description = "descrição da unidade administrativa"
   New-AzureADMSAdministrativeUnit -DisplayName $displayName -Description $description
   ```



#### Revisão

Nesse laboratório, você aprendeu:

+ Instalar Módulo PowerShell Azure AD no PC Local
+ Conectar ao Azure AD pelo powershell
+ Criar unidades administrativas usando o powershell no Azure AD


#### Referências

+ https://docs.microsoft.com/en-us/azure/active-directory/roles/admin-units-manage
+ https://docs.microsoft.com/en-us/powershell/module/azuread/new-azureadmsadministrativeunit?view=azureadps-2.0

