# Lab 1.3 - Criando usuários e grupos usando o powershell

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


## Gerenciando propriedades de usuários

Para atualizar as propriedades é necessário dados dos usuários como: objectId, displayName, userPrincipalName. Se pode obtê-los pelos comandos abaixo:

### Verificar todos usuários em seu AAD com o PowerShell

Execute o comando a seguir:


 **powershell** 
  ```powershell
   Get-AzureADUser
   ```

### Verificar usuários membros em seu AAD com o PowerShell

Execute o comando a seguir:


 **powershell** 
  ```powershell
   Get-AzureADUser -Filter "UserType eq 'Member'"
   ```

### Verificar usuários convidados em seu AAD com o PowerShell

Execute o comando a seguir:


 **powershell** 
  ```powershell
   Get-AzureADUser -Filter "UserType eq 'Guest'"
   ```

Há outra forma de obter o nome principal do usuário, como username@contoso.com ou a ID do objeto do usuário de forma individual, caso possua o “userName” do usuário.

Execute o comando a seguir:


   **powershell** 
   ```powershell
      Get-AzADUser -StartsWith <userName>
   ```

   **saída** 
   ```
      DisplayName    Id                                  Mail UserPrincipalName
      -----------   --                                   ---- -----------------
      username      11111111-1111-1111-1111-111111111111      username@contoso.com

   ```

ou

Execute o comando a seguir:


   **powershell** 
   ```powershell
      (Get-AzADUser -DisplayName <userName>).id
   ```

   **saída** 
   ```
      11111111-1111-1111-1111-111111111111 

   ```
Vamos abaixo atualizar algumas das informações de um usuário.(As demais podem ser encontradas na referência)

Edite as variáveis ($) que irá usar e delete as que não for (Lembre de excluir a referência da variável no código). Execute o comando a seguir:

 **powershell** 
  ```powershell
  $objectId = "11111111-1111-1111-1111-111111111111"
   $displayName = "Cris Green"
   $userPrincipalName = "chris@contoso.com"
   $PasswordProfile = New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile
   $PasswordProfile.Password = "Password8@"
   $givenName = "Antonio"
   $surname = "Silva"
   $jobTitle = "Suporte"
   $department = "TI"
   $streetAddress = "Rua Nove de Julho"
   $state = "São Paulo"
   $country = "Brazil"
   $physicalDeliveryOfficeName = "São Paulo"
   $city = "São Paulo"
   $postalCode = "04739-010"
   $telephoneNumber = "(00)0000-0000"
   $mobile = "(00)00000-0000"
   $companyName = "Contoso”

   Set-AzureADUser -ObjectId $objectId -AccountEnabled $true -City $city -CompanyName $companyName `
   -Country $country -Department $department -DisplayName $displayName `
   -GivenName $givenName -JobTitle $jobTitle -Mobile $mobile `
   -PasswordProfile $PasswordProfile -PhysicalDeliveryOfficeName $physicalDeliveryOfficeName `
   -PostalCode $postalCode -State $state -StreetAddress $streetAddress -Surname $surname `
   -TelephoneNumber $telephoneNumber -UserPrincipalName $userPrincipalName
   ```

## Gerenciando propriedade de grupos

Para atualizar as propriedades é necessário dados dos grupos. Se pode obtê-los pelos comandos abaixo:

### Verificar todos os grupos em seu AAD com o PowerShell

Execute o comando a seguir:


 **powershell** 
   ```powershell
   Get-AzureADGroup
   ```

### Verificar um grupo específico em seu AAD com o PowerShel

Execute o comando a seguir:


 **powershell** 
   ```powershell
   $objectId = "11111111-1111-1111-1111-111111111111"
   Get-AzureADGroup -ObjectId $objectId
   ```

 **saída** 
   ```
   ObjectId                             DisplayName      Description
   --------                             -----------      -----------
   11111111-1111-1111-1111-111111111111 Grupo Escolhido  Grupo da equipe teste
   ```


### Atualizando um grupo específico em seu AAD com o PowerShell

Vamos abaixo atualizar algumas das informações de um grupo(As demais podem ser encontradas na referência).


Edite as variáveis ($) que irá usar e delete as que não for (Lembre de excluir a referência da variável no código). Execute o comando a seguir:


 **powershell** 
   ```powershell
   $objectId = "11111111-1111-1111-1111-111111111111"
   $description = "Grupo da equipe da área financeira"
   $displayName = "Financeiro"
   Set-AzureADGroup -ObjectId $objectId -Description $description -DisplayName $displayName -MailEnabled $false
   ```



### Define as propriedades de um grupo existente em seu AAD com o PowerShell

Vamos abaixo definir algumas das propriedades de um grupo(As demais podem ser encontradas na referência).
 

Edite as variáveis ($) que irá usar e delete as que não for (Lembre de excluir a referência da variável no código). 

Execute o comando a seguir:

 **powershell** 
   ```powershell
   $objectId = "11111111-1111-1111-1111-111111111111"
   $description = "Grupo da equipe da área financeira"
   $displayName = "Financeiro"
   Set-AzureADGroup -ObjectId $objectId -Description $description -DisplayName $description -MailEnabled $false
   ```



#### Revisão

Nesse laboratório, você aprendeu:

+ Instalar Módulo PowerShell Azure AD no PC Local
+ Conectar ao Azure AD pelo powershell
+ Gerenciar propriedades de usuários
+ Gerenciar propriedade de grupos



#### Referências

+ https://docs.microsoft.com/en-us/powershell/module/azuread/set-azureaduser?view=azureadps-2.0
+ https://docs.microsoft.com/en-us/powershell/module/azuread/get-azureadgroup?view=azureadps-2.0
+ https://docs.microsoft.com/en-us/powershell/module/azuread/set-azureadgroup?view=azureadps-2.0
+ https://docs.microsoft.com/en-us/powershell/module/azuread/set-azureadmsgroup?view=azureadps-2.0

