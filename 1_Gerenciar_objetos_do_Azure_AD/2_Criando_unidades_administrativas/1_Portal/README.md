
# Laboratório 2 Bloco 1 - Criando usuários em massa e unidade administrativa utilizando o Portal do Azure

## Objetivos

Neste Laboratório você irá:

+ Tarefa 1: Criar usuários membros em massa no Azure AD
+ Tarefa 1: Criar usuários convidados em massa no Azure AD
+ Tarefa 3: Realize atualizações de usuário em massa
+ Tarefa 2: Criar uma Unidade Administrativa
+ Tarefa 3: Adicionar Recursos à Unidade Administrativa
+ Tarefa 4: Criar usuários convidados em massa no Azure AD


## Tarefa 1: Criando Usuário Membro em massa. 

1. Entre no portal do Azure: **https://portal.azure.com**

2. Na barra de pesquisa procure por **Azure Active Directory** e selecione o serviço.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img1.png)


3. Em seguida selecione **Users** .

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img2.png)

4. Para iniciar a criação de usuários em massa para sua organização, selecione **Bulk create** .

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img4.png)

5. Faça o download do arquivo **.csv**.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img5.png)

6. Para facilitar a edição desse arquivo abra-o em um editor de planilha a sua escolha, como o excel ou planilhas do gogle.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img6.png)


7. Para facilitar a edição desse arquivo abra-o em um editor de planilha a sua escolha, como o excel ou planilhas do google.

>Obs: No **excel** todos o valores devem estar na mesma coluna e separados por virgulas. No **planilhas do google** cada campo deve estar em uma coluna e sem a virgula.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img7.png)

8. Salve o arquivo no formato **.csv**.

>**Obs:** É de extrema importância que salve o arquivo no formato correto.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img8.png)

9. Faça upload do seu arquivo no formato **.csv** .


   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img9.png)

>**Obs:** Ao fazer upload do arquivo o sistema verifica se o formato do arquivo e dos campos estão corretos. Se sim aparecerá que o upload do arquivo foi um sucesso. Caso não esteja aparecendo para você, o erro deve estar na formatação do seu arquivo.

10. Clique em **Submit**.


   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img10.png)
   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img11.png)

>**Obs:** Neste momento o sistema verifica se os campos obrigatórios do arquivo estão devidamente preenchidos e o dominio do email do novos usuários está de acordo com o dominio da organização. Se sim aparecerá que a criação de usuários foi um sucesso. Caso não esteja aparecendo para você, o erro deve estar na ausência de informação nos campos obrigatórios ou no dominio de email dos usuários.

11. Volte a área de usuários e verique se eles foram criados, caso ainda não estejam aparecendo, atualize a página.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img12.png)

## Tarefa 2: Criar uma Unidade Administrativa

1. Entre no portal do Azure: **https://portal.azure.com**


2. Na barra de pesquisa procure por **Azure Active Directory** e selecione o serviço.

   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab1/img1.png)


3. Na página do Azure Active Directory, clique em "Unidades administrativas".
   ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img2.png)


4. Clique em **+Add** para criar uma nova unidade administrativa.
    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img3.png)



5. Preencha as informações solicitadas, como nome e descrição da unidade administrativa.

6. Clique em "Criar" para criar a unidade administrativa.

## Tarefa 3: Adicionar Recursos à Unidade Administrativa

>**Obs:** Com a unidade administrativa criada, você pode começar a adicionar recursos a ela. Por exemplo, você pode adicionar usuários, grupos, aplicativos, políticas etc., dependendo das suas necessidades.

1. Volte ao diretório padrão e selecione **Administrative units**.


    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img12a.png)

2. Preencha os campos como a figura abaixo e em seguida clique em **Next:Assign roles**:

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img13.png)

3. Nessa aba pode-se assinar funções para usuários:

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img14.png)
    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img15.png)

> **Obs:** Nessa aba a funções não são atribuidas a unidade administrativas e sim a cada usuário. As Unidades Administrativas são usadas principalmente para organizar objetos, como usuários, grupos e dispositivos, com base em uma estrutura hierárquica que reflita a organização ou estrutura da empresa. Elas fornecem uma forma de organizar objetos em um contexto de gerenciamento. No entanto, as UAs não têm funcionalidade direta de atribuição de permissões, como os grupos. Alem disso, os usuários que são assinaladas funções nessa aba não são adicionadas diretamente na unidade. A única relação na pespectiva de funções, entre o usuário e a UA, que ele recebeu uma função a partir da criação dela.

4. Nesse laboratório iremos adicionar funções individuais após a criação, apenas selecione **Review e Create** e depois **Create**.
    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img16.png)

5. Uma vez criada, selecione a UA.

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img17.png)


6. Adicione membros a essa UA.

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img18.png)

7. Selecione os usuários e clique em **Select**.

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img19.png)

8. Os usuários do financeiro foram adicionados.

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img20.png)

9. O próximo passo é adicionar funções. Selecione **Roles and administrators**.

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img21.png)

10. Selecione **Printer Administrator**.

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img22.png)

11. Clique em **+Add assignments**, selecione um usuário que esteja na UA e clique em **Add**.

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img23.png)

12. Note que a função foi atribuida.

    >Obs: Mesmo que a UA seja excluída as funções atribuidas ao usuário a partir dela não são excluidas.

    ![Captura de tela de todos os serviços. ](./../../../imagens/Lab2/img23.png)


#### Revisão

Nesse laboratório, você aprendeu:

+ Criar usuários membros em massa no Azure AD
+ Criar uma Unidade Administrativa
+ Adicionar Recursos à Unidade Administrativa