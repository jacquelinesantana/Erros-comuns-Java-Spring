# Manual para dar bom quando der ruim - projetos Spring Java

Uma das boas práticas para a pessoa desenvolvedora Java é não se desesperar diante de bugs na programação, afinal em nossa carreira estes serão sempre muito comuns, e em alguns momentos até vamos precisar provocar esses erros em testes para validar se nossa programação realmente esta nos levando para o caminho assertivo atendendo requisitos do sistema.

Um outro motivo que me levou a pensar nesse material é que quando mais estivermos familiarizados(as)(es) com a leitura de erros no console, mais fácil será a resolução do mesmo.

Para esse material encontraremos mensagens de erro que podem surgir durante o desenvolvimento de uma api em Java com Spring boot, utilizando conexão com banco de dados e JPA para persistência dos dados.

Vale lembrar que você também pode contribuir para esse material se tornar ainda mais rico.

## Importando um projeto para o Eclipse

Um dos erros bem comuns para esse momento é tentar importar um projeto com o mesmo nome de outro projeto que já temos em nosso workspace. Sim isso vai gerar um erro que vai te impedir de dar sequencia no processo de importação.

![Erro ao importar projeto com mesmo nome de outro projeto no mesmo workspace](https://i.imgur.com/KwOV5V7.png)

Soluções cabíveis:

1. Renomear o projeto já existente na sua workspace e depois repetir o processo de importar projeto novamente, segue o passo a passo para essa solução:

   a. fechar a janela do Import no [x]; 

   b. clicar com botão direito do mouse sobre o projeto já existente no seu workspace, apontar o cursor do mouse na opção Refactore 

   c. clicar com botão esquerdo do mouse na opção Rename;

   d. digitar o nome nome para o projeto e digitar Enter

   ![Trocando nome de um projeto já existente no seu workspace](https://i.imgur.com/44NaD97.png)
   

## Não carregou todos os diretórios do Springboot

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

​	c. clicar na opção Update Project;

​	d. na janela seguinte marque as opções: nome do seu projeto e "Force Update of Snapshots/ Releases;

​	e. clique no botão OK e aguarde o download das dependências;

![Forçar download das dependências ](https://i.imgur.com/EwkI52p.png)

![Forçar download das dependências](https://i.imgur.com/G33MQWs.png)

A solução acima também pode ser bem útil quando estamos chamando alguma classe ou método de uma biblioteca que temos certeza, conferindo no pom.xml, que instalamos, mas que ainda assim não funcionam na sua máquina.

## Erro na dependência Mysql

Alguns erros podem acontecer no momento de fazer uso da dependência de banco de dados Mysql, vamos conhecer alguns erros mais comuns.

Lembrando que a leitura do erro deve ser sempre a partir das primeiras linhas de erro, volte a barra de rolagem do console para ter certeza que vai avaliar os erros a partir das primeiras mensagens, já que um erro pode ter efeito cascata trazendo outros erros que na verdade são todos causados pelo primeiro.

Mensagem de erro: Application run failed

org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'dataSourceScriptDatabaseInitializer' defined in class path resource [org/springframework/boot/autoconfigure/sql/init/DataSourceInitializationConfiguration.class]: Unsatisfied dependency expressed through method 'dataSourceScriptDatabaseInitializer' parameter 0: Error creating bean with name 'dataSource' defined in class path resource [org/springframework/boot/autoconfigure/jdbc/DataSourceConfiguration$Hikari.class]: Failed to instantiate [com.zaxxer.hikari.HikariDataSource]: Factory method 'dataSource' threw exception with message: Failed to load driver class com.mysql.cj.jdbc.Driver in either of HikariConfig class loader or Thread context classloader

Note que o inicio do erro já esta falando "Unsatisfied dependency" aqui já temos um indicativo de que a dependência não foi baixada para o projeto, não esta completa ou não foi instalada. Ainda pode ser que a dependência instalada não condiz com a necessária.

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

​	c. cole o código acima entre as tags `<dependencies> </dependencies>` mas sem quebrar nenhuma outra dependência, ATENÇÃO AOS DETALHES;

​	d. salve o arquivo e aguarde a finalização do download das dependências;

​	e. caso necessário force o download das dependências utilizando o passo a passo: [clique aqui]();

