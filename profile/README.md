# JurisForce

A JurisForce é uma plataforma de gestão e automação jurídica para advogados e escritórios brasileiros. Reúne o trabalho do dia a dia, da organização de casos e prazos à pesquisa jurídica e à gestão do escritório.

[Conheça a JurisForce](https://jurisforce.com.br/)

## O que você pode fazer

| Área | Recursos |
| --- | --- |
| Operação | Gerencie casos, clientes, prazos e agenda. Acompanhe processos e publicações. |
| Estratégia | Pesquise jurisprudência e jurimetria e elabore teses e peças com assistência de IA. |
| Pesquisa | Faça consultas e investigações patrimoniais e visualize vínculos entre pessoas e empresas. |
| Gestão | Organize as finanças e a equipe do escritório e faça cálculos jurídicos. |

## Para a equipe

- [Aplicação JurisForce](https://github.com/JurisForce/JurisForce) — código da plataforma web, da API e dos apps móveis (acesso restrito).
- [Documentação interna](https://github.com/JurisForce/docs) — planos e decisões do projeto (acesso restrito).

O frontend usa React, TypeScript, Vite e Tailwind CSS. A API usa Node.js, Express e MongoDB; os contratos entre frontend e API são compartilhados com Zod. Os apps iOS e Android usam Capacitor.

### Rodar a aplicação web localmente

Com acesso ao repositório da aplicação, Node.js 20, npm e Docker Compose, clone a aplicação e, na raiz, prepare o ambiente:

```sh
npm ci
npm ci --prefix server --include=dev
ln -sfn ../server/node_modules shared/node_modules
cp -n server/.env.example server/.env
```

Em `server/.env`, use um MongoDB local, configure `JWT_ACCESS_SECRET` e `JWT_REFRESH_SECRET` com valores diferentes de pelo menos 32 caracteres e mantenha `PORT=3001`. Defina `FRONTEND_URL=http://localhost:8090`, inclua essa origem em `CORS_ORIGINS` e deixe `JURISINTEL_INTERNAL_JWT_SECRET` ausente se não for usar essa integração. Não versione o arquivo `.env`.

```sh
docker compose up -d mongo
npm run dev --prefix server
```

Em outro terminal, na raiz do repositório:

```sh
API_PROXY_TARGET=http://localhost:3001 npm run dev
```

Abra [http://localhost:8090](http://localhost:8090). Esse ambiente básico não habilita integrações que dependem de serviços externos.
