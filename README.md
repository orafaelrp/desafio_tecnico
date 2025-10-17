**Desafio Técnico - Engenheiro SR**

**Descrição**

Este projeto foi desenvolvido para atender a uma demanda técnica fictícia da cooperativa SiCooperative LTDA. Foram gerados dados fictícios para compor as tabelas ASSOCIADO, CONTA e MOVIMENTO. Esses dados foram inseridos em bancos de dados relacionais e não relacionais. Com o ambiente configurado, realizamos a extração dos dados, aplicando tratamento, mascaramento e preparando o objeto final. Esse objeto passa por testes unitários e, quando aprovado, é exportado para um diretório específico nos formatos Delta e Parquet. Todas as senhas utilizadas foram armazenadas no Secrets do próprio Databricks. O processo simula um fluxo real de trabalho, garantindo a qualidade e segurança dos dados manipulados, tanto na base de dados quanto no controle de acesso do usuário.

**Pré-requisitos - Plataformas**

GitHub - Permissão de acesso para leitura e escrita - 'https://github.com/orafaelrp/desafio_tecnico.git'

Databricks - Acesso ao workspace de produção - '/Workspace/Users/orafaelrp@gmail.com/desafio_tecnico'

**Pré-requisitos - Linguagens**

Python (pandas, random, faker, datetime, pymongo, psycopg2, pyspark.sql.types, pyspark.sql.functions)

SQL

Funcionalidades

Mascaramento dos dados

Validação dos dados por meio de testes unitários

Exportação dos dados validados

Fluxo de execução

O fluxo dispara o job 'job_desafio_tecnico' sempre que novos dados fictícios chegam à pasta '/Volumes/workspace/default/desafio_tecnico/'. Os arquivos no formato CSV são lidos e reescritos nas respectivas tabelas e bancos de dados para os quais estão destinados. Após a escrita, realiza-se o mascaramento dos dados, garantindo a segurança da informação. Em seguida, ocorre um join que unifica os dados em um objeto final. Esse objeto passa por testes unitários que validam seus principais aspectos. Estando aprovado, o objeto é então entregue em tabela Delta com o nome "dados_fake.asso_conta_movi", além de ser salvo nos formatos Delta e Parquet no diretório "/Volumes/workspace/default/desafio_tecnico". O job está estruturado para ler esses dados, realizar o tratamento necessário e executar todo o processo automaticamente, garantindo agilidade e robustez sem falhas.

Ordem de execução

<img width="864" height="224" alt="image" src="https://github.com/user-attachments/assets/6fab9180-f7ae-4f64-a20c-dd5e837defab" />
Opcional

Power BI - Para uma entrega mais assertiva de um dashboard, é necessária uma agenda de alinhamento para entender as demandas da área de negócios, incluindo o alinhamento dos dados propostos e recebidos. De todo modo, um protótipo foi desenvolvido e está arquivado neste projeto no GitHub.

Contato

Em caso de dúvidas ou contribuições para o projeto, entre em contato pelo e-mail orafaelrp@gmail.com.

Pontos pessoais

Decisões Técnicas - O armazenamento e processamento em nuvem foram escolhidos por oferecerem segurança adequada e maior capacidade computacional para o fluxo de dados. O fluxo foi desenvolvido como um exemplo prático, demonstrando o processo e a resposta esperada. Em um cenário real, vários pontos seriam otimizados para melhor desempenho e menor consumo computacional, reduzindo operações de I/O e custos de processamento. Não utilizei Docker por entender que todo o fluxo fictício pode ser executado exclusivamente pelo Databricks. Porém, para escalabilidade, Docker poderia ser uma alternativa interessante, pois garantiria maior estabilidade ao processo.

Dificuldades - A configuração dos bancos de dados apresentou desafios. Inicialmente, foram tentados servidores locais (localhost), mas essa abordagem não funcionou, pois o Databricks não se conecta a IPs locais. Assim, optou-se por bancos em nuvem via RDS AWS para PostgreSQL e Atlas para MongoDB.

Pontos de melhoria - Desenvolver uma documentação clara é sempre um desafio, pois precisa fazer sentido para quem vai consumir e manter o projeto. Por isso, melhorar a documentação para facilitar a compreensão e manutenção futura é uma grande oportunidade de evolução.
