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
CNAME          domínio personalizado do GitHub Pages
robots.txt
sitemap.xml
```

## Rodando localmente

Não há build. Sirva a pasta com qualquer servidor estático:

```bash
python3 -m http.server 8080
# abra http://localhost:8080
```

## Deploy (GitHub Pages)

O site é publicado direto da branch `main` (raiz) pelo GitHub Pages, sem build e sem workflow.
O arquivo `CNAME` define o domínio `sobre.financemanager-ai.com.br` e o `.nojekyll` desativa o processamento Jekyll.

1. No repositório: **Settings → Pages → Build and deployment**: Source `Deploy from a branch`, branch `main`, pasta `/ (root)`.
2. No DNS de `financemanager-ai.com.br`, crie um registro **CNAME**: nome `sobre`, valor `jeovanedacosta.github.io`.
3. Em **Settings → Pages → Custom domain**, confirme `sobre.financemanager-ai.com.br` e, quando o certificado estiver pronto, marque **Enforce HTTPS**.

Cada push na `main` publica automaticamente.

## Aviso

O FinanceManager é uma ferramenta de apoio e não substitui orientação contábil.