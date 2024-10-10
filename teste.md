## Desafios Enfrentados

### 1. Discovery e Refinamento da Task
- **Processo Desconhecido:**  
  Por ser um processo que ninguém na RT domina totalmente, foi necessário recorrer a horas de documentação, cursos (de API da própria IOX) e busca por pessoas que conhecem o assunto para extrair informações úteis no processo de criação da API.

### 2. Falta de Afinidade com o Processo
- **Desconhecimento do Escopo:**  
  Além de ninguém na RT dominar o processo, eu, que possuo uma base sólida como desenvolvedor e na criação de APIs, também nunca havia provisionado uma API externa do zero dentro da infraestrutura da AWS. A diferença da organização do Itaú em relação ao que eu estava acostumado tornou o desafio ainda mais significativo.

### 3. Segurança
- **Risco da API:**  
  Uma API que recebe dados externos representa um risco para o banco se não for desenvolvida corretamente e seguindo os padrões exigidos pelo Itaú. Foi necessário ter total atenção a cada detalhe, entendendo as etapas com maestria e aplicando corretamente as políticas de segurança e autenticação (mTLS e certificados) para evitar brechas que pudessem abrir portas para acessos mal-intencionados e indesejados.

---

## Erros e Aprendizados

### 1. Validações da API
- **Desafios na Integração:**  
  Ao subir os repositórios no GitHub e passar pelas actions, ocorreram problemas na pipeline que inicialmente impediram a subida da minha branch feature para dev. Aprendi a buscar diversas documentações e entender todo o processo de validação da API conforme os padrões do banco, até conseguir que a action tivesse todos os checks "verdes".

### 2. Falta do Parâmetro Content-Type
- **Erro Comum:**  
  Não incluir o parâmetro `Content-Type: application/json` no contrato da API resultou em mensagens vazias na fila SQS e um erro desconhecido. Esse erro simples tomou algumas horas do meu tempo até que eu identificasse o problema. Essa experiência me proporcionou uma análise crítica minuciosa do código e uma atenção maior ao fluxo, reduzindo a propensão a erros futuros.

### 3. Falta de Escopo Mencionado no Contrato
- **Acesso Negado:**  
  Utilizei um escopo que não existia no portal de credenciais, resultando em erro de acesso negado. Essa experiência me fez entender a importância de ter um contrato de API robusto e validado com atenção, englobando partes de segurança essenciais.

### 4. Erros ao Consumir a API
- **Desafios nos Testes com a NICE:**  
  Durante os testes, enfrentei vários erros de acesso (403). Isso exigiu uma análise detalhada dos logs, o que desenvolveu minhas habilidades de depuração e monitoração no CloudWatch da AWS, permitindo identificar e corrigir problemas, como:
  - Falta do certificado da NICE, que impediu o processo de mTLS no Lambda Authorizer.
  - Escopo ausente no `access_token`, resultando em acesso negado ao tentar consumir.
  - Falta do header `User-Agent`, que provocou bloqueio no firewall da AWS (WAF).

---

## Benefícios da Entrega

### 1. Integração NICE e Mawé
- **Ponte entre as duas ferramentas:**  
  A criação da ponte entre as ligações de acionamento da NICE e o Mawé garante o retorno necessário e correto para seguir com o fluxo do nosso produto, permitindo enviar os dados para uma fila SQS e posteriormente realizar atualizações nos incidentes da ServiceNow através das outras frentes do produto (lambda, fluxos, etc).

### 2. Novos Horizontes
- **Desbravando Novos Assuntos:**  
  Essa entrega possibilitou trazer para a squad uma solução inovadora, tornando a Millennium uma referência na RT para quem precisar provisionar uma API de consumo externo.

### 3. Conhecimento Agregado
- **Aprendizado Contínuo:**  
  Foram praticamente três sprints com essa história no board, desmistificando desde o refinamento até a entrega final do processo completo de criação de uma API Externa. Contribuí além da API, no aprendizado de vários conceitos da nuvem AWS e do Itaú, como segurança, validação, documentação, contrato, monitoração, testes, entre outros.
  
### 4. Benefício Coletivo
- **Compartilhamento de Aprendizados:**  
  Esses aprendizados não apenas beneficiam meus próximos projetos, mas também podem ser compartilhados com a equipe, elevando o nível técnico de toda a squad. Essa troca de conhecimento aumenta nossa capacidade de entrega.

---

## Valor da Entrega

A implementação desta API representa mais do que uma simples solução técnica; ela é uma transformação na maneira como gerenciamos acionamentos e integrações externas. Anteriormente, com a Twilio, enfrentávamos desafios recorrentes que comprometiam a eficiência da operação, resultando em frustrações e ineficiências. 

Com o Mawé, buscamos não apenas resolver esses problemas, mas também estabelecer uma solução robusta, segura e altamente integrada com a NICE (ferramenta de acionamento). Essa mudança traz um controle significativamente maior sobre todo o processo, permitindo um controle dos acionamentos mais fluido e confiável. Ao garantir a eficiência e a segurança, estamos prontos para enfrentar os desafios futuros e oferecer um serviço ainda mais aprimorado.
