# 5 Erros Comuns na Certificação AWS Developer Associate
## E Como Evitá-los Para Passar de Primeira

---

## 📋 Sobre Este E-book

Este e-book foi criado com base em experiência real de preparação para a certificação AWS Developer Associate (DVA-C02). Após alcançar 693 pontos (27 pontos abaixo da aprovação), identifiquei os erros mais críticos que podem fazer a diferença entre passar ou não.

**Objetivo**: Ajudar você a evitar as armadilhas mais comuns e conquistar sua certificação na primeira tentativa.

---

## ❌ Erro #1: Subestimar os Domínios de Security e Troubleshooting

### Por que isso é um problema?

Muitos candidatos focam apenas em Lambda, API Gateway e DynamoDB, negligenciando os domínios de **Security** (26% da prova) e **Troubleshooting** (12% da prova). Juntos, representam quase **40% do exame**!

### O que acontece:

- Você domina os serviços, mas não sabe configurar IAM Roles corretamente
- Conhece Lambda, mas não sabe debugar timeouts ou erros de permissão
- Entende DynamoDB, mas não consegue resolver problemas de throttling

### Como evitar:

✅ **Dedique pelo menos 30% do seu tempo de estudo para Security**
- IAM Policies (diferença entre identidade e recurso)
- Security Groups vs NACLs
- AWS Secrets Manager e Parameter Store
- Cognito User Pools vs Identity Pools
- KMS e criptografia

✅ **Pratique troubleshooting ativo**
- Leia CloudWatch Logs de aplicações com erro
- Configure X-Ray em aplicações serverless
- Entenda códigos de erro HTTP (400 vs 403 vs 500)
- Pratique debugging de Lambda com diferentes runtime errors

### Recursos recomendados:
- AWS Well-Architected Framework (pilar Security)
- Laboratórios práticos de troubleshooting
- Simulados focados nesses domínios

---

## ❌ Erro #2: Confundir Conceitos Similares

### Por que isso é um problema?

A AWS tem vários serviços e conceitos que parecem iguais, mas têm diferenças sutis. O exame ADORA testar essas diferenças!

### Exemplos de confusões comuns:

**1. API Gateway - Tipos de Autenticação:**
- ❌ Confunde: IAM, Cognito User Pools, Cognito Identity Pools, Lambda Authorizer
- ✅ Saiba quando usar cada um

**2. Lambda - Variáveis de Ambiente vs Parameter Store vs Secrets Manager:**
- ❌ Não sabe quando usar cada opção
- ✅ Entenda casos de uso específicos

**3. DynamoDB - Strongly Consistent Read vs Eventually Consistent Read:**
- ❌ Não considera o impacto em custo e performance
- ✅ Saiba as diferenças e quando usar cada tipo

**4. CodeDeploy - Estratégias de Deploy:**
- ❌ Confunde: All-at-once, Rolling, Blue/Green, Canary
- ✅ Conheça as diferenças e casos de uso

### Como evitar:

✅ **Crie tabelas comparativas**

Exemplo:

| Serviço | Quando Usar | Custo | Latência |
|---------|-------------|-------|----------|
| Secrets Manager | Senhas, rotação automática | Mais caro | Baixa |
| Parameter Store | Configurações, valores simples | Grátis (até limite) | Baixa |
| Environment Variables | Valores não-sensíveis, fixos | Grátis | Nenhuma |

✅ **Use mnemônicos**
- **CORS** = Cross-Origin Resource Sharing (sempre pense: navegador → API)
- **HTTPS** vs **HTTP** = Cognito SEMPRE exige HTTPS

✅ **Pratique questões específicas**
- Foque em simulados que testem essas diferenças sutis

---

## ❌ Erro #3: Não Praticar com Laboratórios Hands-On

### Por que isso é um problema?

Você pode ler toda a documentação, mas se nunca configurou um API Gateway com autenticação Cognito na prática, vai errar questões sobre isso.

### O que acontece:

- Você sabe a teoria, mas não reconhece mensagens de erro reais
- Não entende o fluxo completo de uma requisição
- Erra questões sobre configuração porque nunca viu a console AWS

### Como evitar:

✅ **Crie projetos práticos simples:**

**Projeto 1: API Serverless Completa (2-3 horas)**
```
API Gateway → Lambda → DynamoDB
+ Cognito User Pool para autenticação
+ CloudWatch para logs
+ X-Ray para tracing
```

**Projeto 2: Pipeline CI/CD (2 horas)**
```
CodeCommit → CodeBuild → CodeDeploy → Lambda
```

**Projeto 3: Aplicação com Segredos (1 hora)**
```
Lambda busca credenciais do Secrets Manager
Usa Parameter Store para configurações
Aplica IAM Role com least privilege
```

✅ **Use AWS Free Tier**
- A maioria dos serviços tem free tier generoso
- DynamoDB: 25 GB grátis
- Lambda: 1 milhão de requisições/mês grátis
- API Gateway: 1 milhão de chamadas/mês grátis

✅ **Documente seus labs**
- Tire screenshots de erros comuns
- Anote mensagens de erro e soluções
- Guarde seus CloudFormation/SAM templates

### Laboratórios recomendados:
- AWS Skill Builder (gratuito)
- A Cloud Guru / Pluralsight
- Tutoriais Dojo (hands-on labs)

---

## ❌ Erro #4: Ignorar os Limites e Quotas da AWS

### Por que isso é um problema?

O exame adora perguntar sobre limites de serviços e como contorná-los. Muitos candidatos nem sabem que esses limites existem!

### Limites críticos que você PRECISA saber:

**Lambda:**
- Timeout máximo: 15 minutos
- Memória: 128 MB a 10.240 MB
- Tamanho do pacote deployment: 50 MB (zipped), 250 MB (unzipped)
- Concurrent executions: 1000 (por região, soft limit)
- /tmp storage: 512 MB a 10 GB

**API Gateway:**
- Timeout: 29 segundos (importante!)
- Payload máximo: 10 MB
- Rate limiting: 10.000 RPS (soft limit)

**DynamoDB:**
- Item máximo: 400 KB
- Partition key máximo: 2048 bytes
- Query: 1 MB de dados por operação
- Batch operations: 25 itens ou 16 MB

**Step Functions:**
- Execution history: 25.000 eventos
- Execution time: 1 ano

### Como evitar:

✅ **Memorize os limites principais**
- Crie flashcards com os limites mais cobrados
- Foque especialmente em Lambda e API Gateway

✅ **Saiba as soluções de contorno**

Exemplos:
- Lambda timeout (15min) muito curto? → Use Step Functions
- API Gateway timeout (29s)? → Use procesamento assíncrono
- DynamoDB item > 400KB? → Use S3 e guarde referência no DynamoDB
- Lambda concurrent executions excedido? → Solicite aumento de quota ou use Reserved Concurrency

✅ **Questões de exemplo**

*"Sua função Lambda processa vídeos e demora 20 minutos. Qual a melhor solução?"*
- ❌ Aumentar timeout do Lambda
- ✅ Usar Step Functions com múltiplas Lambdas
- ✅ Usar ECS/Fargate para processamento longo

---

## ❌ Erro #5: Não Gerenciar Bem o Tempo Durante o Exame

### Por que isso é um problema?

O exame tem **65 questões** em **130 minutos** (2h10min). Isso significa **2 minutos por questão**. Muitos candidatos gastam muito tempo nas primeiras questões e ficam sem tempo no final.

### O que acontece:

- Você passa 5 minutos em uma questão difícil no início
- Chega nas últimas 10 questões com apenas 10 minutos
- Marca respostas no chute e perde pontos fáceis

### Estatísticas da minha experiência:

```
Questões 1-20:   Gastei 45 minutos (muito tempo!)
Questões 21-50:  Gastei 60 minutos (corrido)
Questões 51-65:  Gastei 25 minutos (muito rápido, errei várias)
```

**Resultado: 693/720 - Reprovado por 27 pontos** 😢

### Como evitar:

✅ **Estratégia de tempo ideal:**

```
Primeira passada (90 minutos):
- Responda todas as questões que você SABE (40-50 questões)
- Marque para revisão as que tiver dúvida
- Não gaste mais de 2 minutos em nenhuma questão

Segunda passada (30 minutos):
- Revise questões marcadas
- Use eliminação de alternativas
- Refine suas respostas

Revisão final (10 minutos):
- Verifique se não deixou nada em branco
- Revise questões que você teve mais dúvida
```

✅ **Técnica de eliminação:**

Para questões difíceis:
1. Elimine 2 alternativas obviamente erradas
2. Entre as 2 restantes, escolha a mais específica/completa
3. Marque para revisão e siga em frente

✅ **Pratique com tempo:**

- Faça simulados SEMPRE com cronômetro
- Simule as condições reais de prova
- Treine fazer 65 questões em 130 minutos

✅ **Sinais de alerta:**

⚠️ Se após 60 minutos você ainda está na questão 25 → ACELERE
⚠️ Se gastou mais de 3 minutos em uma questão → MARQUE e pule
⚠️ Se faltam 20 minutos e você tem 15 questões → CHUTE inteligente

---

## 🎯 Checklist Final: Você Está Pronto?

Antes de agendar seu exame, verifique:

### Conhecimento Técnico:
- [ ] Sei configurar Lambda com diferentes triggers
- [ ] Entendo IAM Policies (identidade vs recurso)
- [ ] Sei a diferença entre Cognito User Pools e Identity Pools
- [ ] Conheço estratégias de deploy (Blue/Green, Canary, Rolling)
- [ ] Sei quando usar SQS vs SNS vs EventBridge
- [ ] Entendo DynamoDB (partition key, sort key, indexes)
- [ ] Sei debugar aplicações com CloudWatch e X-Ray
- [ ] Conheço os limites principais dos serviços

### Preparação Prática:
- [ ] Fiz pelo menos 3 projetos hands-on completos
- [ ] Pratiquei troubleshooting de erros reais
- [ ] Revisei mensagens de erro comuns
- [ ] Criei tabelas comparativas de serviços similares

### Simulados:
- [ ] Fiz pelo menos 5 simulados completos
- [ ] Minha média está acima de 80%
- [ ] Consigo terminar 65 questões em 120 minutos
- [ ] Revisei e entendi TODOS os erros dos simulados

### Domínios Específicos:
- [ ] Security: 26% - Me sinto confiante
- [ ] Development: 32% - Me sinto confiante
- [ ] Deployment: 24% - Me sinto confiante
- [ ] Troubleshooting: 12% - Me sinto confiante
- [ ] Monitoring: 6% - Me sinto confiante

---

## 📚 Recursos Recomendados

### Simulados (ESSENCIAL):
1. **Tutorials Dojo** - Melhor custo-benefício
2. **Whizlabs** - Boas explicações
3. **AWS Skill Builder** - Oficial, gratuito

### Cursos:
1. **Stephane Maarek (Udemy)** - Muito completo
2. **A Cloud Guru** - Bons labs práticos
3. **AWS Skill Builder** - Oficial

### Documentação:
1. AWS Developer Guide (cada serviço)
2. AWS Well-Architected Framework
3. AWS FAQs (especialmente Lambda, API Gateway, DynamoDB)

### Comunidades:
1. Reddit: r/AWSCertifications
2. Discord: AWS Study Group
3. LinkedIn: AWS Certification Study Groups

---

## 🚀 Próximos Passos

1. **Identifique seus pontos fracos** usando simulados
2. **Crie um plano de estudo de 30 dias** focado nos erros comuns
3. **Faça labs práticos** semanalmente
4. **Refaça simulados** até atingir 85%+ consistentemente
5. **Agende seu exame** quando se sentir pronto
6. **Use a estratégia de tempo** no dia da prova

---

## 💪 Mensagem Final

Falhar por 27 pontos foi frustrante, mas me ensinou muito sobre o que o exame realmente cobra. Os 5 erros que listei aqui foram os que me custaram a aprovação.

**A diferença entre passar e reprovar não é quanto você estudou, mas COMO você estudou.**

Foque nos domínios certos, pratique muito, gerencie bem seu tempo e você vai conseguir!

Boa sorte! 🎯

---

## 📧 Contato

Criado por: **Jaine Santos**
GitHub: [JaineSantos0](https://github.com/JaineSantos0)
LinkedIn: [jainejosiane](https://www.linkedin.com/in/jainejosiane/)

**#AWS #Certification #DeveloperAssociate #StudyGuide**

---

**Versão:** 1.0  
**Última atualização:** Novembro 2024  
**Baseado em:** Experiência real de preparação para DVA-C02
