# Implantação técnica — Datamundo

Este documento preserva o contexto técnico do pacote original do projeto, separando os detalhes de implantação da apresentação principal do portfólio.

## Pacote técnico

O pacote completo contempla uma implementação integrada para Google Cloud, BigQuery, Dataform e Looker/Looker Studio. A proposta inclui ingestão, modelagem, governança, testes, dashboards, documentação e infraestrutura.

## Componentes previstos

- `ingestion/`: job Python para ler ZIP/XLSX/CSV, normalizar colunas, gravar Parquet no Cloud Storage e carregar tabelas raw no BigQuery.
- `terraform/`: infraestrutura base no Google Cloud, incluindo buckets, datasets, service accounts, permissões, Cloud Run Job e variáveis.
- `dataform/`: repositório Dataform com declarações raw, staging, marts, assertions e operações.
- `looker/`: modelo LookML, views, explores e dashboards LookML, quando aplicável.
- `sql/`: SQL auxiliar para setup, validação, monitoramento e segurança.
- `docs/`: diagnóstico, catálogo, métricas, governança, runbook e checklist de produção.
- `security/`: plano LGPD, policy tags, mascaramento e classificação de dados.
- `monitoring/`: plano de monitoramento, alertas e controle de custo.
- `scripts/`: comandos de implantação e validação.

## Pontos que precisam ser adaptados em um ambiente real

Para uma implantação completa em produção, é necessário definir ou substituir:

1. `PROJECT_ID`;
2. Região do BigQuery e dos serviços Google Cloud;
3. Nomes dos buckets;
4. Conta de serviço e permissões;
5. Conexão real do Looker/Looker Studio com o BigQuery;
6. Imagem do Cloud Run Job no Artifact Registry, se houver automação de ingestão;
7. Domínio, grupos de usuários e regras de acesso.

## Ordem sugerida de implantação

1. Criar ou escolher um projeto GCP.
2. Validar faturamento, permissões e APIs necessárias.
3. Criar buckets e datasets.
4. Subir os arquivos originais no bucket raw.
5. Executar o processo de ingestão.
6. Criar ou importar o repositório Dataform.
7. Executar staging e marts.
8. Conectar o Looker Studio às tabelas finais.
9. Validar métricas e filtros.
10. Aplicar controles de privacidade antes de compartilhar.

## Observação de segurança

Dados brutos, arquivos com informações pessoais, identificadores de alunos/leads ou detalhes sensíveis não devem ser publicados em repositórios públicos.
