# FinanceManager — Landing Page

Site estático (HTML, CSS e JS puros) que apresenta o [FinanceManager](https://financemanager-ai.com.br), com foco em Imposto de Renda e DARF.

- **Site:** https://sobre.financemanager-ai.com.br
- **App (destino dos botões):** https://financemanager-ai.com.br

## Estrutura

```
index.html
css/style.css
js/main.js
assets/        favicon.svg e mockups (jpg + webp)
robots.txt
sitemap.xml
.github/workflows/deploy.yml
```

## Rodando localmente

Não há build. Sirva a pasta com qualquer servidor estático:

```bash
python3 -m http.server 8080
# abra http://localhost:8080
```

## Deploy (S3 + CloudFront + GitHub Actions)

O workflow [deploy.yml](.github/workflows/deploy.yml) roda no push para `main` e também manualmente.
Ele só executa quando a variável de repositório `DEPLOY_ENABLED` for `true`.

### O que você precisa criar na AWS

1. **Bucket S3 novo** (exclusivo da landing), com acesso público bloqueado.
2. **Distribuição CloudFront** com o bucket como origem (OAC), `index.html` como objeto raiz e redirecionamento para HTTPS.
3. **Certificado ACM** para `sobre.financemanager-ai.com.br` na região `us-east-1`, associado à distribuição, com o domínio como CNAME alternativo.
4. **DNS:** registro CNAME/ALIAS de `sobre` apontando para o domínio do CloudFront.
5. **Usuário IAM** com permissão `s3:PutObject`, `s3:DeleteObject`, `s3:ListBucket` no bucket e `cloudfront:CreateInvalidation` na distribuição.

### Secrets do GitHub (Settings → Secrets and variables → Actions)

| Nome | Descrição |
|---|---|
| `LANDING_AWS_ACCESS_KEY_ID` | Chave do usuário IAM |
| `LANDING_AWS_SECRET_ACCESS_KEY` | Segredo do usuário IAM |
| `LANDING_AWS_REGION` | Região do bucket (ex.: `sa-east-1`) |
| `LANDING_S3_BUCKET_NAME` | Nome do bucket novo |
| `LANDING_CLOUDFRONT_DISTRIBUTION_ID` | ID da distribuição |

Variável (não secret): `DEPLOY_ENABLED=true`, para ativar o deploy.

## Aviso

O FinanceManager é uma ferramenta de apoio e não substitui orientação contábil.