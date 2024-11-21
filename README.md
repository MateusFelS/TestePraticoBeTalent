# Plano de Testes - Sauce Demo

## 1. Plano de Testes

### 1.1 Objetivo
Garantir que os fluxos principais da aplicação funcionem corretamente, proporcionando uma experiência de usuário satisfatória e sem problemas funcionais.

### 1.2 Escopo
- **Funcionalidade**: Login, navegação, compra, logout.
- **UI/UX**: Identificação de elementos confusos ou inconsistentes.

### 1.3 Ambiente de Teste
- Navegador (Chrome, Brave)
- Sistema Operacional (Windows 10)

---

## 2. Casos de Teste

### 2.1 Login
| ID   | Descrição                          | Pré-condição            | Passos                                                                 | Resultado Esperado                              | Resultado Real                                   |
|------|------------------------------------|-------------------------|------------------------------------------------------------------------|------------------------------------------------|-------------------------------------------------|
| TC01 | Login com credenciais válidas      | Página de login aberta  | 1. Insira credenciais válidas. <br> 2. Clique em "Login".              | Redirecionado para a página de produtos.       | ✅ Pass                                         |
| TC02 | Login com credenciais inválidas    | Página de login aberta  | 1. Insira credenciais inválidas. <br> 2. Clique em "Login".            | Exibe mensagem de erro apropriada.            | ⚠️ Pass, mas mensagem de erro cortada.          |
| TC03 | Login com campos em branco         | Página de login aberta  | 1. Deixe campos em branco. <br> 2. Clique em "Login".                  | Exibe mensagem de erro apropriada.            | ✅ Pass                                         |
| TC04 | Tentar acessar página sem login    | Página protegida        | 1. Acesse diretamente a URL da página de produtos sem login.           | Redirecionado para a página de login.          | ✅ Pass                                         |

### 2.2 Carrinho
| ID   | Descrição                    | Pré-condição               | Passos                                               | Resultado Esperado                              | Resultado Real                                   |
|------|------------------------------|----------------------------|-----------------------------------------------------|------------------------------------------------|-------------------------------------------------|
| TC05 | Adicionar item ao carrinho   | Página de produtos aberta  | 1. Faça o Login <br>2. Clique em "Add to Cart".     | Item adicionado ao carrinho com sucesso.       | ✅ Pass                                         |
| TC06 | Remover item do carrinho     | Carrinho com itens         | 1. Faça o Login <br>2. Clique em "Add to Cart" <br>3. Clique em "Remove" no item do carrinho.| Item removido do carrinho.| ✅ Pass                   |
| TC07 | Carrinho vazio               | Carrinho vazio             | 1. Faça o Login <br>2. Clique no icone de Cart.    | Exibe mensagem "Carrinho vazio".               | ❌ Fail - Nenhuma mensagem é retornada          |
| TC08 | Soma de preços no carrinho   | Carrinho com itens         | 1. Faça o Login <br>2. Clique em "Add to Cart" <br>3. Clique no icone de Cart <br>4. Verifique a soma dos preços. | Soma dos preços exibida corretamente.          | ✅ Pass   |

### 2.3 Checkout
| ID   | Descrição                     | Pré-condição                  | Passos                                               | Resultado Esperado                              | Resultado Real                                   |
|------|-------------------------------|-------------------------------|-----------------------------------------------------|------------------------------------------------|----------------------------------------------|
| TC09 | Checkout com carrinho vazio   | Carrinho vazio                | 1. Faça o Login <br>2. Clique em "Add to Cart" <br>3. Clique no icone de Cart <br>4. Insira credenciais válidas no formulário <br>5. Clique em "Finish" | Exibe mensagem "Carrinho vazio". | ❌ Fail - Checkout permitido com carrinho vazio.|
| TC10 | Checkout com credenciais válidas | Carrinho com itens           | 1. Faça o Login <br>2. Clique em "Add to Cart" <br>3. Clique no icone de Cart <br>4. Insira credenciais válidas no formulário. <br>5. Clique em "Finish" | Pedido finalizado com sucesso.                 | ✅ Pass                                   |
| TC11 | Checkout com postal code inválido | Carrinho com itens           | 1. Faça o Login <br>2. Clique em "Add to Cart" <br>3. Clique no icone de Cart <br>4. Insira letras no campo de código postal. | Exibe mensagem de erro para entrada inválida.   | ❌ Fail - Permite letras no código postal. |

### 2.4 Filtro
| ID   | Descrição                     | Pré-condição           | Passos                                               | Resultado Esperado                              | Resultado Real                                   |
|------|-------------------------------|------------------------|-----------------------------------------------------|------------------------------------------------|-------------------------------------------------|
| TC12 | Filtro por preço              | Página de produtos aberta | 1. Faça o Login <br>2. Selecione um filtro no dropdown. | Produtos são ordenados corretamente.           | ✅ Pass                                  |
| TC13 | Nome de produto inválido      | Página de produtos aberta | 1. Faça o Login <br>2. Verifique os nomes dos produtos listados.        | Todos os nomes devem ser adequados.            | ⚠️ Pass, mas há um produto chamado `test.allTheThings()`. |

---

## 3. Resultados dos Testes

### 3.1 Tabela Resumida
| Cenário                  | Resultado |
|--------------------------|-----------|
| Login                   | ⚠️ Pequenas falhas de UI. |
| Carrinho                | ❌ Checkout com carrinho vazio permitido. |
| Checkout                | ❌ Código postal inválido aceito. |
| Filtro                  | ⚠️ Nome de produto inconsistente. |

---

## 4. Melhorias UX/UI
- **Mensagem de erro no login**: Mensagem cortada prejudica clareza.
- **Produto com nome técnico**: Substituir `test.allthethings()` por um nome mais comercial.
- **Carrinho vazio**: Bloquear finalização de compra se o carrinho estiver vazio.
- **Validação no checkout**: Implementar validação rigorosa para códigos postais.

---

## 5. Análise de Riscos
- **Risco Funcional**: Checkout vazio pode causar problemas financeiros e de estoque.
- **Risco UX/UI**: Mensagens de erro inadequadas podem confundir os usuários.
- **Risco Reputacional**: Produtos com nomes técnicos podem parecer inacabados para o cliente final.

---

## 6. Extras

### 6.1 Sugestões de Automação
- Automatizar fluxos críticos usando Cypress:
  - Login
  - Fluxo de compra
  - Testes de validação no checkout
