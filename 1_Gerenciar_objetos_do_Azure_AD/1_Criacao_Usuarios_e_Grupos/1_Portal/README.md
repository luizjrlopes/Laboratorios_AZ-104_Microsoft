
 # Laboratório 1 Bloco 1 - Gerenciar objetos do Azure AD utilizando o Portal do Azure

## Cenário de laboratório

Para permitir que os usuários de uma empresa se autentiquem usando o Azure AD, você foi encarregado de provisionar usuários e contas de grupo. 

## Objetivos

Neste Laboratório você irá:

+ Tarefa 1: Criar e configurar usuários membros do Azure AD
+ Tarefa 2: Criar e configurar usuários convidados Azure AD
+ Tarefa 3: Criar grupos do Azure AD com associação atribuída e dinâmica


## Tarefa 1: Criando Usuário Membro da Organização 

1. Entre no portal do Azure: **https://portal.azure.com**

2. Na barra de pesquisa procure por **Azure Active Directory** e selecione o serviço.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img1.png)


3. Em seguida selecione **Users** .

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img2.png)

4. Selecione **New User** e em seguida selecione **Create new user** .

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img3.png)

4. Na aba **Basics**, preencha as informações e em seguida selecione **Next:Properties** (Abaixo um exemplo básico):

   | Basics                                 | Values                         |
   |  --                                    | --                             |
   | User principal name                    | **newuser@yourdomain.com**     |
   | Mail nickname                          | :ballot_box_with_check: Derive from user principal name    |
   | Display name                           | **New User**                   |
   | Password                               |**Pa$$u0rd1\*** </br> :black_square_button: **Auto-generate password**   |
   | Account enabled                        |:ballot_box_with_check: Derive from user principal name             |



   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img4.png)

5. Na aba **Properties**, preencha os campos abaixo e selecione **Review + Create** e depois **Create**.
   
   | Properties     | Values                  |
   |  --            | --                      |
   | First name     | **New**                 |
   | Last name      |  **User**               |
   | User type      |  **Member**             |
   | Job title      | **Cloud Administrator** |
   | Company name   | **Cloud Expert**        |
   | Department     | **IT**                  |
   | Usage location     | **Brazil**                  |


   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img5.png)

6. O usuário está criado.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img6.png)

## Tarefa 2: Criando usuário convidado no Portal


1. Volte ao Diretório Padrão do **Azure Active Directory**, em seguida selecione **Users**.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img2.png)

2. Selecione **New User** e em seguida selecione **Invite external user** .

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img7.png)




2. Na aba **Basics**, preencha as informações e em seguida selecione **Next:Properties** (Abaixo um exemplo básico):

   | Basics                          | Values                        |
   |  --                                    | --                             |
   | Email                        | **< seuemail@gmail.com >**                |
   | Display name                                   |  **< Seu Nome >**     |
   | Send invite message                            | :ballot_box_with_check:   |
   | Message                              | **Seja Bem vindo. Agora você poderá colaborar em meu Tenant.**                      |
  
    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img8.png)

>Obs: No campo **Email** digite um email seu como; gmail, outlook ou afins para que receba a solicitação por email do acesso.
 
3. Na aba **Properties**, preencha os campos e selecione **Review + Invite** e depois **Invite**.
   
   
   | Properties     | Values                  |
   |  --            | --                      |
   | First name     | **< Seu Nome >**                 |
   | Last name      |  **< Seu Sobrenome >**               |
   | User type      |  **Guest**             |
   | Job title      | **System Administrator** |
   | Company name   | **Cloud Expert**        |
   | Department     | **IT**                  |
   | Usage location     | **Brazil**                  |

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img9.png)

4. O usuário está criado.
 
      ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img10.png)

## Tarefa 3: Criando grupos do Azure AD com associação atribuída e dinâmica

**Primeira Parte - Iremos adicionar um usuário em um grupo de forma manual utilizando associação a atribuida.** 




6. No menu esquerdo no Diretório Padrão do **Azure Active Directory**, selecione **Groups**.
 ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img16.png)
 




7. Selecione **New group**. 
 ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img17.png)


8. Vamos associar um usuário à um grupo de tipo **Atribuído**. Preencha conforme o campo abaixo e clique em **No members selected** para selecionar um usuário.

   | New Group     | Values                  |
   |  --            | --                      |
   | Group type     | **Security**                 |
   | Group Name      |  **IT Departament**               |
   | Group description      |  **Este grupo engloba todos os usuários ligados a àrea de TI da organização.**             |
   | Azure AD roles can be assigned to the group      | **No** |
   | Membership type   | **Assigned**        |
   | Owners     | **No owners selected**                  |
   


   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img18.png)


9. Digite o nome do primeiro usuário criado na área de pesquisa, em seguida, marque a caixa de seleção ao lado dele e depois em **Select**.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img19.png)

10. No campo **Members** estará mostrando que um usuário foi selecionado. Em seguida selecione **Create**.

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img20.png)

10. O grupo foi criado. Caso ainda não esteja aparecendo basta clicar em **Refresh** para atualizar a página.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img21.png)


**Segunda parte - Iremos adicionar usuário em um grupo de forma automática a partir de um parâmetro utilizando associação dinâmica.** 
>**Obs: Para criação de grupo utilizando associação a atribuída basta uma licença gratuita, porém para criação de grupo utilizando associação dinâmica é necessário uma licença Azure AD Premium P2.**

1. Verifique qual licença do Azure AD está utilizando. Se for como a figura abaixo, siga os passos 2 a 5, caso esteja utilizando uma licença **Premium**, continue a partir do passo 6.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img11.png)

2. No menu esquerdo do **Diretório Padrão**, selecione **Licenses**.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img12.png)

3. Em **Quick tasks**, selecione **Get a free trial**.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img13.png)

4. Em **Azure AD Preemium P2**, selecione **Free trial** e em seguida **Activate**.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img14.png)

5. Volte ao Diretório Padrão do **Azure Active Directory**, em verifique se a licença foi alterada.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img15.png)

6. No menu esquerdo no Diretório Padrão do **Azure Active Directory**, selecione **Groups**.
  ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img16.png)
 

7. Selecione **New group**. 
  ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img17.png)

8. Vamos associar um usuário à um grupo de tipo **Dinâmico**. Preencha conforme o campo abaixo e clique em **add dynamic query** para selecionar um usuário.

   | New Group     | Values                  |
   |  --            | --                      |
   | Group type     | **Security**                 |
   | Group Name      |  **System Administrators**               |
   | Group description      |  **Administradores do sistema.**             |
   | Azure AD roles can be assigned to the group      | **No** |
   | Membership type   | **Dynamic User**        |
   | Owners     | **No owners selected**                  |
   
 
   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img22.png)

9. Preencha as regras de configuração conforme o campo abaixo e depois clique em **Save**.


   | Configure Rule   | Values                     |
   |  --              | --                         |
   | Property         | **jobTitle**               |
   | Operator         |  **equals**                |
   | Value            |  **System Administrator**  |

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img23.png)

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img24.png)

9. Preencha as regras de configuração conforme o campo abaixo e depois clique em **Save**.
   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img22.png)

10. Clique em **Create**.

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img25.png)

11. O grupo foi criado. Caso ainda não esteja aparecendo basta clicar em **Refresh** para atualizar a página.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img26.png)

12. Selecione o grupo **System Administrators**. Clique me Members.


   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img27.png)

13. Note que um usuário foi adicionado automaticamente pelo sistema por atender a condição do grupo.


   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img28.png)

#### Revisão

Nesse laboratório, você aprendeu:

+ Criar e configurar usuários membros do Azure AD
+ Criar e configurar usuários convidados Azure AD
+ Criar grupos do Azure AD com associação atribuída e dinâmica


