# 🧪 Test Report — Boticario.com.br

> **Projeto:** Testes Manuais de Interface e Usabilidade  
> **Site testado:** [boticario.com.br](https://www.boticario.com.br)  
> **Tipo de teste:** Manual + Performance  
> **Status geral:** ⚠️ Falhas Críticas Identificadas

---

## 📋 Sumário Executivo

Este relatório documenta os defeitos encontrados durante a execução de testes manuais no site **boticario.com.br**. Foram cobradas as áreas de busca, carrinho de compras, cadastro de usuário e performance. Testes de checkout e testes sobre pedidos foram excluídos do escopo por envolverem compra ou pedidos anteriores. Todos os casos de teste estão disponiveis na [Planilha de Testes](https://docs.google.com/spreadsheets/d/1yzHIiVTLtATZ8Pi8iRw9bqCNlBwRrq8HEsG3ITYom_U/edit?usp=sharing). 

| Métrica | Valor |
|---|---|
| Total de casos com falha documentados | 6 |
| Severidade Alta | 3 |
| Severidade Média | 2 |
| Severidade Baixa | 1 |

---

## 🐛 Defeitos Encontrados

### CT-025 — Busca com caracteres especiais: comportamento inconsistente

| Campo | Detalhe |
|---|---|
| **ID** | CT-025 |
| **Módulo** | Busca / Search |
| **Severidade** | 🟢 Baixa |
| **Ambiente** | Desktop |

**Descrição:**  
A funcionalidade de busca apresenta comportamento inconsistente ao receber determinados caracteres especiais como entrada. Caracteres como `@`, `$`, `%` e `*` são ignorados durante a pesquisa, sem retorno de mensagem informativa ao usuário.

**Resultado Esperado:** Exibição de mensagem de "Nenhum resultado encontrado" ou tratamento adequado dos caracteres especiais.  
**Resultado Obtido:** Caracteres especiais são ignorados, podendo retornar resultados genéricos sem relação com a entrada do usuário.

---

### CT-026 — Busca com SQL Injection: bloqueio sem tratamento adequado

| Campo | Detalhe |
|---|---|
| **ID** | CT-026 |
| **Módulo** | Busca / Segurança |
| **Severidade** | 🟠 Média |
| **Ambiente** | Desktop |

**Descrição:**  
Ao inserir uma tentativa de SQL Injection no campo de busca (`OR 1=1 --`), o acesso é negado pelo sistema, o que confirma que não há risco de segurança aparente. No entanto, o bloqueio ocorre de forma abrupta, interrompendo a fluidez da navegação sem apresentar mensagem amigável ao usuário.

**Resultado Esperado:** Acesso negado com mensagem informativa e retorno suave ao estado anterior da busca.  
**Resultado Obtido:** Acesso negado, porém com interrupção brusca do fluxo de navegação, sem feedback claro ao usuário.

---

### CT-041 — Alteração de quantidade de produto: ícone da sacola não atualiza

| Campo | Detalhe |
|---|---|
| **ID** | CT-041 |
| **Módulo** | Carrinho / Sacola de Compras |
| **Severidade** | 🔴 Alta |
| **Ambiente** | Desktop |

**Descrição:**  
Ao adicionar mais de uma unidade do mesmo produto ao carrinho, o contador exibido no ícone da sacola não é atualizado para refletir a quantidade total de itens. O ícone permanece indicando um número inferior ao real, podendo induzir o usuário ao erro.

**Resultado Esperado:** O ícone da sacola deve exibir a quantidade total de produtos adicionados, incluindo múltiplas unidades de um mesmo item.  
**Resultado Obtido:** O número exibido no ícone não aumenta ao adicionar mais unidades do mesmo produto.

---

### CT-071 — Cadastro com CPF já utilizado: duplicidade permitida

| Campo | Detalhe |
|---|---|
| **ID** | CT-071 |
| **Módulo** | Cadastro / Autenticação |
| **Severidade** | 🔴 Alta |
| **Ambiente** | Desktop |

**Descrição:**  
O sistema permite que o mesmo CPF seja cadastrado em duas contas diferentes, sem emitir qualquer alerta ou impedimento. Isso representa uma falha de integridade de dados e pode viabilizar fraudes ou duplicação de identidade na plataforma.

**Resultado Esperado:** O sistema deve validar o CPF no momento do cadastro e impedir o registro caso ele já esteja vinculado a outra conta.  
**Resultado Obtido:** Cadastro concluído com sucesso utilizando um CPF já associado a outra conta existente.

---

### CT-072 — Cadastro com telefone já utilizado: duplicidade permitida

| Campo | Detalhe |
|---|---|
| **ID** | CT-072 |
| **Módulo** | Cadastro / Autenticação |
| **Severidade** | 🔴 Alta |
| **Ambiente** | Desktop |

**Descrição:**  
Assim como ocorre com o CPF, o sistema também permite o cadastro do mesmo número de telefone em mais de uma conta, sem validação ou bloqueio. Isso compromete a singularidade dos dados de contato e pode prejudicar fluxos de recuperação de senha e comunicações.

**Resultado Esperado:** O sistema deve validar o número de telefone e impedir o vínculo com uma nova conta caso já esteja em uso.  
**Resultado Obtido:** Cadastro concluído com sucesso utilizando um número de telefone já associado a outra conta existente.

---

### CT-093 — Performance crítica no Lighthouse mobile (42/100)

| Campo | Detalhe |
|---|---|
| **ID** | CT-093 |
| **Módulo** | Performance / Web Vitals |
| **Severidade** | 🟠 Média |
| **Ambiente** | Mobile (Lighthouse) |

**Descrição:**  
O teste de velocidade de carregamento realizado via Google Lighthouse no ambiente mobile retornou uma pontuação de **42 pontos**, abaixo da meta estabelecida de **≥70 pontos**. Esse resultado indica problemas de otimização que impactam negativamente a experiência do usuário em dispositivos móveis e o posicionamento em mecanismos de busca (SEO).

| Indicador | Meta | Obtido |
|---|---|---|
| Performance Score (Mobile) | ≥ 70 | 42 |

**Impactos possíveis:** Carregamento lento de recursos, imagens não otimizadas para mobile, JavaScript bloqueante, ausência de cache eficiente e layout shifts (CLS elevado).

---

*Relatório gerado para fins de portfólio — Testes executados manualmente, sem automação.*
