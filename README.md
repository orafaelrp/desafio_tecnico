**Desafio Técnico - Engenheiro SR**

**Descrição**

  Este projeto foi criado para atender a uma demanda técnica fictícia da cooperativa SiCooperative LTDA. Para isso, foram gerados dados simulados para as tabelas ASSOCIADO, CONTA e MOVIMENTO, que foram inseridos em bancos de dados relacionais e não relacionais. Com o ambiente configurado, inicia-se a extração dos dados, seguida pelo tratamento, que inclui o mascaramento e o cruzamento das bases para formar o conjunto final. Esse conjunto é então submetido a testes unitários para garantir sua qualidade. Após ser validado, o resultado é gravado em formato Delta no Lake e exportado para um diretório específico nos formatos Delta e Parquet. As senhas de conexão com os bancos são mantidas de forma segura no Secrets do Databricks. Dessa forma, o processo simula um fluxo de trabalho real, assegurando a qualidade dos dados e a segurança no acesso às informações.

**Pré-requisitos - Plataformas**

  - GitHub - Permissão de acesso para leitura e escrita - 'https://github.com/orafaelrp/desafio_tecnico.git'

  - Databricks - Acesso ao workspace de produção - '/Workspace/Users/orafaelrp@gmail.com/desafio_tecnico'

**Pré-requisitos - Linguagens**

  - Python (pandas, random, faker, datetime, pymongo, psycopg2, pyspark.sql.types, pyspark.sql.functions)

  - SQL

**Funcionalidades**

  - Extração e mascaramento dos dados

  - Validação do objeto por meio de testes unitários

  - Exportação dos dados validados

**Fluxo de execução**

  Este pipeline é acionado automaticamente mediante detecção de novos arquivos fictícios no diretório montado '/Volumes/workspace/default/desafio_tecnico/'. O job ‘job_desafio_tecnico’ inicia a ingestão dos dados oriundos dos bancos relacional Postgres e MongoDB por meio de conectores específicos. Durante o processamento, aplica-se mascaramento nas colunas classificada como sensíveis, seguido pela realização de uma operação de join entre as bases. A coluna UNIQUE_ID sofre anonimização via função hash MD5 para garantir a irreversibilidade dos dados. O dataset resultante é submetido a um conjunto estruturado de testes unitários automatizados que validam integridade referencial. Uma vez aprovado, os dados são persistidos em uma tabela Delta Lake denominada "dados_fake.asso_conta_movi". Depois o objeto é armazenado nos formatos Delta e Parquet no path físico '/Volumes/workspace/default/desafio_tecnico'.
  
**Ordem de execução**

  <img width="864" height="224" alt="image" src="https://github.com/user-attachments/assets/6fab9180-f7ae-4f64-a20c-dd5e837defab" />

**Opcional**

  Power BI - Para uma entrega mais assertiva de um dashboard, é necessária uma agenda de alinhamento para entender as demandas da área de negócios, incluindo o alinhamento dos dados propostos e recebidos. De todo modo, um protótipo foi desenvolvido e está arquivado neste projeto no GitHub.

**Contato**

  Em caso de dúvidas ou contribuições para o projeto, entre em contato pelo e-mail orafaelrp@gmail.com.

**Pontos pessoais**

  Decisões Técnicas - O processamento em nuvem foram escolhidos por oferecer segurança adequada e maior capacidade computacional para o processo como um todo. O fluxo foi desenvolvido como um exemplo prático, demonstrando o processo em si e a resposta obtida. Em um cenário real, vários pontos seriam otimizados para melhor desempenho e menor consumo computacional, reduzindo operações de I/O e custos de processamento. A plataforma Docker não foi utilizada, pois o Databricks tem tudo que é necessário para atender a demanda apresentada na escala encontrada. Contudo em uma escala maior, o Docker pode ser uma alternativa interessante, pois garantiria maior estabilidade ao processo.

  Dificuldades - A configuração dos bancos de dados apresentou alguns desafios. Inicialmente, foram tentados servidores locais (localhost), mas essa abordagem não funcionou, pois o Databricks não se conecta a IPs locais. Neste caso a solução foi a utilização de bancos em nuvem via RDS AWS para PostgreSQL e Atlas para MongoDB.

  Pontos de melhoria - Desenvolver uma documentação clara é sempre um desafio, pois precisa fazer sentido para quem vai consumir e ou manter o projeto. Orientando assim o consumodor em casos de necessidade. Por isso, melhorar a documentação para facilitar a compreensão e manutenção futura é uma grande oportunidade de evolução.
