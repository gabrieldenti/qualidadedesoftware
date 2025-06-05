# Plano de Teste

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
Este plano de teste tem como escopo a validação das funcionalidades principais da aplicação Swag Labs, garantindo que os fluxos críticos da loja, como autenticação, navegação por produtos, gerenciamento do carrinho de compras e finalização de pedidos, estejam funcionando corretamente. Além disso, serão avaliados requisitos não-funcionais como o tempo de resposta e a estabilidade da aplicação.

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
| UC_AddToCart                 | Adicionar item ao carrinho     |
| UC_RemoveFromCart            | Remover item do carrinho       |
| UC_Checkout                  | Preencher informações de checkout e finalizar pedido |

#### 2.2.2 Requisitos funcionais

| Identificador do requisito | Nome do requisito                                                | Casos de uso relacionados    |
|----------------------------|------------------------------------------------------------------|------------------------------|
| RF001                      | Adicionar item ao carrinho                                       | UC_AddToCart                 |
| RF002                      | Remover item do carrinho                                         | UC_RemoveFromCart            |
| RF003                      | Validar formato do CEP (apenas números)                          | UC_Checkout                  |
| RF004                      | Validar campos First Name e Last Name (entrada independente)     | UC_Checkout                  |
| RF005                      | Exibir erro ao prosseguir sem Last Name preenchido               | UC_Checkout                  |

### 2.3 Cenários e Casos de Teste

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

| Requisito | Cenário de Teste                                                       | ID do Caso | Objetivo                                                                                      | Passos                                                                                                                                                                                                                                                   | Resultado Esperado                                                                                               | Status | Evidências/Observações                                                                                                   |
|-----------|-------------------------------------------------------------------------|------------|------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|--------|----------------------------------------------------------------------------------------------------------------------------|
| RF001     | Adicionar item ao carrinho a partir da página inicial de produtos        | CT001      | Verificar que ao clicar em “Add to cart” um produto é inserido no carrinho e o botão muda.    | 1. Acessar https://www.saucedemo.com/v1/index.html<br>2. Fazer login com usuário válido (por ex.: standard_user / secret_sauce)<br>3. Na página de produtos, clicar em “Add to cart” do produto “Sauce Labs Backpack”                             | O botão muda para “Remove”, o contador de itens no ícone do carrinho incrementa para “1” e o produto passa a figurar no carrinho.  | Aberto | Ao clicar em “Add to cart”, o botão não muda, o contador não incrementa e o produto não aparece no carrinho.                |
| RF001     | Tentar adicionar produto específico que não responde ao clique           | CT002      | Identificar comportamento quando um produto não é adicionado ao clicar em “Add to cart”.      | 1. Fazer login<br>2. Na página de produtos, clicar em “Add to cart” do produto “Test.allTheThings() T-Shirt (Red)”                                                                                                                                       | Espera-se que o botão mude para “Remove” e o contador de itens aumente para “1”.                                       | Aberto | O produto não é adicionado ao carrinho, o botão permanece em “Add to cart” e o contador não altera.                       |
| RF002     | Remover item adicionado ao carrinho na página inicial de produtos         | CT003      | Verificar que, após adicionar um item, é possível removê-lo clicando em “Remove”.             | 1. Fazer login<br>2. Clicar em “Add to cart” do “Sauce Labs Bike Light”<br>3. Clicar em “Remove” para o mesmo produto                                                                                                                                   | O botão volta para “Add to cart”, o contador de itens decrementa (para “0”) e o produto sai do carrinho.                 | Aberto | Ao clicar em “Remove”, o botão não muda, o contador não decrementa e o produto permanece no carrinho.                       |
| RF003     | Inserir letras e caracteres especiais no campo CEP durante checkout        | CT004      | Garantir que o campo “Postal Code” aceite somente números.                                      | 1. Adicionar ao menos um item ao carrinho<br>2. Clicar no ícone do carrinho<br>3. Clicar em “Checkout”<br>4. Preencher “First Name” com “Gabriel”<br>5. Preencher “Last Name” com “Denti”<br>6. No campo “Postal Code”, digitar “ABC123!@#” | O campo “Postal Code” deve aceitar apenas dígitos (bloquear ou recusar letras e caracteres especiais). Se inválido, exibir “Error: Postal Code is required”. | Aberto | O campo aceita letras e caracteres especiais sem validação, permitindo “ABC123!@#”.                                         |
| RF004     | Inserir texto nos campos First Name e Last Name para verificar independência | CT005      | Verificar se é possível digitar “First Name” e “Last Name” sem que um sobrescreva o outro.     | 1. Na tela de “Checkout: Your Information”, no campo “First Name”, digitar “Gabriel”<br>2. No campo “Last Name”, digitar “Denti”                                                                                                                         | O campo “First Name” deve manter “Gabriel” e o campo “Last Name” deve armazenar “Denti” de forma independente.           | Aberto | Ao digitar em “Last Name”, o texto sobrescreve o que foi digitado em “First Name”; o campo “Last Name” fica vazio.         |
| RF005     | Prosseguir no checkout sem preencher Last Name e verificar mensagem de erro | CT006      | Verificar se, ao tentar continuar sem “Last Name”, aparece “Error: Last Name is required”.     | 1. Na tela de “Checkout: Your Information”, preencher “First Name” com “Gabriel”<br>2. Deixar “Last Name” vazio<br>3. Preencher “Postal Code” com “01001000”<br>4. Clicar em “Continue”                                                               | A aplicação deve exibir a mensagem “Error: Last Name is required” logo abaixo do campo “Last Name” e impedir o prosseguimento. | Aberto | A mensagem “Error: Last Name is required” aparece, mas, devido ao bug de sobrescrita, não é possível corrigir o campo “Last Name”. |

<small>**Observações gerais**:  
- Todos os casos de teste acima estão com status “Aberto” pois refletem defeitos identificados durante a execução.  
- As evidências devem ser coletadas em capturas de tela ou logs de console, indicando o momento exato da falha.  
- Caso surja a necessidade de testes adicionais (por exemplo, comportamento de inputs vazios ou inputs especiais em outros campos), utilize novos IDs seguindo a mesma numeração sequencial.</small>

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

## 4 – REPORT DE DEFEITO

[Espaço para preenchimento do defeito encontrado seguindo o template acima]

