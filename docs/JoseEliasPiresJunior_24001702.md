# Avaliação — Engenharia de Software

**Sistema Integrado de Gestão de Farmácia — MVP**

Aluno: Jose Elias Pires Junior  
RA: 24001702  
Data: 25/03/2026

---

## 1. Definição do MVP

Nesse trabalho eu resolvi focar na parte que achei mais importante, que é o processo de venda da farmácia.

O meu MVP começa quando o cliente chega no balcão e vai até a hora que a venda é finalizada com o comprovante. Coloquei o estoque junto porque não tem como vender sem verificar isso antes.

**O que entrou no MVP:**

- Cadastro e identificação de cliente
- Busca de produto
- Fazer a venda (a vista ou a prazo)
- Verificar e atualizar o estoque
- Emitir o comprovante no final
- Controle básico de usuário por tipo (atendente, gerente)

**O que ficou fora:**

- Parte de compras e fornecedores
- Relatórios gerenciais
- Contas a pagar
- Movimentação entre unidades

**Por que escolhi assim:**  
Porque sem a venda funcionando nada mais faz sentido. Acho que é melhor acertar o principal primeiro do que tentar fazer tudo de uma vez.

---

## 2. Regras de Negócio

**RN01 — Sem estoque não vende**  
Se o produto não tiver disponível no estoque, o sistema não deixa continuar a venda. Simples assim.

**RN02 — Remédio controlado precisa de receita**  
Tem produtos que precisam de receita médica. Nesses casos o farmacêutico precisa liberar antes de vender.

**RN03 — Venda a prazo só pra quem tiver cadastrado**  
Se o cliente quiser pagar depois, ele precisa estar cadastrado no sistema. Sem cadastro não rola.

**RN04 — Estoque baixa sozinho**  
Quando a venda é concluída, o sistema já tira do estoque automatico. Não precisa de ninguém fazendo isso na mão.

**RN05 — Aviso quando o estoque tiver acabando**  
Se o produto chegar num nível baixo, o sistema avisa. Assim o gerente sabe que precisa repor.

**RN06 — Sempre gera comprovante**  
Toda venda finalizada tem que ter um comprovante, independente da forma de pagamento.

**RN07 — Cada perfil acessa só o que é dele**  
Atendente não pode mexer em produto, gerente não acessa financeiro, e por aí vai.

---

## 3. Requisitos Funcionais

**RF01 — Cadastrar cliente**  
O atendente consegue cadastrar um cliente novo com nome, CPF, telefone e endereço.

**RF02 — Buscar produto**  
Dá pra procurar produto por nome, código ou fabricante e ver o preço e estoque disponível.

**RF03 — Registrar venda**  
O sistema deixa fazer uma venda com um ou mais produtos.

**RF04 — Checar estoque antes de vender**  
Antes de confirmar um item, o sistema verifica se tem quantidade suficiente.

**RF05 — Fechar venda e emitir comprovante**  
Ao finalizar, o sistema gera o comprovante com os dados da venda.

**RF06 — Venda a prazo**  
Permite registrar venda pra pagar depois, e salva isso em contas a receber.

**RF07 — Farmacêutico validar receita**  
O farmacêutico consegue aprovar ou recusar uma receita pelo sistema.

**RF08 — Atualizar estoque depois da venda**  
Quando a venda fecha, o estoque é atualizado automatico.

**RF09 — Gerente cadastrar produto**  
O gerente pode adicionar produto novo com todas as informações.

**RF10 — Alertar estoque baixo**  
Quando o produto tiver abaixo do mínimo, o sistema avisa o gerente.

**RF11 — Ver contas a receber**  
O setor financeiro consegue ver as vendas a prazo em aberto, pagas ou atrasadas.

---

## 4. Requisitos Não Funcionais

**RNF01 — Velocidade**  
O sistema tem que responder rápido, sem travar na hora do atendimento.

**RNF02 — Segurança**  
Todo acesso precisa de login e senha. Cada usuário só entra no que é do seu perfil.

**RNF03 — Disponibilidade**  
Tem que funcionar durante todo o horário de funcionamento da farmácia.

**RNF04 — Fácil de usar**  
Tem que ser simples o bastante pra qualquer atendente conseguir usar sem dificuldade.

**RNF05 — Não pode salvar incompleto**  
Se der erro no meio da venda, o sistema não pode salvar pela metade. Tem que salvar tudo ou nada.

---

## 5. Casos de Uso

Os casos de uso do meu MVP são:

- UC01 — Registrar Venda
- UC02 — Identificar ou Cadastrar Cliente
- UC03 — Verificar Estoque
- UC04 — Emitir Comprovante
- UC05 — Registrar Venda a Prazo
- UC06 — Validar Receita Médica
- UC07 — Cadastrar Produto
- UC08 — Buscar Produto
- UC09 — Alertar Estoque Baixo
- UC10 — Ver Contas a Receber

**Relacionamentos principais:**

O UC01 (Registrar Venda) depende de outros casos pra funcionar. Ele sempre aciona o UC02 pra identificar o cliente, o UC08 pra buscar o produto e o UC03 pra checar o estoque — esses são includes porque sempre acontecem. Quando o pagamento é a prazo, ele aciona o UC05. Quando o produto é controlado, aciona o UC06 — esses só acontecem em situações específicas, então são extends. O UC03 quando identifica estoque baixo aciona o UC09.

Os atores principais são: Atendente, Farmacêutico, Gerente, Financeiro e o próprio Sistema.

---

## 6. Documentação dos Casos de Uso

---

### UC01 — Registrar Venda

**Ator:** Atendente

**Descrição:**  
O atendente faz o registro da venda. Ele busca o produto, verifica se tem em estoque, adiciona os itens e finaliza com comprovante.

**Antes de começar:**  
O atendente precisa estar logado e ter produto disponível.

**Depois que termina:**  
A venda fica salva, o estoque é atualizado e o comprovante é gerado.

**Como funciona:**

1. Atendente começa uma venda nova
2. Identifica se o cliente tem cadastro (ou cadastra na hora)
3. Busca o produto que o cliente quer
4. O sistema verifica o estoque
5. Atendente coloca a quantidade
6. Sistema calcula o valor e adiciona o item
7. Repete pros outros produtos se precisar
8. Atendente escolhe a forma de pagamento
9. Finaliza e o comprovante sai

**O que pode dar errado:**

- Se não tiver em estoque, o item é bloqueado
- Se o produto for controlado, tem que chamar o farmacêutico primeiro
- Se for a prazo, o sistema lança em contas a receber

**Relações com outros casos:**  
Depende de: UC02, UC03, UC08, UC04  
Em casos específicos aciona: UC05, UC06

---

**Fluxo de atividades — UC01:**

O atendente abre uma venda nova. Primeiro ele verifica se o cliente tem cadastro — se não tiver, cadastra na hora. Depois busca o produto. O sistema checa o estoque. Se não tiver, bloqueia e avisa. Se o produto for controlado, o farmacêutico precisa liberar antes. Estando tudo certo, o atendente coloca a quantidade, o sistema calcula o valor e adiciona o item. Se tiver mais produto, repete o processo. No final o atendente escolhe o pagamento — se for a prazo, o sistema já registra em contas a receber. Ao finalizar, o comprovante é gerado.

---

### UC02 — Identificar ou Cadastrar Cliente

**Ator:** Atendente

**Descrição:**  
O atendente verifica se o cliente já ta cadastrado. Se não tiver, faz o cadastro na hora.

**Antes de começar:**  
Atendente logado e com uma venda em andamento.

**Depois que termina:**  
Cliente vinculado à venda.

**Como funciona:**

1. Atendente digita CPF ou nome do cliente
2. Sistema procura na base
3. Se achar, vincula à venda
4. Se não achar, atendente preenche os dados e salva

**O que pode dar errado:**

- Venda à vista: o atendente pode optar por não identificar o cliente

**Relações:** é chamado pelo UC01

---

**Fluxo de atividades — UC02:**

O atendente digita o CPF ou nome. O sistema procura. Se encontrar, o cliente já fica vinculado à venda. Se não encontrar, o atendente preenche nome, CPF e telefone e salva. Em venda à vista o cliente pode nem ser identificado.

---

### UC03 — Verificar Estoque

**Ator:** Sistema

**Descrição:**  
O sistema checa se tem quantidade suficiente do produto antes de deixar adicionar na venda.

**Antes de começar:**  
Produto selecionado e quantidade informada.

**Depois que termina:**  
Item liberado ou bloqueado.

**Como funciona:**

1. Sistema pega o produto e a quantidade pedida
2. Consulta o estoque da unidade
3. Se tiver, libera o item
4. Se ficar abaixo do mínimo depois da venda, dispara o alerta

**O que pode dar errado:**

- Sem estoque suficiente: bloqueia o item e avisa

**Relações:** chamado pelo UC01, aciona UC09 quando necessário

---

**Fluxo de atividades — UC03:**

O sistema recebe o produto e a quantidade. Consulta o estoque. Se não tiver o suficiente, bloqueia e retorna erro. Se tiver, libera. Depois verifica se após a baixa o estoque vai ficar abaixo do mínimo — se sim, aciona o alerta do UC09.

---

### UC04 — Emitir Comprovante

**Ator:** Sistema

**Descrição:**  
Depois que a venda é finalizada, o sistema monta e exibe o comprovante.

**Antes de começar:**  
Venda concluída com sucesso.

**Depois que termina:**  
Comprovante disponível pra imprimir ou fechar.

**Como funciona:**

1. Sistema recebe que a venda foi finalizada
2. Monta o comprovante com: data, cliente, itens e pagamento
3. Exibe na tela
4. Atendente decide se imprime ou só fecha

**O que pode dar errado:**

- Erro ao gerar: sistema salva um log mas a venda continua salva

**Relações:** chamado pelo UC01

---

**Fluxo de atividades — UC04:**

Venda finalizada. Sistema coleta os dados e monta o comprovante. Se der erro, registra e avisa, mas a venda já ta salva. Se não der erro, exibe o comprovante. Atendente imprime ou fecha.

---

### UC05 — Registrar Venda a Prazo

**Ator:** Sistema e Atendente

**Descrição:**  
Quando o cliente vai pagar depois, o sistema registra isso como uma conta a receber.

**Antes de começar:**  
Cliente cadastrado e pelo menos um item na venda.

**Depois que termina:**  
Lançamento criado em contas a receber com situação "Aberta".

**Como funciona:**

1. Atendente escolhe pagamento a prazo
2. Sistema verifica se cliente ta cadastrado
3. Cria o lançamento em contas a receber
4. Volta pra finalizar a venda

**O que pode dar errado:**

- Cliente sem cadastro: bloqueia e pede pra cadastrar antes

**Relações:** acionado pelo UC01 quando o pagamento é a prazo

---

**Fluxo de atividades — UC05:**

Atendente escolhe a prazo. O sistema verifica se tem cliente. Se não tiver, bloqueia. Se tiver, cria o lançamento em contas a receber com valor, vencimento e situação Aberta. Depois volta pra finalizar a venda normalmente.

---

### UC06 — Validar Receita Médica

**Ator:** Farmacêutico

**Descrição:**  
Quando o produto é controlado, o farmacêutico precisa olhar a receita e liberar antes de continuar a venda.

**Antes de começar:**  
Produto controlado adicionado na venda e farmacêutico disponível.

**Depois que termina:**  
Item liberado ou recusado.

**Como funciona:**

1. Sistema detecta produto controlado
2. Avisa o farmacêutico
3. Farmacêutico olha a receita do cliente
4. Aprova ou recusa
5. Se aprovar, a venda continua

**O que pode dar errado:**

- Receita ruim ou sem receita: farmacêutico recusa e o item é bloqueado

**Relações:** acionado pelo UC01 quando o produto é controlado

---

**Fluxo de atividades — UC06:**

Sistema detecta produto controlado. Avisa o farmacêutico. Farmacêutico analisa a receita. Se a receita tiver boa, libera o item e volta pro UC01. Se não tiver, recusa e o item é removido da venda.

---

### UC07 — Cadastrar Produto

**Ator:** Gerente

**Descrição:**  
O gerente adiciona um produto novo no sistema.

**Antes de começar:**  
Gerente logado.

**Depois que termina:**  
Produto salvo e disponível pra venda.

**Como funciona:**

1. Gerente abre a tela de produto
2. Preenche nome, código, preço, fabricante e estoque mínimo
3. Sistema valida os dados
4. Salva

**O que pode dar errado:**

- Código já existe: não salva e avisa
- Campo obrigatório vazio: destaca e bloqueia

**Relações:** nenhuma com outros casos de uso

---

**Fluxo de atividades — UC07:**

Gerente abre o cadastro. Preenche os dados do produto. Se o código já existir, o sistema avisa e não salva duplicado. Se algum campo obrigatório estiver vazio, também bloqueia. Se tudo estiver ok, salva o produto.

---

### UC08 — Buscar Produto

**Ator:** Atendente

**Descrição:**  
O atendente busca o produto pelo nome ou código pra adicionar na venda.

**Antes de começar:**  
Atendente com venda em andamento.

**Depois que termina:**  
Produto selecionado pra adicionar.

**Como funciona:**

1. Atendente digita o nome ou código
2. Sistema mostra os resultados
3. Atendente escolhe o produto
4. Sistema mostra preço e estoque

**O que pode dar errado:**

- Nada encontrado: sistema avisa e permite nova busca

**Relações:** chamado pelo UC01

---

**Fluxo de atividades — UC08:**

Atendente digita o que quer buscar. Sistema retorna os resultados. Se não achar nada, avisa. Se achar, o atendente seleciona e o sistema mostra preço e estoque disponível.

---

### UC09 — Alertar Estoque Baixo

**Ator:** Sistema e Gerente

**Descrição:**  
Quando o estoque de algum produto fica abaixo do mínimo, o sistema manda um aviso pro gerente.

**Antes de começar:**  
Produto com mínimo configurado e estoque atualizado após venda.

**Depois que termina:**  
Gerente fica sabendo que precisa repor.

**Como funciona:**

1. Sistema percebe que o estoque chegou no mínimo
2. Gera o aviso com nome do produto e quantidades
3. Mostra pro gerente

**O que pode dar errado:**

- Gerente offline: aviso fica salvo e aparece quando ele logar

**Relações:** acionado pelo UC03

---

**Fluxo de atividades — UC09:**

O UC03 percebe que o estoque vai ficar abaixo do mínimo. O sistema monta o aviso. Se o gerente ta logado, aparece na hora. Se não ta, fica salvo pra mostrar depois.

---

### UC10 — Ver Contas a Receber

**Ator:** Financeiro

**Descrição:**  
O setor financeiro consulta as vendas a prazo, podendo filtrar por situação.

**Antes de começar:**  
Usuário financeiro logado.

**Depois que termina:**  
Lista exibida conforme o filtro.

**Como funciona:**

1. Financeiro entra no módulo de contas a receber
2. Sistema mostra todos os lançamentos
3. Financeiro pode filtrar por: Aberta, Recebida ou Atrasada
4. Lista atualiza

**O que pode dar errado:**

- Filtro sem resultado: sistema mostra mensagem informando que não tem nada

**Relações:** nenhuma com outros casos de uso

---

**Fluxo de atividades — UC10:**

Financeiro acessa o módulo. Sistema mostra tudo. Se quiser, o financeiro aplica um filtro por situação. A lista atualiza. Se não tiver nada no filtro, aparece uma mensagem.
