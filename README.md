------------------------------------------------------- <ins>**Desafio Técnico**</ins> -------------------------------------------------------


<ins>**Descrição**</ins>

  Este projeto foi criado para atender a uma demanda técnica fictícia. Neste caso, a cooperativa fictícia chamada SiCooperative LTDA necessita de um pipeline de dados para gerar valor junto às áreas de negócio. Para isso, foram gerados dados simulados para as tabelas ASSOCIADO, CONTA e MOVIMENTO, que foram inseridos em bancos de dados relacionais e não relacionais. Uma vez que o ambiente está previamente configurado, é feita a extração dos dados, seguido pelo tratamento, mascaramento e o cruzamento das bases para formar o conjunto final. Esse conjunto é então submetido a testes unitários para garantir sua qualidade. Após a validação, o resultado é gravado em formato Delta no Lake e exportado para um diretório específico nos formatos CSV, Delta e Parquet. 

<ins>**Pré-requisitos - Plataformas**</ins>

  - GitHub privado - Permissão de acesso para leitura e escrita: https://github.com/orafaelrp/desafio_tecnico.git

  - Databricks - Acesso ao workspace de produção: /Workspace/Users/orafaelrp@gmail.com/desafio_tecnico

<ins>**Pré-requisitos - Linguagens**

  - Python (pandas, random, faker, datetime, pymongo, psycopg2, pyspark.sql.types, pyspark.sql.functions)

  - SQL

<ins>**Funcionalidades**</ins>

  - Extração e mascaramento dos dados

  - Validação do objeto por meio de testes unitários

  - Exportação dos dados validados

<ins>**Fluxo de execução**</ins>

  O pipeline é acionado automaticamente mediante detecção de novos arquivos fictícios no diretório montado '/Volumes/workspace/default/desafio_tecnico/'. O job ‘job_desafio_tecnico’ inicia a ingestão dos dados oriundos dos bancos relacional Postgres e MongoDB por meio de conectores específicos. Durante o processamento, aplica-se mascaramento nas colunas classificada como sensíveis(cpf/cnpj, email, número do cartão), seguido pela realização de uma operação de left join entre a tabela MOVIMENTO e as outras bases. Após a coluna UNIQUE_ID recebe colunas especificas que geram a unicidade dos dados apresentados, sofrendo anonimização via função hash MD5 para garantir a irreversibilidade dos dados. O dataset resultante é submetido a um conjunto estruturado de testes unitários automatizados que validam integridade referencial. Uma vez aprovado, os dados são persistidos em uma tabela Delta Lake denominada "dados_fake.asso_conta_movi". Depois o objeto é armazenado nos formatos Delta e Parquet no path físico '/Volumes/workspace/default/desafio_tecnico'.

  - Job name: job_desafio_tecnico
  - Job ID: 208694950806642
  - Job link: https://dbc-4f2eb8a6-531b.cloud.databricks.com/jobs/208694950806642?o=2243053869670813

Para casos de atualização manual, apenas é necessário o clique do botão azul no canto superior direito. O job está parametrizado para executar todo o processo de forma automática.

  <img width="1870" height="885" alt="image" src="https://github.com/user-attachments/assets/57c7f250-94e4-4a6b-a3d3-82f4c647ed2e" />


<ins>**Ordem de execução**</ins>


  <img width="864" height="224" alt="image" src="https://github.com/user-attachments/assets/6fab9180-f7ae-4f64-a20c-dd5e837defab" />


  Tempo médio de processamento: 2 a 3 minutos



<ins>**Contato**</ins>

  Em caso de dúvidas ou contribuições para o projeto, entre em contato pelo e-mail orafaelrp@gmail.com.

------------------------------------------------------- <ins>**Pontos pessoais**</ins> -------------------------------------------------------
          
<ins>**Decisões técnicas - ações realizadas**</ins>
  - Plataformas: O processamento em nuvem foi escolhido por oferecer segurança adequada e maior capacidade computacional para o processo como um todo. Para isso o banco relacional escolhido foi o Postgres/RDS AWS e para não relacional foi o Atlas MongoDB. Já o tratamento dos dados foi realizado via notebook Databricks com linguagem Python e SQL.
  
  - Segurança da informação: Fazendo uso das features já desenvolvidas pelo Databricks, todos os dados de login e senha usados para conectar aos bancos de dados foram criados, armazenados e acessados diretamente pelo recurso Secrets do Databricks. Dessa forma, o processo simulou um fluxo de trabalho real, permitindo a utilização dos dados sem comprometer a segurança ou liberar acessos indevidos ao banco. Assim, foi garantido uma maior proteção e qualidade, tanto dos dados quanto do acesso às informações. Para acessar os dados de acesso e conexão com os bancos informados no processo, segue comando abaixo.

        %run /Workspace/Users/orafaelrp@gmail.com/desafio_tecnico/secrets_databricks

<ins>**Decisões técnicas - ações não realizadas**</ins>
  - Controle de versionamento: Nenhum controle manual de versionamento foi feito, pois o Databricks oferece essa solução pronta e escalável dentro da própria plataforma. Tudo ocorre automaticamente, sem a ativação de uma flag ou mesmo sem a intervenção humana. Todas as versões já escritas estão disponíveis em sistema. É apenas necessário informar qual versão se deseja consultar ao final da query, conforme o exemplo abaixo.

        SELECT * FROM dados_fake.asso_conta_movi VERSION AS OF 12

  - Processamento distribuído: Nenhuma versão do Spark foi ativada, pois este software vem ativado por default dentro do Databricks. Não sendo necessário a sua ativação dentro dos notebooks. Juntamente com o ele, o Pyspark vem automaticamente ativado e atualizado em sistema. Pois é essa lib que faz a conexão entre Spark e os dados do notebook.

  - Logs de qualidade: Não foram criados logs de qualidade nesta versão, pois ainda existe a chance de entregar dados com risco de baixa qualidade ou até mesmo com erro. Do ponto de vista da engenharia, foi preferível entregar o dado apenas em sua total qualidade. Nesse sentido, a tabela apenas é criada se o dado for completamente aprovado nos testes unitários. Contudo esse filtro pode ser ajustado conforme a necessidade. E este for o caso, permitir o nascimento da tabela ainda que com alguns pontos de atenção aceitáveis, uma tabela auxiliar informando a qualidade deste ou de mais objetos deve ser criada em um schema interno para controle de qualidade e governança.

  - Docker: A plataforma Docker não foi utilizada, pois o Databricks já conta com diversas features﻿ testadas e validadas pelo mercado. Dessa forma, para este projeto e nesta escala, a plataforma tem tudo o que é necessário para atender à demanda identificada. Porém, em uma escala maior, o Docker pode ser uma alternativa interessante, já que garantiria maior estabilidade ao processo como um todo.
  
<ins>**Dificuldades**</ins>
  - Configuração de ambiente: A configuração dos bancos de dados apresentou alguns desafios. No início, foram testados servidores locais (localhost), mas essa abordagem não funcionou porque o Databricks não se conecta a IPs locais sem tunelamento ou VPN. Essas soluções foram substituídas pelo processamento em nuvem. Pois a antiga abordagem envolveria custos no processo e certa complexidade na configuração. Levando ainda em consideração que devido ao prazo informado, talvez não fizesse sentido neste momento.

<ins>**Pontos de melhoria**</ins>
  - Documentação README: Fazer uma documentação clara e objetiva nunca é tarefa simples, mas é essencial para o sucesso de qualquer projeto. Por isso, é importante dedicar tempo para deixá-la mais concisa e completa, garantindo assom que o projeto continue evoluindo e sendo útil no futuro. Considerando tudo que foi abordado neste README, essa não poderia ser uma exceção. Melhorar a documentação para facilitar a compreensão e a manutenção é um ponto de meloria.

  - Fluxo de processo: Este fluxo foi desenvolvido como um exemplo prático, demonstrando o processo em si e a resposta obtida a cada passo executado. Em um cenário real, vários pontos seriam otimizados para melhor desempenho e menor consumo computacional, reduzindo o número de operações de I/O e custos de processamento.
    
  - Framework SiCooperative: Diante da demanda por processamento distribuído, qualidade dos dados e segurança da informação, poderia ser desenvolvido um framework de trabalho para atender esses pontos. Conexões a bancos, gerenciamento de senhas e testes unitários poderiam coexistir facilmente em uma única funcionalidade. Assim, esse comando poderia ser importado facilmente em qualquer notebook que necessitasse dessas tarefas.

<ins>**Opcional**</ins>
  - Power BI: Para uma entrega mais assertiva de um dashboard, é necessária uma agenda de alinhamento para entender as demandas da área de negócios, incluindo o alinhamento dos dados propostos e requisitos tecnicos patra essa entrega. De todo modo, um protótipo foi desenvolvido fazendo consumo dos dados trabalhados neste projeto.
