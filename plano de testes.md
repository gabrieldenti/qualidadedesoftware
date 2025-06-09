# Plano de Teste

**Nome do Sistema**: Swag Labs  
**Link do site**: https://www.saucedemo.com  
**Data**: 01/06/2025  
*versão 1.0*  
*Autores: Gabriel Denti, Caio Teixeira, Laila Covre, Celso Eloy*  

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
|------------------------------|---------------------------------------------------------|
| UC_RemoveDoCarrinho          | Remover item do carrinho                                |
| UC_Checkout                  | Preencher informações de checkout e finalizar pedido    |
| UC_NavegarParaDetalhes       | Acessar página de detalhes de um produto                |
| UC_FiltrarProdutos           | Filtrar produtos por categoria                          |
| UC_AdicionarAoCarrinho       | Adicionar produtos ao carrinho a partir da tela inicial |

#### 2.2.2 Requisitos funcionais

| Identificador do requisito | Nome do requisito                                                        | Casos de uso relacionados |
|----------------------------|---------------------------------------------------------------------------|---------------------------|
| RF001                      | Remover item do carrinho                                                  | UC_RemoveDoCarrinho      |
| RF002                      | Validar formato do CEP (apenas números)                                   | UC_Checkout              |
| RF003                      | Validar campos First Name e Last Name                                     | UC_Checkout              |
| RF005                      | Impedir checkout sem itens no carrinho                                    | UC_Checkout              |
| RF006                      | Permitir edição independente do campo Last Name no checkout               | UC_Checkout              |
| RF007                      | Redirecionar corretamente à página de detalhes do produto clicado         | UC_NavegarParaDetalhes   |
| RF008                      | Filtrar corretamente os produtos por categoria selecionada                | UC_FiltrarProdutos       |
| RF009                      | Adicionar itens ao carrinho pela tela de listagem e atualizar o contador  | UC_AdicionarAoCarrinho   |

---

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

---

#### CT001 – Remover item adicionado ao carrinho na página de produtos

| Campo                     | Descrição                                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------------------------|
| **Requisito**             | RF001                                                                                                      |
| **Cenário de Teste**      | Verificar que, após adicionar um item, é possível removê-lo clicando em “Remove” na página de produtos.    |
| **ID do Caso**            | CT001                                                                                                      |
| **Objetivo**              | Garantir que a remoção de um produto reflita corretamente no botão (“Remove” → “Add to cart”), no contador do carrinho e na lista de itens. |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **problem_user** / **secret_sauce**).<br>2. Na lista de produtos, clicar em **“Add to cart”** do produto **“Sauce Labs Bike Light”**.<br>3. Clicar em **“Remove”** para o mesmo produto. |
| **Resultado Esperado**    | - O botão volta a exibir **“Add to cart”**.<br>- O contador do carrinho diminui de **1** para **0**.<br>- O produto **“Sauce Labs Bike Light”** não aparece mais na lista de itens do carrinho. |
| **Status**                | Falhou                                                                                                     |
| **Evidências/Observações**| Ao clicar em **“Remove”**, o botão não muda, o contador não decrementa e o produto permanece no carrinho. |

---

#### CT002 – Inserir letras e caracteres especiais no campo Postal Code durante checkout

| Campo                     | Descrição                                                                                                   |
|---------------------------|-------------------------------------------------------------------------------------------------------------|
| **Requisito**             | RF002                                                                                                       |
| **Cenário de Teste**      | Garantir que o campo **“Postal Code”** aceite somente números.                                               |
| **ID do Caso**            | CT002                                                                                                       |
| **Objetivo**              | Validar que o sistema bloqueie ou rejeite entradas que contenham letras e caracteres especiais no campo CEP. |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **standard_user** / **secret_sauce**).<br>2. Adicionar ao menos um item ao carrinho.<br>3. Clicar no ícone do carrinho e depois em **“Checkout”**.<br>4. Preencher **“First Name”** com **“Gabriel”** e **“Last Name”** com **“Denti”**.<br>5. No campo **“Postal Code”**, digitar **“ABC123!@#”**.<br>6. Clicar em **“Continue”**. |
| **Resultado Esperado**    | - O campo **“Postal Code”** aceita apenas dígitos (bloquear letras e símbolos).<br>- Se o formato estiver incorreto, exibir **“Error: Postal Code is required”** e impedir a continuação. |
| **Status**                | Falhou                                                                                                      |
| **Evidências/Observações**| O campo aceita letras e caracteres especiais sem validação, permitindo **“ABC123!@#”** e não apresenta mensagem de erro adequada. |

---

#### CT003 – Inserir texto nos campos First Name e Last Name para verificar independência

| Campo                     | Descrição                                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------------------------|
| **Requisito**             | RF003                                                                                                     |
| **Cenário de Teste**      | Verificar se é possível digitar **“First Name”** e **“Last Name”** sem que um sobrescreva o outro.         |
| **ID do Caso**            | CT003                                                                                                     |
| **Objetivo**              | Garantir que os campos de nome e sobrenome funcionem de forma independente, sem troca ou exclusão de conteúdo. |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **problem_user** / **secret_sauce**).<br>2. Adicionar ao menos um item ao carrinho e avançar até a página **“Checkout: Your Information”**.<br>3. No campo **“First Name”**, digitar **“Gabriel”**.<br>4. No campo **“Last Name”**, digitar **“Denti”**. |
| **Resultado Esperado**    | - O campo **“First Name”** mantém o valor **“Gabriel”**.<br>- O campo **“Last Name”** armazena **“Denti”** sem interferir no campo de nome. |
| **Status**                | Falhou                                                                                                     |
| **Evidências/Observações**| Ao digitar em **“Last Name”**, o texto sobrescreve o que foi digitado em **“First Name”**; o campo **“Last Name”** permanece vazio. |

---

#### CT004 – Clicar em um produto para verificar a sua descrição

| Campo                     | Descrição                                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------------------------|
| **Requisito**             | RF007                                                                                                     |
| **Cenário de Teste**      | Verificar se a descrição do produto se encontra disponível na página do produto.                           |
| **ID do Caso**            | CT004                                                                                                     |
| **Objetivo**              | Garantir que a descrição do produto esteja válida após entrar na página do produto.                       |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **error_user** / **secret_sauce**).<br>2. Clicar em um produto na página inicial.<br>3. Verificar se a descrição correspondente está presente. |
| **Resultado Esperado**    | - A descrição do produto esteja disponível e correta.                                                      |
| **Status**                | Falhou                                                                                                     |
| **Evidências/Observações**| A descrição exibida é incorreta ou ausente.                                                                |

---

#### CT005 – Disponibilizar check-out sem a inclusão de produtos no carrinho

| Campo                     | Descrição                                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------------------------|
| **Requisito**             | RF005                                                                                                     |
| **Cenário de Teste**      | Verificar se é possível realizar o check-out não contendo produtos no carrinho.                            |
| **ID do Caso**            | CT005                                                                                                     |
| **Objetivo**              | Garantir que a compra não seja realizada sem a inclusão de produtos no carrinho.                           |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **performance_glitch_user** / **secret_sauce**).<br>2. Não adicionar itens ao carrinho.<br>3. Ir para o carrinho e clicar em **Checkout**.<br>4. Preencher **First Name**, **Last Name** e **Postal Code**; clicar em **Continue** e depois em **Finish**. |
| **Resultado Esperado**    | - A compra não pode ser realizada quando não houver itens no carrinho.                                      |
| **Status**                | Falhou                                                                                                     |
| **Evidências/Observações**| Mesmo com o carrinho vazio, o fluxo permite finalizar a compra.                                            |

---

#### CT006 – Inserir o campo Last Name no checkout

| Campo                     | Descrição                                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------------------------|
| **Requisito**             | RF006                                                                                                     |
| **Cenário de Teste**      | Verificar se o campo **Last Name** está disponível para edição no checkout.                                |
| **ID do Caso**            | CT006                                                                                                     |
| **Objetivo**              | Garantir que o campo de sobrenome possa ser preenchido corretamente.                                       |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **error_user** / **secret_sauce**).<br>2. Adicionar ao menos um item ao carrinho e avançar até **Checkout: Your Information**.<br>3. Digitar **“Laila”** em **First Name** e **“Covre”** em **Last Name**. |
| **Resultado Esperado**    | - **First Name** mantém o valor **“Laila”**.<br>- **Last Name** aceita e armazena **“Covre”**.             |
| **Status**                | Falhou                                                                                                     |
| **Evidências/Observações**| Campo **Last Name** não permite edição ou armazenamento.                                                   |

---

#### CT007 – Redirecionamento ao clicar em item da listagem de produtos

| Campo                     | Descrição                                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------------------------|
| **Requisito**             | RF007                                                                                                     |
| **Cenário de Teste**      | Verificar se ao clicar em um item na listagem de produtos, o sistema redireciona corretamente para a página do produto selecionado. |
| **ID do Caso**            | CT007                                                                                                     |
| **Objetivo**              | Garantir que o clique em um produto leve à sua página de detalhes com nome, descrição e preço corretos.   |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **problem_user** / **secret_sauce**).<br>2. Clicar no produto **“Sauce Labs Backpack”**. |
| **Resultado Esperado**    | - A página de detalhes exibida contém as informações corretas de **“Sauce Labs Backpack”**.                 |
| **Status**                | Falhou                                                                                                     |
| **Evidências/Observações**| Exibe detalhe de produto diferente (por exemplo **“Sauce Labs Fleece Jacket”**).                           |

---

#### CT008 – Funcionamento do filtro de categoria na página de produtos

| Campo                     | Descrição                                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------------------------|
| **Requisito**             | RF008                                                                                                     |
| **Cenário de Teste**      | Testar se o filtro por categoria exibe corretamente os produtos relacionados.                              |
| **ID do Caso**            | CT008                                                                                                     |
| **Objetivo**              | Garantir que a filtragem por categoria funcione corretamente.                                              |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **problem_user** / **secret_sauce**).<br>2. Selecionar uma categoria no filtro.<br>3. Verificar que somente produtos dessa categoria são exibidos. |
| **Resultado Esperado**    | - A lista exibe apenas produtos da categoria selecionada.                                                  |
| **Status**                | Falhou                                                                                                     |
| **Evidências/Observações**| Produtos de outras categorias continuam visíveis.                                                         |

---

#### CT009 – Adicionar múltiplos produtos ao carrinho a partir da tela principal

| Campo                     | Descrição                                                                                                  |
|---------------------------|------------------------------------------------------------------------------------------------------------|
| **Requisito**             | RF009                                                                                                     |
| **Cenário de Teste**      | Verificar se o botão **“Add to cart”** funciona para todos os produtos na tela inicial.                   |
| **ID do Caso**            | CT009                                                                                                     |
| **Objetivo**              | Garantir que vários produtos possam ser adicionados ao carrinho com atualização correta do contador.      |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **problem_user** / **secret_sauce**).<br>2. Clicar em **“Add to cart”** para **“Test.allTheThings() T-Shirt (Red)”**, **“Sauce Labs Fleece Jacket”** e **“Sauce Labs Bolt T-Shirt”**.<br>3. Observar se o botão muda para **“Remove”** e o contador incrementa. |
| **Resultado Esperado**    | - Botão muda para **“Remove”** após cada clique.<br>- Contador do carrinho incrementa corretamente.<br>- Todos os produtos são adicionados. |
| **Status**                | Falhou                                                                                                     |
| **Evidências/Observações**| Clique não produz efeito: botões não mudam e contador não incrementa.                                     |

---

### CT010 - Inserir apenas o campo Last Name no checkout

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF003                              |
| **Cenário de Teste**      | Verificar se o sistema indica quais informações falta ao inserir apenas Last Name                         |
| **ID do Caso**            | CT010                            |
| **Objetivo**              | Garantir que o usuário seja informado que faltam First Name e Postal Code para concluir o checkout                            |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **standard_user** / **secret_sauce**).<br>2. Selecione o(s) produto(s) e vá para o carrinho.<br>3. Clique no botão de Checkout.<br>4. Preencha o apenas o campo Last Name e clique em Continue.                                   |
| **Resultado Esperado**    | O sistema deveria retornar a seguinte mensagem de erro “Error: First Name and Postal Code are required”      |
| **Status**                | Falhou                                                  |
| **Evidências/Observações**| Video em anexo                   |

---

### CT011 - Inserir apenas o campo First Name no checkout

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF003                             |
| **Cenário de Teste**      | Verificar se o sistema indica quais informações falta ao inserir apenas First Name                         |
| **ID do Caso**            | CT011                            |
| **Objetivo**              | Garantir que o usuário seja informado que faltam Last Name e Postal Code para concluir o checkout                            |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **standard_user** / **secret_sauce**).<br>2. Selecione o(s) produto(s) e vá para o carrinho.<br>3. Clique no botão de Checkout.<br>4. Preencha o apenas o campo First Name e clique em Continue.                                   |
| **Resultado Esperado**    | O sistema deveria retornar a seguinte mensagem de erro “Error: Last Name and Postal Code are required”      |
| **Status**                | Falhou                                                  |
| **Evidências/Observações**| Video em anexo                    |

---

### CT012 - Inserir apenas o campo Postal Code no checkout

| Campo                     | Descrição                                                        |
|---------------------------|------------------------------------------------------------------|
| **Requisito**             | RF003                              |
| **Cenário de Teste**      | Verificar se o sistema indica quais informações falta ao inserir apenas Postal Code                         |
| **ID do Caso**            | CT012                            |
| **Objetivo**              | Garantir que o usuário seja informado que faltam First Name e Postal Codee  para concluir o checkout                            |
| **Passos**                | 1. Acessar https://www.saucedemo.com e fazer login (usuário **standard_user** / **secret_sauce**).<br>2. Selecione o(s) produto(s) e vá para o carrinho.<br>3. Clique no botão de Checkout.<br>4. Preencha o apenas o campo Postal Code e clique em Continue.                                   |
| **Resultado Esperado**    | O sistema deveria retornar a seguinte mensagem de erro “Error: First Name and Last Name are required”      |
| **Status**                | Falhou                                                  |
| **Evidências/Observações**| Video em anexo                    |

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

## 4 – REPORT DE DEFEITO (Espaço para preenchimento)


---

### Defeito 001

**Título do Bug**: Produto não é removido do carrinho ao clicar em “Remove” na página de produtos  
**ID**: DFT-001  
**Reportado por**: Gabriel Denti  
**Data do Relato**: 05/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Alta  
**Severidade**: Alta  

**Descrição**  
Ao clicar em “Remove” na página de produtos para um item previamente adicionado, o botão não retorna para “Add to cart”, o contador de itens não decrementa e o produto permanece listado no carrinho.

**Para Reproduzir**  
1. Acessar https://www.saucedemo.com e fazer login com usuário **problem_user** / **secret_sauce**.  
2. Na página de produtos, clicar em **“Add to cart”** do produto **“Sauce Labs Bike Light”**.  
3. Retornar à página de produtos e clicar em **“Remove”** no mesmo produto.  

**Resultado Esperado**  
- Botão volta a exibir **“Add to cart”**.  
- Contador do carrinho diminui de **1** para **0**.  
- Produto não aparece mais no carrinho.  

**Resultado Atual**  
- Botão permanece em **“Remove”**.  
- Contador continua em **1**.  
- Produto ainda aparece no carrinho.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-001]

**Ambiente de Teste**  
- **Desktop**: Windows 11, Mozilla Firefox

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
**Data do Relato**: 05/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Média  
**Severidade**: Média  

**Descrição**  
O campo “Postal Code” na página de checkout não valida o formato e aceita entradas como “ABC123!@#”, sem exibir mensagem de erro.

**Para Reproduzir**  
1. Login como **standard_user** / **secret_sauce**.  
2. Adicionar item ao carrinho e avançar para “Checkout: Your Information”.  
3. Preencher **First Name** com “Gabriel” e **Last Name** com “Denti”.  
4. Digitar **“ABC123!@#”** em **Postal Code**.  
5. Clicar em **Continue**.  

**Resultado Esperado**  
- Campo aceita apenas dígitos ou exibe **“Error: Postal Code is required”**.  
- Não permite avançar sem CEP válido.

**Resultado Atual**  
- Campo aceita **“ABC123!@#”** sem erro e permite prosseguir.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-002]

**Ambiente de Teste**  
- **Desktop**: Windows 11, Mozilla Firefox   

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
**Data do Relato**: 05/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Alta  
**Severidade**: Alta  

**Descrição**  
Ao digitar no campo “Last Name”, o conteúdo previamente inserido em “First Name” é apagado e os caracteres aparecem em “First Name”, deixando “Last Name” vazio.

**Para Reproduzir**  
1. Login como **problem_user** / **secret_sauce**.  
2. Adicionar item ao carrinho e avançar para “Checkout: Your Information”.  
3. Digitar “Gabriel” em **First Name**.  
4. Digitar “Denti” em **Last Name**.  

**Resultado Esperado**  
- **First Name** mantém “Gabriel”.  
- **Last Name** armazena “Denti” independentemente.

**Resultado Atual**  
- **First Name** passa a exibir “Denti” (ou apenas a última letra).  
- **Last Name** permanece vazio.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-003]

**Ambiente de Teste**  
- **Desktop**: Windows 11, Mozilla Firefox  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 004

**Título do Bug**: Descrição do produto ausente ou incorreta na página de detalhes  
**ID**: DFT-004  
**Reportado por**: Laila Covre  
**Data do Relato**: 06/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Alta  
**Severidade**: Crítica  

**Descrição**  
Ao clicar em um produto, a descrição não é exibida ou está incorreta na página de detalhes.

**Para Reproduzir**  
1. Login como **error_user** / **secret_sauce**.  
2. Clicar em qualquer produto na página inicial.

**Resultado Esperado**  
- Exibir descrição correta do produto.

**Resultado Atual**  
- Descrição ausente ou errada.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-004]

**Ambiente de Teste**  
- **Desktop**: Windows 10, Google Chrome  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 005

**Título do Bug**: Checkout disponível sem itens no carrinho  
**ID**: DFT-005  
**Reportado por**: Laila Covre  
**Data do Relato**: 06/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Média  
**Severidade**: Média  

**Descrição**  
O sistema possibilita a realização do checkout sem a inclusão de itens no carrinho.

**Para Reproduzir**  
1. Login como **performance_glitch_user** / **secret_sauce**.  
2. Acessar carrinho vazio.  
3. Clicar em **Checkout**, preencher dados e finalizar.

**Resultado Esperado**  
- Impedir finalização sem produtos.

**Resultado Atual**  
- Checkout concluído mesmo sem itens.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-005]

**Ambiente de Teste**  
- **Desktop**: Windows 10, Google Chrome  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 006

**Título do Bug**: Campo “Last Name” não editável no checkout  
**ID**: DFT-006  
**Reportado por**: Laila Covre  
**Data do Relato**: 06/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Baixa  
**Severidade**: Baixa  

**Descrição**  
O campo “Last Name” não permite inserção ou armazenamento do sobrenome durante o checkout.

**Para Reproduzir**  
1. Login como **error_user** / **secret_sauce**.  
2. Adicionar item ao carrinho e ir para checkout.  
3. Digitar “Laila” em **First Name** e “Covre” em **Last Name**.

**Resultado Esperado**  
- **Last Name** aceita e armazena “Covre”.

**Resultado Atual**  
- Campo permanece inativo, sem edição.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-006]

**Ambiente de Teste**  
- **Desktop**: Windows 10, Google Chrome  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 007

**Título do Bug**: Produto incorreto exibido ao clicar em item na página de produtos  
**ID**: DFT-007  
**Reportado por**: Caio Teixeira  
**Data do Relato**: 09/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Alta  
**Severidade**: Alta  

**Descrição**  
Clicando em qualquer produto na página principal, o usuário é redirecionado para um produto diferente, causando confusão.

**Para Reproduzir**  
1. Login como **problem_user** / **secret_sauce**.  
2. Clicar em **“Sauce Labs Backpack”**.  
3. Observar o detalhe exibido.

**Resultado Esperado**  
- Página de detalhe de **“Sauce Labs Backpack”**.

**Resultado Atual**  
- Exibe outro produto (ex.: **“Sauce Labs Fleece Jacket”**).

**Anexos**  
- [Na pasta do repositório, nomeado DFT-007]

**Ambiente de Teste**  
- **Desktop**: Windows 11, Google Chrome  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 008

**Título do Bug**: Filtros de produto não aplicam alterações  
**ID**: DFT-008  
**Reportado por**: Caio Teixeira  
**Data do Relato**: 05/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Alta  
**Severidade**: Média  

**Descrição**  
Ao alterar filtros (nome/preço), a lista de produtos não é atualizada.

**Para Reproduzir**  
1. Login como **problem_user** / **secret_sauce**.  
2. Aplicar qualquer filtro.  

**Resultado Esperado**  
- Lista atualiza conforme filtro.

**Resultado Atual**  
- Lista permanece inalterada.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-008]

**Ambiente de Teste**  
- **Desktop**: Windows 11, Google Chrome  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 009

**Título do Bug**: Itens não são adicionados ao carrinho na tela inicial  
**ID**: DFT-009  
**Reportado por**: Caio Teixeira  
**Data do Relato**: 05/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Alta  
**Severidade**: Alta  

**Descrição**  
Alguns produtos (Test.allTheThings() T-Shirt, Fleece Jacket, Bolt T-Shirt) não respondem ao “Add to cart”.

**Para Reproduzir**  
1. Login como **problem_user** / **secret_sauce**.  
2. Clicar em “Add to cart” nos itens afetados.

**Resultado Esperado**  
- Botão muda para “Remove” e contador incrementa.

**Resultado Atual**  
- Nenhuma ação; botão e contador inalterados.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-009]

**Ambiente de Teste**  
- **Desktop**: Windows 11, Google Chrome  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 010

**Título do Bug**: Mensagem de erro inválida no checkout v1  
**ID**: DFT-010  
**Reportado por**: Celso Eloy  
**Data do Relato**: 06/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Baixa  
**Severidade**: Média  

**Descrição**  
Se apenas **Last Name** for preenchido, a mensagem deveria exigir **First Name** e **Postal Code**, mas exibe apenas **“Error: First Name is required”**.

**Para Reproduzir**  
1. Login como **standard_user**.  
2. Ir ao carrinho com itens.  
3. Clicar em **Checkout**, preencher só **Last Name**, clicar em **Continue**.

**Resultado Esperado**  
- **“Error: First Name and Postal Code are required”**.

**Resultado Atual**  
- Exibe **“Error: First Name is required”**.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-010]

**Ambiente de Teste**  
- **Desktop**: Windows 10, Opera 119.0.5497.56  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 011

**Título do Bug**: Mensagem de erro inválida no checkout v2  
**ID**: DFT-011  
**Reportado por**: Celso Eloy  
**Data do Relato**: 06/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Baixa  
**Severidade**: Média  

**Descrição**  
Se apenas **First Name** for preenchido, a mensagem deveria exigir **Last Name** e **Postal Code**, mas exibe apenas **“Error: Last Name is required”**.

**Para Reproduzir**  
1. Login como **standard_user**.  
2. Ir ao carrinho com itens.  
3. Clicar em **Checkout**, preencher só **First Name**, clicar em **Continue**.

**Resultado Esperado**  
- **“Error: Last Name and Postal Code are required”**.

**Resultado Atual**  
- Exibe **“Error: Last Name is required”**.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-011]

**Ambiente de Teste**  
- **Desktop**: Windows 10, Opera 119.0.5497.56  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  

---

### Defeito 012

**Título do Bug**: Mensagem de erro inválida no checkout v3  
**ID**: DFT-012  
**Reportado por**: Celso Eloy  
**Data do Relato**: 06/06/2025  
**Versão do Sistema**: 1.0  
**Prioridade**: Baixa  
**Severidade**: Média  

**Descrição**  
Se apenas **Postal Code** for preenchido, a mensagem deveria exigir **First Name** e **Last Name**, mas exibe **“Error: First Name is required”**.

**Para Reproduzir**  
1. Login como **standard_user**.  
2. Ir ao carrinho com itens.  
3. Clicar em **Checkout**, preencher só **Postal Code**, clicar em **Continue**.

**Resultado Esperado**  
- **“Error: First Name and Last Name are required”**.

**Resultado Atual**  
- Exibe **“Error: First Name is required”**.

**Anexos**  
- [Na pasta do repositório, nomeado DFT-012]

**Ambiente de Teste**  
- **Desktop**: Windows 10, Opera 119.0.5497.56  

**Histórico de Status**  
- [x] Novo  
- [ ] Em Análise  
- [ ] Em Progresso  
- [ ] Resolvido  
- [ ] Não Reproduzível  
- [ ] Rejeitado  
