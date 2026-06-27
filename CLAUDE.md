# CLAUDE.md — Alavo PSA
# Leia este arquivo completo antes de qualquer ação.

---

## QUEM É A ALAVO

A Alavo é uma empresa de saúde corporativa sediada em Caruaru/PE, Brasil.
Implementa programas integrados de saúde (física, mental e social) dentro de empresas,
com equipes multidisciplinares (fisioterapia, nutrição, psicologia, educação física).

**Fundadores:**
- Eduardo Florêncio — CEO, responsável por vendas e estratégia
- Elian — Gestor operacional, co-responsável pela infraestrutura de IA

**Fase atual (junho 2026):** Validação 02
- Primeiro contrato recorrente ativo: ATESeg
- Faturamento acumulado em ~21 meses: ~R$3.000
- Meta: R$1 milhão de faturamento até 2028

---

## ECOSSISTEMA DE PRODUTOS

### Produto principal (B2B)
**Alavo PSA — Programas de Saúde Integrada**
Sistema de gestão dos programas corporativos. Este repositório.
Hospedado em: https://alavo-psa.vercel.app
GitHub: github.com/alavo-tech/alavo-psa

### Produtos autônomos (B2B2C — profissionais assinam para usar com seus pacientes)
- **Alavo Training** — fichas de treino e prescrição de exercícios (já construído)
  GitHub: github.com/alavo-tech/alavo-training
- **Alavo Nutrients** — nutrição e acompanhamento alimentar (a construir)
- **Alavo Mind** — saúde mental e bem-estar emocional (a construir)

### Hub de Saúde
Versões integradas dos três apps acima, disponíveis dentro do PSA para os participantes
das empresas clientes. O PSA é o produto principal; os três módulos são benefícios do programa.

---

## STACK TÉCNICA

- HTML + CSS + JavaScript puro (sem frameworks)
- Chart.js para gráficos
- window.storage com fallback para localStorage
- Deploy via Vercel (conectado ao GitHub — push na main = deploy automático)
- Arquivo único: index.html
- Sem backend por enquanto — tudo no client-side

**NÃO migrar para React, Next.js, banco de dados ou outra stack sem autorização explícita.**
Se uma migração for recomendada, proponha separadamente com justificativa e custo.

---

## REGRAS DE DESENVOLVIMENTO

### Antes de qualquer alteração
1. Leia o index.html completo
2. Mapeie as funções existentes antes de criar novas
3. Nunca remova uma função sem confirmar que não é chamada em nenhum onclick, evento ou outra função
4. Faça backup mental do estado antes de editar

### O que nunca fazer
- Nunca usar `confirm()`, `alert()` ou `prompt()` nativos — o sandbox bloqueia. Use sempre `dlgConfirm()`, `dlgAlert()` e `showToast()`
- Nunca usar `Blob URL` ou `window.open()` para downloads — use data URI com base64
- Nunca duplicar definições de função — verifique se já existe antes de criar
- Nunca colocar `async` em funções que já são `async` (evitar `async async function`)
- Nunca inserir código após `</script>` ou `</html>`
- Nunca renomear chaves do localStorage, IDs de HTML ou valores de currentRole sem criar compatibilidade

### Validação obrigatória antes de entregar
Após qualquer alteração no index.html, rode:
```
node --check index.html
```
Se houver erro de sintaxe, corrija antes de fazer commit.

### Padrão de commit
```
git add .
git commit -m "descrição clara do que foi feito"
git push
```
O Vercel atualiza automaticamente após o push.

---

## PERFIS DE ACESSO DO SISTEMA

| Perfil | Como acessa | currentRole |
|--------|-------------|-------------|
| ADM | Código fixo ALAVO2024 | 'adm' |
| Profissional de saúde | Código individual ALV-XXXX | 'profissional' |
| Empresa/colaborador | Código da empresa EMPNOME-ANO | 'empresa' |

Nunca alterar os valores de currentRole. Nunca remover nenhum dos três acessos.

---

## CHAVES DO STORAGE

Estas chaves existem no sistema. Nunca renomear:
- `profissionais`
- `equipes`
- `empresas`
- `participantes`
- `psas`
- `eventos`
- `posts`
- `materiais`
- `iasc_respostas`
- `historico`

O backup JSON exportado deve sempre incluir todas essas chaves.
Backups com versão "PSA-Alavo-v4" devem continuar sendo aceitos na importação.

---

## FUNÇÕES CRÍTICAS — NÃO REMOVER

- `dlgConfirm()` — substituto do confirm() nativo
- `dlgAlert()` — substituto do alert() nativo
- `showToast()` — notificações rápidas
- `parseLocalDate()` — converte datas sem bug de timezone (não usar new Date('YYYY-MM-DD') diretamente)
- `logAction()` — registra todas as ações no histórico
- `startApp()` — inicializa o app após login ou importação
- `loadPage()` — renderiza as páginas
- `exportarDados()` — exportação JSON
- `importarDados()` — importação JSON com FileReader
- `excluirEmpresa()` — deve permanecer como função standalone async

---

## CONTEXTO ESTRATÉGICO

Eduardo não tira pró-labore ainda. O produto precisa gerar caixa.
Prioridade de decisão técnica:
1. O que mantém o sistema funcionando para o cliente atual (ATESeg)
2. O que acelera a capacidade comercial
3. O que constrói infraestrutura para escala

Quando propor melhorias, sempre indicar:
- Impacto no funcionamento atual
- Risco de quebrar algo
- Complexidade estimada
- Se pode ser feito por etapas

---

## CONTATO E REPOSITÓRIOS

- Email: contato@alavo.net
- Site: alavo.net
- GitHub org: github.com/alavo-tech
- PSA online: https://alavo-psa.vercel.app
- Training online: https://alavo-training.vercel.app (verificar URL atual)
