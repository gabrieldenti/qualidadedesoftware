# Plano de Teste
teste
**Nome do Sistema**: Swag Labs  

**Link do site**: https://www.saucedemo.com  

**Data**: 01/06/2025  

*versão 1.0*  

*Autores: Gabriel Denti, Caio Teixeira, Laila Covre, Celso*  

---

## 1 Introdução

### 1.1 Visão Geral da Aplicação  
O sistema Swag Labs é uma aplicação web voltada para simulação de uma loja virtual, permitindo a realização de operações como login, adição e remoção de produtos no carrinho, finalização de compras, entre outros. Seu propósito é fornecer um ambiente de testes para validação de funcionalidades de um e-commerce.

### 1.2 Escopo do Plano de Teste  
Este plano de teste tem como escopo a validação das funcionalidades principais da aplicação Swag Labs, garantindo que os fluxos críticos da loja — como autenticação, navegação por produtos, gerenciamento do carrinho de compras e finalização de pedidos — estejam funcionando corretamente. Além disso, serão avaliados requisitos não-funcionais como o tempo de resposta e a estabilidade da aplicação.

### 1.3 Objetivos do Plano de Teste  
- Garantir que as funcionalidades críticas do sistema estejam funcionando conforme o esperado.  
- Identificar e reportar falhas ou comportamentos inesperados.  
- Avaliar a usabilidade e a performance geral do sistema em diferentes cenários de uso.  

---

## 2 – TESTES

### 2.1 Escopo do Teste  
Esta seção define o alcance dos testes a serem executados. Inclui:  
- Testes de funcionalidades de adição e remoção de itens ao carrinho a partir da página de produtos.  
- Testes de validação de campos no fluxo de checkout (First Name, Last Name e Postal Code).  
- Verificação de mensagens de erro apropriadas para entradas inválidas.  
- Avaliação de requisitos não-funcionais de tempo de resposta (inferior a 2 segundos para carregamento de páginas principais).  

### 2.2 Requisitos a Testar

#### 2.2.1 Casos de uso

| Identificador do caso de uso | Nome do caso de uso            |
|------------------------------|--------------------------------|
| UC_RemoverDoCarrinho            | Remover item do carrinho       |
| UC_Checkout                  | Preencher informações de checkout e finalizar pedido |

#### 2.2.2 Requisitos funcionais

| Identificador do requisito | Nome do requisito                                                | Casos de uso relacionados    |
|----------------------------|------------------------------------------------------------------|------------------------------|
| RF001                      | Remover item do carrinho                                         | UC_RemoveDoCarrinho           |
| RF002                      | Validar formato do CEP (apenas números)                          | UC_Checkout                  |
| RF003                      | Validar campos First Name e Last Name (entrada independente)     | UC_Checkout                  |


---

## 2.3 Cenários e Casos de Teste

#### Estrutura de Caso de Teste

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | Requisito do sistema a ser validado                              |
| **Cenário de Teste**      | Descrição da situação que será validada                          |
| **ID do Caso**            | Identificador único do caso de teste                             |
| **Objetivo**              | Objetivo específico do caso de teste                             |
| **Passos**                | Passos detalhados para execução                                  |
| **Resultado Esperado**    | Comportamento que o sistema deve apresentar após a execução      |
| **Status**                | Passou / Falhou                                                  |
| **Evidências/Observações**| Screenshots, logs ou comentários adicionais                      |

## 2.3 Cenários e Casos de Teste

### CT001 – Remover item adicionado ao carrinho na página de produtos

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF001                                                            |
| **Cenário de Teste**      | Verificar que, após adicionar um item, é possível removê-lo clicando em “Remove” na página de produtos. |
| **ID do Caso**            | CT001                                                            |
| **Objetivo**              | Garantir que a remoção de um produto reflita corretamente no botão (“Remove” → “Add to cart”), no contador do carrinho e na lista de itens. |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **problem_user** / **secret_sauce**).  <br>2. Na lista de produtos, clicar em **“Add to cart”** do produto **“Sauce Labs Bike Light”**.  <br>3. Em seguida, clicar em **“Remove”** para o mesmo produto. |
| **Resultado Esperado**    | - O botão do produto volta a exibir **“Add to cart”**.  <br>- O contador do carrinho diminui de “1” para “0”.  <br>- O produto **“Sauce Labs Bike Light”** não aparece mais na lista de itens do carrinho. |
| **Status**                | Falhou                                                           |
| **Evidências/Observações**| Ao clicar em **“Remove”**, o botão não muda, o contador não decrementa e o produto permanece no carrinho. |

---

### CT002 – Inserir letras e caracteres especiais no campo Postal Code durante checkout

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF002                                                            |
| **Cenário de Teste**      | Garantir que o campo **“Postal Code”** aceite somente números.   |
| **ID do Caso**            | CT002                                                            |
| **Objetivo**              | Validar que o sistema bloqueie ou rejeite entradas que contenham letras e caracteres especiais no campo CEP. |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **standard_user** / **secret_sauce**).  <br>2. Adicionar ao menos um item ao carrinho.  <br>3. Clicar no ícone do carrinho e depois em **“Checkout”**.  <br>4. Preencher **“First Name”** com **“Gabriel”** e **“Last Name”** com **“Denti”**.  <br>5. No campo **“Postal Code”**, digitar **“ABC123!@#”**.  <br>6. Clicar em **“Continue”**. |
| **Resultado Esperado**    | - O campo **“Postal Code”** aceita apenas dígitos (bloquear letras e símbolos).  <br>- Se o formato estiver incorreto, exibir **“Error: Postal Code is required”** e impedir a continuação. |
| **Status**                | Falhou                                                           |
| **Evidências/Observações**| O campo aceita letras e caracteres especiais sem validação, permitindo **“ABC123!@#”** e não apresenta mensagem de erro adequada. |

---

### CT003 – Inserir texto nos campos First Name e Last Name para verificar independência

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF003                                                            |
| **Cenário de Teste**      | Verificar se é possível digitar **“First Name”** e **“Last Name”** sem que um sobrescreva o outro. |
| **ID do Caso**            | CT003                                                            |
| **Objetivo**              | Garantir que os campos de nome e sobrenome funcionem de forma independente, sem troca ou exclusão de conteúdo. |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **problem_user** / **secret_sauce**).  <br>2. Adicionar ao menos um item ao carrinho e avançar até a página **“Checkout: Your Information”**.  <br>3. No campo **“First Name”**, digitar **“Gabriel”**.  <br>4. No campo **“Last Name”**, digitar **“Denti”**. |
| **Resultado Esperado**    | - O campo **“First Name”** mantém o valor **“Gabriel”**.  <br>- O campo **“Last Name”** armazena **“Denti”** sem interferir no campo de nome. |
| **Status**                | Falhou                                                           |
| **Evidências/Observações**| Ao digitar em **“Last Name”**, o texto sobrescreve o que foi digitado em **“First Name”**; o campo **“Last Name”** permanece vazio. |

---

### 2.4 Níveis de Criticidade

| Nível    | Descrição                                               |
|----------|---------------------------------------------------------|
| Crítico  | Impede o uso essencial do sistema                       |
| Alto     | Impacta significativamente funções importantes          |
| Médio    | Afeta funcionalidades secundárias                       |
| Baixo    | Problemas cosméticos ou de baixa relevância             |

### 2.5 SLA de Resolução

| Severidade | Prazo Máximo para Correção |
|------------|----------------------------|
| Crítico    | 24 horas                   |
| Alto       | 72 horas                   |
| Médio      | 5 dias                     |
| Baixo      | 10 dias                    |

---

## 3 – TEMPLATE DE REPORT DE DEFEITOS

**Título do Bug**:  
**ID**:  
**Reportado por**:  
**Data do Relato**:  
**Versão do Sistema**:  
**Prioridade**: [Alta / Média / Baixa]  
**Severidade**: [Crítica / Alta / Média / Baixa]

### Descrição  
[Descrição detalhada do problema]

### Para Reproduzir  
1. …  
2. …  
3. …

### Resultado Esperado  
[Comportamento correto do sistema]

### Resultado Atual  
[Comportamento observado]

### Anexos  
- Capturas de tela  
- Vídeos  
- Logs

### Ambiente de Teste  
- **Desktop**: Sistema Operacional, Navegador, Versão, Rede  
- **Mobile**: Dispositivo, Sistema Operacional, Navegador, Versão, Rede

### Histórico de Status  
- [ ] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

## 4 – REPORT DE DEFEITO [Espaço para preenchimento do defeito encontrado seguindo o template acima]

### Defeito 001

**Título do Bug**: Produto não é removido do carrinho ao clicar em “Remove” na página de produtos  
**ID**: DFT-001  
**Reportado por**: Gabriel Denti
**Data do Relato**:05/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Alta  
**Severidade**: Alta  

**Descrição**  
Ao clicar em “Remove” na página de produtos para um item previamente adicionado, o botão não retorna para “Add to cart”, o contador de itens não decrementa e o produto permanece listado no carrinho.

**Para Reproduzir**  
1. Acessar https://www.saucedemo.com e fazer login com usuário **problem_user** / **secret_sauce”.  
2. Na página de produtos, clicar em **“Add to cart”** do produto **“Sauce Labs Bike Light”**.  
3. Retornar à página de produtos e clicar em **“Remove”** no mesmo produto.  

**Resultado Esperado**  
- Botão volta a exibir **“Add to cart”**.  
- Contador do carrinho diminui de “1” para “0”.  
- Produto não aparece mais no carrinho.  

**Resultado Atual**  
- O botão permanece em **“Remove”**.  
- Contador continua em “1”.  
- Produto ainda aparece no carrinho.

**Anexos**  
[Na pasta deste repositorio, nomeado com o ID do defeito]

**Ambiente de Teste**  
- **Desktop**: Windows 11, Mozilla Firefox.

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 002 

**Título do Bug**: Campo “Postal Code” aceita letras e caracteres especiais durante checkout  
**ID**: DFT-002  
**Reportado por**: Gabriel Denti 
**Data do Relato**:05/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Média  
**Severidade**: Média  

**Descrição**  
O campo “Postal Code” na página de checkout não valida o formato e aceita entradas como “ABC123!@#”, sem exibir mensagem de erro.

**Para Reproduzir**  
1. Acessar https://www.saucedemo.com e fazer login com usuário **standard_user** / **secret_sauce”.  
2. Adicionar item ao carrinho e avançar para “Checkout: Your Information”.  
3. Preencher **“First Name”** com “Gabriel”, **“Last Name”** com “Denti”.  
4. No campo **“Postal Code”**, digitar **“ABC123!@#”**.  
5. Clicar em **“Continue”**.

**Resultado Esperado**  
- Campo bloqueia caracteres não numéricos ou exibe “Error: Postal Code is required”.  
- Não permite avançar sem CEP válido.

**Resultado Atual**  
- Campo aceita “ABC123!@#” sem erro e permite tentar avançar.

**Anexos**  
[Na pasta deste repositorio, nomeado com o ID do defeito]

**Ambiente de Teste**  
- **Desktop**: Windows 11, Mozilla Firefox.

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 003 

**Título do Bug**: Campo “Last Name” sobrescreve conteúdo de “First Name” ao digitar  
**ID**: DFT-003  
**Reportado por**: Gabriel Denti
**Data do Relato**:05/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Alta  
**Severidade**: Alta  

**Descrição**  
Na página de checkout, ao digitar no campo “Last Name”, o valor é inserido no campo “First Name”, apagando o nome digitado anteriormente.

**Para Reproduzir**  
1. Acessar https://www.saucedemo.com e fazer login com usuário **problem_user** / **secret_sauce”.  
2. Adicionar item ao carrinho e avançar para “Checkout: Your Information”.  
3. No campo **“First Name”**, digitar “Gabriel”.  
4. No campo **“Last Name”**, digitar “Denti”.

**Resultado Esperado**  
- “First Name” mantém “Gabriel”.  
- “Last Name” armazena “Denti” sem sobrescrever.

**Resultado Atual**  
- “First Name” fica com “Denti” ou apenas última letra digitada; “Last Name” permanece vazio.

**Anexos**  
[Na pasta deste repositorio, nomeado com o ID do defeito]


**Ambiente de Teste**  
- **Desktop**: Windows 11, Mozilla Firefox.  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

