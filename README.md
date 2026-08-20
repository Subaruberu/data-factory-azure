# GitHub e Azure DevOps para Versionamento e Backups

Desafio prático do bootcamp **DIO — Azure** com foco em integrar o **Azure Data Factory (ADF)** a um repositório Git, garantindo versionamento de código, histórico de alterações e backup automático das configurações do pipeline.

## 🎯 Objetivo

Configurar o controle de versão (source control) de uma Data Factory diretamente pelo Git, permitindo:

- Rastreabilidade de todas as mudanças feitas nos pipelines, datasets e linked services;
- Colaboração segura entre múltiplos desenvolvedores sem sobrescrever alterações;
- Backup automático da configuração da Factory a cada commit;
- Separação entre ambiente de desenvolvimento (`collaboration branch`) e ambiente publicado (`publish branch`).

## 🛠️ Tecnologias utilizadas

- **Azure Data Factory** — orquestração e definição dos pipelines
- **GitHub** — repositório remoto para versionamento
- **Git configuration (ADF Studio)** — integração nativa entre Factory e repositório

## ⚙️ Etapas realizadas

1. **Criação do Data Factory** no portal do Azure, dentro do grupo de recursos do projeto.
2. **Configuração do repositório Git** em *Manage > Git configuration*, conectando a Factory ao repositório [`data-factory-azure`](https://github.com/Subaruberu/data-factory-azure).
3. Definição dos parâmetros de conexão:
   - **Repository type:** GitHub
   - **Git repository link:** `https://github.com/Subaruberu/data-factory-azure`
   - **Collaboration branch:** branch principal de desenvolvimento
   - **Publish branch:** `adf_publish` (branch técnica gerada automaticamente para os artefatos de publicação/ARM templates)
   - **Root folder:** `/`
4. **Importação de recursos existentes** para o repositório, garantindo que a configuração atual da Factory fosse versionada desde o primeiro commit.
5. Validação da conexão (*Repo Connected*) e commit inicial salvo no repositório.
6. Publicação (*Publish*) para consolidar as alterações na branch `adf_publish`, gerando os ARM templates de deploy.

## ⚠️ Troubleshooting

Durante a configuração, foi necessário lidar com um erro de conexão (**Internal Server Error**) ao tentar carregar a *collaboration branch*. A causa mais comum é o repositório estar vazio (sem nenhum commit), o que impede o ADF de listar branches existentes. A solução foi garantir um commit inicial no repositório antes de refazer a conexão.

## ✅ Resultado

Com o repositório conectado, todo o desenvolvimento da Factory passa a ser versionado automaticamente: cada *Save* gera um commit na branch de colaboração, e cada *Publish* atualiza a branch `adf_publish` com o estado consolidado da infraestrutura — funcionando como um backup vivo e auditável do ambiente.

## 📚 Referências

- [Documentação oficial — CI/CD no Azure Data Factory](https://learn.microsoft.com/pt-br/azure/data-factory/continuous-integration-delivery)
- Bootcamp Azure — Digital Innovation One (DIO)

---
Desenvolvido por [Willian Fernandes Dias](https://github.com/Subaruberu) como parte do bootcamp Azure da DIO.
