**Desafio Técnico - Engenheiro SR**

* **Descrição**

  Este projeto foi criado para atender a uma demanda técnica fictícia da cooperativa SiCooperative LTDA. Para isso, foram gerados dados fictícios gerando as tabelas ASSOCIADO, CONTA e MOVIMENTO. os dados foram inseridos em bancos de dados relacionais e não relacionais. Com o ambiente configurado, realizamos a extração dos dados, aplicando tratamento, mascaramento e preparando o objeto final. Esse objeto passa por testes unitários e, quando aprovado, é exportado para um diretório específico em formatos delta e parquet. Todas as senhas aqui utilizadas foram armazenadas no Secrets do própria Databricks. Neste sentido o processo busca simular um fluxo real de trabalho, garantindo a qualidade e segurança dos dados manipulados, tanto pela base de dados quanto  pelo acesso do usuário.

* **Pré requisitos - Plataformas**

  - GitHub - Permissão de acesso para leitura e escrita - 'https://github.com/orafaelrp/desafio_tecnico.git'
  - Databricks - Acesso ao workspace de produção - '/Workspace/Users/orafaelrp@gmail.com/desafio_tecnico'

* Pré requisitos - Linguagens
  - Python (pandas, random, faker, datetime, pymongo, psycopg2, pyspark.sql.types, pyspark.sql.functions)
  - SQL

* **Funcionalidades**

  - Mascaramento dos dados
  - Validação de dados com testes unitários
  - Export dos dados validados

* **Fluxo de execução**

  O fluxo que dispara o job 'job_desafio_tecnico' sempre que novos dados fictícios chegam na pasta '/Volumes/workspace/default/desafio_tecnico/'. Esse job está preparado para ler esses dados, fazer o tratamento necessário e seguir todo o processo sozinho, garantindo que tudo aconteça de forma ágil e sem falhas.


* **Ordem de execução**

 <img width="864" height="224" alt="image" src="https://github.com/user-attachments/assets/6fab9180-f7ae-4f64-a20c-dd5e837defab" />
Tempo médio: 2 a 3 minutos

* **Opcional**

  Power BI - Para a entrega masi assertiva de um dashboard, uma agenda de entenimento da necessidade da área de negócio precisa ocrrer. Até mesmo para alinahr os dados porpostos e recebidos. De todo modo, um protótipo foi gerado e arquivado neste projeto do GitHub.

* **Contato**

  Em caso de duvidas e ou contruições para com o projeto, segue e-mail orafaelrp@gmail.com.

* **Pontos pessoais**

  * Decisões Técnicas - O armazenamento e processamento em nuvem foram escolhidos, pois alem de entregar segurança adequada para a informação, tem um maior poder de processamento perante o fluxo. Outro ponto de atenção, é que o fluxo foi escrito a nível de exemplificar o processo. Mostrando como ele ocorre e qual a resposta ele vai apresentar. Em uma situação real para esse projeto, muitos pontos seriam reescritos, priorizando uma melhor performance e menos consumo computacional. Gerando menos menos operações I/O e um menor custo de processamento no fim do trabalho. Não senti necessidade de utilizar Docker, pois acredito que tudo que preciso para realizar este fluxo ficticio, pode ser executado com Databricks. Em caso de escalabilidade deste processo, sim Docker pode ser uma opção interessante pois ele grantiria estabilidade ao processo.

  * Dificuldades - A configuração dos bancos, gerou certa dificuldade. Inicialmente foi tentado bancos com servidor do tipo localhost. Porém este metodo não foi efetivo porque a plataforma Databricks, não faz conexão com ip localHost. Neste sentido, uma nova abordagem foi tentada, onde os bancos foram configurados em nuvem via RDS AWS para Postergres e Atlas para MongoDB.

  * Pontos de melhoria - Escrever uma documentação a este nível é sem duvida algo dificil de se fazer. Pois tudo que se coloca aqui, parece fazer sentido. O ponto é que essa docemnetação tem que fazer sentido para o consumidor, para quem vai depender dela para dar manutenção no projeto. Então sem duvida alguma, escreve uma documentação como essa é um ponto de melhoria. 
