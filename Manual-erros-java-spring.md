# Manual para dar bom quando der ruim - projetos Spring Java

Uma das boas práticas para a pessoa desenvolvedora Java é não se desesperar diante de bugs na programação, afinal em nossa carreira estes serão sempre muito comuns, e em alguns momentos até vamos precisar provocar esses erros em testes para validar se nossa programação realmente esta nos levando para o caminho assertivo atendendo requisitos do sistema.

Um outro motivo que me levou a pensar nesse material é que quando mais estivermos familiarizados(as)(es) com a leitura de erros no console, mais fácil será a resolução do mesmo.

Para esse material encontraremos mensagens de erro que podem surgir durante o desenvolvimento de uma api em Java com Spring boot, utilizando conexão com banco de dados, JPA para persistência dos dados e Mysql como banco de dados.

Vale lembrar que você também pode contribuir para esse material se tornar ainda mais rico.

## Importando um projeto para o Eclipse

Um dos erros bem comuns para esse momento é tentar importar um projeto com o mesmo nome de outro projeto que já temos em nosso workspace. Sim isso vai gerar um erro que vai te impedir de dar sequencia no processo de importação.

![Erro ao importar projeto com mesmo nome de outro projeto no mesmo workspace](https://i.imgur.com/KwOV5V7.png)

Soluções cabíveis:

1. Renomear o projeto já existente na sua workspace e depois repetir o processo de importar projeto novamente, segue o passo a passo para essa solução:

   a. fechar a janela do Import no [x]; 

   b. clicar com botão direito do mouse sobre o projeto já existente no seu workspace, apontar o cursor do mouse na opção **Refactore** 

   c. clicar com botão esquerdo do mouse na opção **Rename**;

   d. digitar o nome nome para o projeto e digitar **Enter**

   ![Trocando nome de um projeto já existente no seu workspace](https://i.imgur.com/44NaD97.png)
   

## Não carregou todos os diretórios do Spring boot

Na correria do dia a dia, podemos esquecer que as vezes a tecnologia também precisa de seu tempo respeitado, se você sentir que falta algo em seu novo projeto, lembre-se de aguardar ele carregar todas a dependências instaladas. você pode acompanhar as instalações pela barra de status da sua IDE, veja que na imagem a seguir o projeto esta baixando as dependências e esta acusando 26% da instalação apenas.

![Instalando as dependências do projeto](https://i.imgur.com/GlFBw7i.png)

Após aguardar as dependências serem todas instaladas para o projeto vamos conseguir ver todas as camadas padrão já aplicadas ao projeto.

![Estrutura correta do projeto](https://i.imgur.com/2YroG2K.png)

## Recarregar dependências do projeto

Ainda mesmo após as instalações das dependências pode acontecer de devido algum problema com a internet, essa instalação não funcionar conforme o necessário, faltar alguma biblioteca. 

Por algum motivo... em algumas IDE's também é comum ao reiniciar o computador do nada o projeto que esta funcionando apresentar erro, no arquivo pom.xml. para esses casos a solução a seguir pode ajudar.

Para forçar o o download das dependências que faltam podemos seguir as seguintes instruções:

​	a. Clicar com botão direito do mouse sobre o nome do projeto;

​	b. apontar o cursor do mouse na opção Maven;

​	c. clicar na opção Update **Project**;

​	d. na janela seguinte marque as opções: nome do seu projeto e **Force Update of Snapshots/ Releases**;

​	e. clique no botão **OK** e aguarde o download das dependências;

![Forçar download das dependências ](https://i.imgur.com/EwkI52p.png)

![Forçar download das dependências](https://i.imgur.com/G33MQWs.png)

A solução acima também pode ser bem útil quando estamos chamando alguma classe ou método de uma biblioteca que temos certeza, conferindo no pom.xml, que instalamos, mas que ainda assim não funcionam na sua máquina.

## Executar o projeto correto

É importante sempre ao rodar um projeto confirmar se esta executando o projeto correto, já que no dia a dia de uma pessoa desenvolvedora, dependendo da empresa que você vir a trabalhar, podemos estar envolvides em mais de um projeto. Sempre vale apena confirmar o projeto que esta sendo executado no momento.

No console você consegue confirmar o nome do projeto que esta sendo executado, veja a imagem a seguir:

![confirmar a aplicação que esta rodando no servidor no momento](https://i.imgur.com/hshLfWr.png)

Acima temos o nome da aplicação em amarelo no Package Explorer, e podemos notar que é esse mesmo nome que esta no console em execução.

Para evitar erros, você pode executar o projeto de 2(duas) formas:

1. Clicar em executar na barra de ferramentas da IDE e depois clique na seta de seleção de execução de projetos, por ultimo clique no projeto que deseja executar, imagem abaixo. 

   ![selecionar o projeto correto para execução](https://i.imgur.com/HC9zIab.png)

   2. Sim ainda pode ser utilizada a forma de clicar com botão direito sobre o arquivo main() do projeto e executar para executa-lo.

## Ao tentar executar projeto, a porta parece já esta sendo utilizada

Outro problema comum é o console retornar a mensagem dizendo: "Description: Web server failed to start. Port 8080 was already in use.", que indica que a porta que executa a aplicação pela IDE já esta em uso. 
![Mensagem de erro para a porta do projeto](https://i.imgur.com/44skRIf.png)

1. Uma possível causa e já existir uma aplicação sendo executada na IDE. Para isso vamos apenas parar a aplicação em execução.

   a. Para confirmar se temos outro projeto, ou o mesmo projeto já estiver em execução verifique o botão Stop esta ativo em cor "vermelha", segue imagem, note que destacamos o botão em amarelo.

   ![projeto em execução na IDE](https://i.imgur.com/CZMQJNP.png)

   b. Para corrigir o projeto, clique nesse botão **STOP** e execute o seu projeto novamente.

1. Outra possível causa, caso tenha instalados novos softwares em sua máquina ou esteja rodando projetos pela primeira vez no seu computador, é de ter outro app utilizando a porta 8080. Para esse caso devemos configurar outra porta para rodar os projetos.

   

   

## Erro na dependência Mysql

Alguns erros podem acontecer no momento de fazer uso da dependência de banco de dados Mysql, vamos conhecer alguns erros mais comuns.

Lembrando que a leitura do erro deve ser sempre a partir das primeiras linhas de erro, volte a barra de rolagem do console para ter certeza que vai avaliar os erros a partir das primeiras mensagens, já que um erro pode ter efeito cascata trazendo outros erros que na verdade são todos causados pelo primeiro.

```
Mensagem de erro: Application run failed

org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'dataSourceScriptDatabaseInitializer' defined in class path resource [org/springframework/boot/autoconfigure/sql/init/DataSourceInitializationConfiguration.class]: Unsatisfied dependency expressed through method 'dataSourceScriptDatabaseInitializer' parameter 0: Error creating bean with name 'dataSource' defined in class path resource [org/springframework/boot/autoconfigure/jdbc/DataSourceConfiguration$Hikari.class]: Failed to instantiate [com.zaxxer.hikari.HikariDataSource]: Factory method 'dataSource' threw exception with message: Failed to load driver class com.mysql.cj.jdbc.Driver in either of HikariConfig class loader or Thread context classloader
```

Note que o inicio do erro já esta falando "**Unsatisfied dependency**" aqui já temos um indicativo de que a dependência não foi baixada para o projeto, não esta completa ou não foi instalada. Ainda pode ser que a dependência instalada não condiz com a necessária.

 Para esse erro, foi necessário aplicar a dependência correta ao projeto, nesse caso:

1. Verificar se a dependência esta presente em seu arquivo pom.xml e caso não esteja, ou tenha outra que não condiz com a necessária, teremos que aplicar a dependência correta:

```
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
```

​	a. Verifique o arquivo xml para garantir que a dependência acima não esta presente;

​	b. copie o código xml acima;

​	c. cole o código acima entre as tags `<dependencies> </dependencies>` mas sem quebrar nenhuma outra dependência, **ATENÇÃO AOS DETALHES**;

​	d. salve o arquivo e aguarde a finalização do download das dependências;

​	e. caso necessário force o download das dependências utilizando o passo a passo: [clique aqui](https://github.com/jacquelinesantana/Erros-comuns-Java-Spring/blob/main/Manual-erros-java-spring.md#n%C3%A3o-carregou-todos-os-diret%C3%B3rios-do-springboot);

### Erro de no conector do banco de dados, mas executa o projeto

Esse tipo de erro é necessário estar atente para identificar, conforme podemos ver na imagem a seguir o projeto foi "Started", mas ainda assim esta com erro nas linhas acima.

![Erro no driver do banco de dados](https://i.imgur.com/cnYKSAa.png)

Para a correção de tal erro, podemos realizar alguns testes.

1. Verificar se o banco de dados esta acessível no workbench, normalmente esse erro se dá pela falha ou não execução do serviço Mysql no servidor/computador.

2. Verificar se nos serviços do seu sistema operacional o Mysql esta em execução, caso contrário podemos iniciar o serviço, no painel de serviços.

   a. abra o Workbech na sua máquina e tente executar clicando em sua conexão.

   ![workbech conectar com o banco de dados](https://i.imgur.com/hjY1JNx.png)

   b. note que existe a mensagem de "**No connection establised**" no canto inferir esquerdo da tela, indicando que não tem conexão estabelecida.
   
   ![sem conexão estabelecida com banco de dados](https://i.imgur.com/QbdFx3u.png)
   
   c. uma solução é avaliarmos os serviços do sistema operacional e verificar se o serviço do MYSQL esta ativo, digite as teclas **Windows + R**, na caixa do executar digite `services.msc` e clique em **OK**, e clique na opção conforme a imagem a seguir:
   
   ![serviços do sistema operacional](https://i.imgur.com/ZbFcBBv.png)
   
   d. na janela Serviços, procure o nome Mysql entre os serviços, se na linha do serviço estiver sem  a indicação "**Em execução**" e ainda sem estar com a inicialização automática, conforme a imagem a seguir;
   
   ![serviço mysql parado](https://i.imgur.com/oQhI8n9.png)
   
   e. clique com botão direito do mouse sobre o serviço MYSQL, vá até a opção propriedades e clique nesta opção.
   
   ![ativando o serviço para inicialização automática junto ao sistema operacional](https://i.imgur.com/wmq3fXE.png)
   
   f. agora você deve mudar a opção do tipo de inicialização para Automático e clicar no botão **Aplicar** e **OK** 
   
   g. depois disso clique novamente com botão direito do mouse no serviço MYSQL e clique na opção **iniciar**
   
   ![Imgur](https://i.imgur.com/77Wbp9H.png)
   
   h. agora é só executar o projeto novamente na sua IDE.

### Erro de Usuário e/ou senha informados incorretamente

A mensagem de erro a seguir é para o caso de usuário e/ ou senha informados incorretamente, note que a mensagem já indica "Access denied for user 'root@localhost' (using password: YES)".

![Imgur](https://i.imgur.com/rf2h2pY.png)

1. A solução aqui é confirmar os dados de usuário e/ou senha do banco de dados.

   a. abra o arquivo **application.properties** e verifique a digitação dos dados `user` e `password`. Vale também confirmar o nome do host.

   b. salve o arquivo e execute o projeto novamente. Na imagem a seguir temos a informação do local onde o banco esta, no caso na máquina local localhost, destacado em amarelo e as informações de usuário e senha destacadas em vermelho.

   ![Arquivo application properties](https://i.imgur.com/BJrHJo8.png)
   
   

