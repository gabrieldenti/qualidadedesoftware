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

| Identificador do caso de uso | Nome do caso de uso                                     |
| ---------------------------- | ------------------------------------------------------- |
| UC\_RemoveDoCarrinho         | Remover item do carrinho                                |
| UC\_Checkout                 | Preencher informações de checkout e finalizar pedido    |
| UC\_NavegarParaDetalhes      | Acessar página de detalhes de um produto                |
| UC\_FiltrarProdutos          | Filtrar produtos por categoria                          |
| UC\_AdicionarAoCarrinho      | Adicionar produtos ao carrinho a partir da tela inicial |


#### 2.2.2 Requisitos funcionais

| Identificador do requisito | Nome do requisito                                                        | Casos de uso relacionados |
| -------------------------- | ------------------------------------------------------------------------ | ------------------------- |
| RF001                      | Remover item do carrinho                                                 | UC\_RemoveDoCarrinho      |
| RF002                      | Validar formato do CEP (apenas números)                                  | UC\_Checkout              |
| RF003                      | Validar campos First Name e Last Name (entrada independente)             | UC\_Checkout              |
| RF007                      | Redirecionar corretamente à página de detalhes do produto clicado        | UC\_NavegarParaDetalhes   |
| RF008                      | Filtrar corretamente os produtos por categoria selecionada               | UC\_FiltrarProdutos       |
| RF009                      | Adicionar itens ao carrinho pela tela de listagem e atualizar o contador | UC\_AdicionarAoCarrinho   |



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

### CT004 – Clicar em um produto para verificar a sua descrição

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF004                                                            |
| **Cenário de Teste**      | Verificar se a descrição do produto se encontra disponível na página do produto. |
| **ID do Caso**            | CT004                                                            |
| **Objetivo**              | Garantir que a descrição do produto esteja válida após entrar na página do produto. |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **errro_user** / **secret_sauce**).  <br>2. clicar em um produto na página inicial.  <br>3. Verificar se possui a mesma ou alguma descrição sobre o produto.   |
| **Resultado Esperado**    | - A descrição do produto esteja disponível após clicar na página. |
| **Status**                | Falhou                                                           |
| **Evidências/Observações**| A descrição é contrária ao do produto em questão. |

---

### CT005 – disponibilizar check-out sem a inclusão de produtos no carrinho

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF005                                                            |
| **Cenário de Teste**      | Verificar se é possível realizar o check-out não contendo produtos no carrinho. |
| **ID do Caso**            | CT005                                                            |
| **Objetivo**              | Garantir que a compra não seja realizada sem a inclusão de produtos no carinho. |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **performance_glitch_user** / **secret_sauce**).  <br>2. Não adicionar itens ao carrinho   <br>3. Ir para o carrinho e clicar em **checkout** <br>4. Adicionar seu **First Name**, **Last Name** e **Zip Code**. <br5> Clicar em **continuar** e logo depois em **Finish**.  |
| **Resultado Esperado**    | - A compra não poderá ser realizada pelo site quando não possuir itens no carrinho. |
| **Status**                | Falhou                                                           |
| **Evidências/Observações**| Com o carrinho vazio é possível seguir para o checktout e realizar uma compra. |

---

### CT006 – Inserir o campo **Last Name** no checkout

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF006                                                            |
| **Cenário de Teste**      | Verificar se é digitar o campo **Last Name** no checkout. |
| **ID do Caso**            | CT006                                                            |
| **Objetivo**              | Garantir que o campo de sobrenome esteja disponível para edição. |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **error_user** / **secret_sauce**).  <br>2. Adicionar ao menos um item ao carrinho e avançar até a página **“Checkout: Your Information”**.  <br>3. No campo **“First Name”**, digitar **“Laila”**.  <br>4. No campo **“Last Name”**, digitar **“Covre”**. |
| **Resultado Esperado**    | - O campo **“First Name”** mantém o valor **“Laila”**.  <br>- O campo **“Last Name”** não armazena e não possibilita a edição do nome. |
| **Status**                | Falhou                                                           |
| **Evidências/Observações**| Ao digitar em **“Last Name”**, a caixa de texto não tem possibilidade de escrita ou armazenamento.|

---

### CT007 – Redirecionamento ao clicar em item da listagem de produtos

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF007                                                            |
| **Cenário de Teste**      | Verificar se ao clicar em um item na listagem de produtos, o sistema redireciona corretamente para a página do item selecionado.|
| **ID do Caso**            | CT007                                                            |
| **Objetivo**              | Garantir que o produto clicado na listagem leve à sua própria página de detalhes, exibindo nome, descrição e preço corretos.|
| **Passos**                |	1. Acessar https://www.saucedemo.com e fazer login com **"problem_user"**. 2. Na página de produtos, clicar no item “Sauce Labs Backpack”. |
| **Resultado Esperado**    | - A página de detalhes exibida deve conter as informações corretas do produto “Sauce Labs Backpack”.
| **Status**                | Falhou                                                           |
| **Evidências/Observações**| Produto incorreto é exibido (por exemplo, “Sauce Labs Fleece Jacket” aparece ao clicar em “Sauce Labs Backpack”).

---

### CT008 – Funcionamento do filtro de categoria na página de produtos

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF008                                                            |
| **Cenário de Teste**      | Testar se o filtro por categoria exibe corretamente os produtos relacionados.|
| **ID do Caso**            | CT008                                                           |
| **Objetivo**              |Garantir que a filtragem por categoria funciona corretamente.|
| **Passos**                |	1. Acessar https://www.saucedemo.com e fazer login com **"problem_user"**. 2. Na página de produtos, selecionar uma categoria no filtro 3. Verificar que somente os produtos daquela categoria são exibidos |
| **Resultado Esperado**    | - A página deve exibir apenas produtos da categoria selecionada.
| **Status**                | Falhou                                                           |
| **Evidências/Observações**| Produto incorreto é exibido (por exemplo,selecionei o filtro por preço, porém permaneceu filtrado por ordem alfabetica).

### CT009 – Adicionar múltiplos produtos ao carrinho a partir da tela principal

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF009                                                            |
| **Cenário de Teste**      |Verificar se o botão "Add to cart" está funcionando corretamente para todos os produtos na tela inicial.|
| **ID do Caso**            | CT009                                                          |
| **Objetivo**              |	Garantir que os produtos podem ser adicionados ao carrinho a partir da tela principal.|
| **Passos**                |	1. Acessar https://www.saucedemo.com e fazer login com **"problem_user"**. 2. Na página de produtos, selecionar uma categoria no filtro 3. Localizar os seguintes itens: **"Test.allTheThings() T-Shirt (Red)"** **"Sauce Labs Fleece Jacket"** **"Sauce Labs Bolt T-Shirt"** 4. Clicar em "Add to cart" para cada um deles 5. Observar se o botão muda para **"Remove"** e o contador do carrinho é incrementado |
| **Resultado Esperado**    | -  O botão muda para “Remove” após o clique - O contador do carrinho é incrementado corretamente - Os produtos são adicionados ao carrinho com sucesso |
| **Status**                | Falhou                                                           |
| **Evidências/Observações**| O clique em "Add to cart" não produz efeito: o botão não muda, o item não é adicionado ao carrinho e nenhuma ação visível ocorre. |



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

**Título do Bug**: Campo “Last Name” sobrescreve conteúdo de “First Name” ao digitar.  
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


### Defeito 004 

**Título do Bug**: Ao clicar em um produto, a descrição do mesmo está incorreta
**ID**: DFT-004
**Reportado por**: Laila Covre
**Data do Relato**: 06/06/2025
**Versão do Sistema**: 1.0
**Prioridade**: Alta
**Severidade**: Crítica

**Descrição**
A descrição do produto fica indisponível assim que o usuário clica no produto e entra na sua página.

**Para Reproduzir**

Acessar https://www.saucedemo.com e fazer login com usuário **error_user** / **secret_sauce**

Clicar em um produto na página inicial

**Resultado Esperado**

A descrição correta do produto está disponível

**Resultado Atual**

O produto está sem descrição

**Anexos**
[Na pasta deste repositório, nomeado com o ID do defeito]

**Ambiente de Teste**

Desktop: Windows 10, Google Chrome

**Histórico de Status**

- [x] Novo

- [ ] Em Análise

- [ ] Em Progresso

- [ ] Resolvido

- [ ] Não Reproduzível

- [ ] Rejeitado

### Defeito 005 

**Título do Bug**: Check out disponível sem itens no carrinho
**ID**: DFT-005
**Reportado por**: Laila Covre
**Data do Relato**: 06/06/2025
**Versão do Sistema**: 1.0
**Prioridade**: Média
**Severidade**: Média

**Descrição**

O sistema possibilita a realização do checkout sem a inclusão de itens no carrinho

**Para Reproduzir**

Acessar https://www.saucedemo.com e fazer login com usuário **performance_glitch_user** / **secret_sauce**

clicar no carrinho vazio e avaçar para o check out

inserir os dados e finalizar


**Resultado Esperado**

O sistemas deve impedir a realização do checkout

**Resultado Atual**

O sistema finaliza a compra

**Anexos**
[Na pasta deste repositório, nomeado com o ID do defeito]

Ambiente de Teste

Desktop: Windows 10, Google Chrome

**Histórico de Status**

- [x] Novo

- [ ] Em Análise

- [ ] Em Progresso

- [ ] Resolvido

- [ ] Não Reproduzível

- [ ] Rejeitado


### Defeito 006

**Título do Bug**: O campo **Last Name** é impossibilitado de edições na aba checkout
**ID**: DFT-006
**Reportado por**: Laila Covre
**Data do Relato**: 06/06/2025
**Versão do Sistema**: 1.0
**Prioridade**: Baixa
**Severidade**: Baixa

**Descrição**
Ao realizar o checkout o campo **Last Name** impossibilita o usuário de digitar seu sobrenome.

**Para Reproduzir**

Acessar https://www.saucedemo.com e fazer login com usuário **error_user** / **secret_sauce**

Adicionar um item ao carrinho e realizar o check out

Adicionar os dados de nome e sobrenome e zip code.

**Resultado Esperado**

O sistema deve armazenar o sobrenome inserido.

**Resultado Atual**

O sistema não armazena ou possibilita a edição do sobrenome.

**Anexos**
[Na pasta deste repositório, nomeado com o ID do defeito]

Ambiente de Teste

Desktop: Windows 10, Google Chrome

**Histórico de Status**

- [x] Novo

- [ ] Em Análise

- [ ] Em Progresso

- [ ] Resolvido

- [ ] Não Reproduzível

- [ ] Rejeitado

### Defeito 007

**Título do Bug**: Produto incorreto é exibido ao clicar em item na página de produtos  
**ID**: DFT-007   
**Reportado por**: Caio Teixeira  
**Data do Relato**:09/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Alta   
**Severidade**: Alta  

**Descrição**  
Clicando em qualquer produto na página principal redireciona o usuário para uma página de produto diferente, causando confusão e dificultando a navegação correta entre os itens.

**Para Reproduzir**  
1. Acessar https://www.saucedemo.com e fazer login com usuário **problem_user** / **secret_sauce”.  
2. Na página de produtos, clicar em qualquer item, por exemplo: “Sauce Labs Backpack”
3. Observar o produto exibido na nova página

**Resultado Esperado**  
Ao clicar em um produto, a página correspondente ao produto clicado deve ser aberta, mostrando nome, descrição e valor corretos.

**Resultado Atual**  
O sistema redireciona para outro produto aleatório, diferente do que foi clicado.

**Anexos**  
[Na pasta deste repositorio, nomeado com o ID do defeito DFT-004]

**Ambiente de Teste**  
- **Desktop**: Windows 11, Google Chrome.

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

### Defeito 008 

**Título do Bug**: Filtros da lista não aplicam alterações  
**ID**: DFT-008  
**Reportado por**: Caio Teixeira  
**Data do Relato**:05/06/2025   
**Versão do Sistema**: 1.0  
**Prioridade**: Alta  
**Severidade**: Média  

**Descrição**  
Na tela onde há filtros para visualização de registros, ao alterar qualquer filtro, a lista não é atualizada. O sistema ignora a ação do usuário, permanecendo com o conteúdo anterior.

**Para Reproduzir**  
1. Acessar https://www.saucedemo.com e fazer login com usuário **problem_user** / **secret_sauce”.  
2. Alterar o valor de qualquer filtro (ex: nome, preço).
3. Observar que a lista exibida não sofre alterações. 

**Resultado Esperado**  
- A lista deve ser atualizada automaticamente com base nos filtros selecionados.  

**Resultado Atual**  
- A lista permanece inalterada mesmo após modificar os filtros. Nenhuma atualização ocorre.

**Anexos**  
[Na pasta deste repositorio, nomeado com o ID do defeito]


**Ambiente de Teste**  
- **Desktop**: Windows 11, Google Chrome.  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

### Defeito 009 

**Título do Bug**: Itens não são adicionados ao carrinho na tela inicial.
**ID**: DFT-009  
**Reportado por**: Caio Teixeira  
**Data do Relato**:05/06/2025   
**Versão do Sistema**: 1.0  
**Prioridade**: Alta  
**Severidade**: Alta  

**Descrição**  
Na página inicial onde são exibidos todos os produtos, ao clicar em "Add to cart" para determinados itens, nada acontece. A ação é ignorada e os produtos não são adicionados ao carrinho.

**Itens afetados**  
-Test.allTheThings() T-Shirt (Red)
-Sauce Labs Fleece Jacket
-Sauce Labs Bolt T-Shirt

**Para Reproduzir**  
1. Acessar https://www.saucedemo.com e fazer login com usuário **problem_user** / **secret_sauce”.  
2. Na página inicial com os produtos, localizar um dos itens afetados.
3. Clicar em "Add to cart".
4. Verificar se o contador do carrinho é incrementado ou se o botão muda para "Remove".

**Resultado Esperado**  
- O botão deve mudar para “Remove”.
- O contador do carrinho deve ser atualizado corretamente.
- O item deve ser adicionado ao carrinho.

**Resultado Atual**  
- A ação é ignorada. O item não é adicionado ao carrinho, e o botão permanece inalterado.

**Anexos**  
[Na pasta deste repositorio, nomeado com o ID do defeito]


**Ambiente de Teste**  
- **Desktop**: Windows 11, Google Chrome.  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

### Defeito 010
Título do Bug: Mensagem de erro inválida no checkout v1
ID:DFT-010
Reportado por: celso eloy
Data do Relato: 6/6/25
Versão do Sistema: 1.0
Prioridade: baixa
Severidade: média

**Descrição:**
Mensagem de erro inválida é exibida quando o usuário quer fazer checkout apenas com o Last Name preenchido

**Para Reproduzir:**
-	Usuario logou como standard_user
-	Usuario vai para a pagina do carrinho
-	Usuario tenha selecionado o(s) produto(s)

1.	Usuario clica no botão de Checkout
2.	Usuario preenche o apenas o campo Last Name
3.	Usuario clica no botão de continuar
**Resultado Esperado:**
O sistema deveria retornar a seguinte mensagem de erro “Error: First Name and Postal Code are required”
**Resultado Atual:** Sistema retorna a seguinte mensagem de erro: “Error: First Name is required”
Anexos: se encontra com o ID do erro
Ambiente de Teste
Desktop: Windows 10, Opera, 119.0.5497.56


### Defeito 011
Título do Bug: Mensagem de erro invalida no checkout v2
ID:DFT-011
Reportado por: celso eloy
Data do Relato: 6/6/25
Versão do Sistema: 1.0
Prioridade: baixa
Severidade: media
Descrição:
Mensagem de erro inválida é exibida quando o usuário quer fazer checkout apenas com o First Name preenchido

Para Reproduzir:
-	Usuario logou como standard_user
-	Usuario vai para a pagina do carrinho
-	Usuario tenha selecionado o(s) produto(s)

4.	Usuario clica no botão de Checkout
5.	Usuario preenche o apenas o campo First Name
6.	Usuario clica no botão de continuar
Resultado Esperado
O sistema deveria retornar a seguinte mensagem de erro “Error: Last Name and Postal Code are required”
Resultado Atual: Sistema retorna a seguinte mensagem de erro: “Error: Last Name is required”
Anexos: se encontra com o ID do erro
Ambiente de Teste
Desktop: Windows 10, Opera, 119.0.5497.56

### Defeito 012
Título do Bug: Mensagem de erro invalida no checkout v3
ID:DFT-012
Reportado por: celso eloy
Data do Relato: 6/6/25
Versão do Sistema: 1.0
Prioridade: baixa
Severidade: media
**Descrição:**
Mensagem de erro inválida é exibida quando o usuário quer fazer checkout apenas com o First Name preenchido

**Para Reproduzir:**
-	Usuario logou como standard_user
-	Usuario vai para a pagina do carrinho
-	Usuario tenha selecionado o(s) produto(s)

7.	Usuario clica no botão de Checkout
8.	Usuario preenche o apenas o campo Postal Code
9.	Usuario clica no botão de continuar
**Resultado Esperado:**
O sistema deveria retornar a seguinte mensagem de erro “Error: First Name and Last Name are required”
**Resultado Atual:** Sistema retorna a seguinte mensagem de erro: “Error: First Name is required”

Anexos: se encontra com o ID do erro


Ambiente de Teste
Desktop: Windows 10, Opera, 119.0.5497.56
