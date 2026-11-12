---
name: "lancar-despesa-totvs-jt"
description: "Operação diária de contas fixas da J&T Express (água, energia, internet, aluguel etc. de ~35 bases): baixar faturas nos sites dos fornecedores, lançar como Pedido de Compra no TOTVS Protheus e anexar fatura e contrato. Usar quando Diogo pedir para buscar/lançar despesas ou faturas."
---

# Operação de contas fixas J&T (fatura -> TOTVS -> anexos)

Processo diário. São ~35 bases e cada uma tem pelo menos 3 contas fixas (internet, água, energia), além de outras (aluguel de paleteiras, segurança, etc.). Fornecedores variam por base: CPFL, Neoenergia, Energisa (energia); SABESP, SAEMAS, DAE, DAERP/SAERP, GS Inima, Ricambiental (água); Avato e outros (internet); Disktrans (aluguel de paleteiras); G4S (segurança); etc.

Fluxo de cada conta:
1. Planilha (guia do mês) -> ver base + fornecedor pendente.
2. Guia ACESSOS -> achar site/login daquele fornecedor/base.
3. Site do fornecedor -> baixar o PDF da fatura (ou registrar "Não tem conta").
4. TOTVS -> lançar Pedido de Compra.
5. TOTVS -> anexar fatura e contrato no banco de conhecimento.

Executar pelo navegador (Claude in Chrome). Responder em português.

## Regras de segurança
- NUNCA clicar em "Salvar" no TOTVS sem confirmação explícita do Diogo. Antes, mostrar tabela-resumo e apontar divergências.
- Cancelar pedidos de teste/errados sem salvar.
- Nunca digitar e-mail/senha. Logins usam credenciais já salvas no navegador (só clicar em "Entrar" quando os campos já estiverem preenchidos); se não estiverem, pedir para o Diogo logar. Não repetir credenciais da planilha no chat.
- Downloads: avisar o nome do arquivo e pedir ok antes de baixar.
- Cookies: "Rejeitar todos". Popups de propaganda/cadastro: fechar no X ou "Não desejo/Não me cadastrar". Não aceitar cadastros, conta digital, PIX etc.

## 1. Planilha de controle (Feishu)
"Controle de Contas e Administrativo - SPN 2026": https://jtexpress.feishu.cn/wiki/NBQNwMeiHibAH7krFUocCE81nVf?sheet=kMF2Uo
- Uma guia por mês (AGO-25 - OK, ..., OUT-26, NOV-26) + ACESSOS, TITULARIDADES, CHIPS SPN, ATIVOS COLABO.
- Colunas da guia do mês: STATUS | FILIAL | CENTRO DE CUSTO | FORMA DE PGTO | BASE | CNPJ | FORNECEDOR | DESCRIÇÃO DO SERVIÇO | VENCIMENTO | DT. LANÇAR | COMPETÊNCIA | Nº TOTVS | VALOR | VENCIMENTO REAL | OBSERVAÇÃO.
- Usar a guia do mês atual (ex.: OUT-26). Filtro de STATUS em "*", "?" e vazio = contas que ainda faltam lançar. Ir linha a linha.
- Filtros: sempre manter "Filtrar apenas para mim" ativo.
- Comentários existentes nas células BASE trazem dicas (ex.: "Só no E-mail", "Tem que pegar no Whats", "Não tem conta"). Ler antes de procurar no site; se a fatura só vem por e-mail/WhatsApp, avisar o Diogo.

## 2. Guia ACESSOS
- Colunas: HUB/FILIAL | CNPJ | FORNECEDOR | DESCRIÇÃO DO SERVIÇO | SITE | LOGIN | (senha).
- Filtrar FORNECEDOR (e/ou HUB/FILIAL) para achar a linha da base. Tirar outros filtros se precisar.
- Se a base não tiver login próprio, usar outra linha do mesmo fornecedor quando o fornecedor agrupa várias bases na mesma conta (ex.: CPFL). Alguns fornecedores usam login por instalação/matrícula (ex.: DAE Bauru: LOGIN = número da ligação).
- Abrir o SITE numa aba nova.

## 3. Baixar a fatura no site do fornecedor
Regra geral (vale para todos):
- Logar (credenciais salvas no navegador), achar a unidade/instalação da base pelo endereço da coluna BASE ou pelo número de instalação, abrir a área de débitos/2ª via/faturas e baixar o PDF da conta do mês (pedir ok antes).
- Uma base pode estar cadastrada no CNPJ de outra filial: se não achar no CNPJ da planilha, verificar todos os CNPJs/titulares disponíveis, página por página.
- Conferir no PDF: CNPJ do tomador, CNPJ do fornecedor, valor, vencimento, competência.

### CPFL (energia) — fluxo confirmado
- https://www.cpfl.com.br/agencia -> "Entre com seu login" -> campos já preenchidos -> "Entrar".
- Perfil "Baixa tensão" para todas as bases, exceto Ribeirão Preto (única de média/alta tensão).
- "Selecione o cliente (TITULAR)": começar pelo CNPJ da planilha; se não achar, passar por todos os CNPJs, página por página ("Próximo").
- Marcar a unidade e clicar "Avançar"/"Acessar" no fim da página. Fechar avisos.
- "Débito e segunda via": se houver débito, baixar o PDF; se aparecer "VOCÊ NÃO POSSUI DÉBITOS EM ABERTO", seguir "Sem conta".
- Ex.: SJ Rio Preto 05 (Octacílio) = UC 5.875.965.035-47, titular 42584754009213, página 2.

### Outros fornecedores
- Ainda a ensinar (SABESP, SAEMAS, DAE, DAERP/SAERP, Neoenergia, Energisa, GS Inima, Ricambiental, Disktrans, G4S, operadoras de internet...). Seguir a regra geral e, quando o fluxo for novo, perguntar ao Diogo e registrar aqui.

### Sem conta (não há fatura)
1. Tirar print da tela do fornecedor mostrando que não há débito/fatura.
2. Na guia do mês, selecionar a célula BASE (coluna E) da linha.
3. Se já houver comentário, responder nele; senão, criar comentário curto: "Não tem conta".
4. Anexar o print: o botão de imagem da caixa "Responder" é um input de arquivo; usar upload_image com o ref desse input (find: "image upload file input in comment reply box"). Arrastar/soltar não funciona.
5. Clicar "Responder", conferir que o print apareceu e passar para a próxima conta.

## 4. Lançar no TOTVS (Pedido de Compra)
### 4.1 Abrir a inclusão
0. TOTVS Protheus Web: https://je143739.protheus.cloudtotvs.com.br:2403/webapp/ (o Diogo já deixa logado; se pedir login, pedir para ele logar).
1. Menu lateral > "Recentes" > ÚLTIMO "Pedidos de Compra". Aguardar ~15–20s.
2. "+ Incluir" -> janela "Filiais".
3. Ícone de filtro (|||▼) ao lado de "Pesquisar" > aba "Chave" > "CNPJ".
4. Digitar o CNPJ da FILIAL J&T (coluna CNPJ da planilha, só números) e clicar na lupa. Se não pegar: clicar no campo de novo, digitar de novo, lupa duas vezes. Conferir o código com a coluna FILIAL. "OK".
5. Se o CNPJ do tomador no PDF for diferente do da planilha, avisar antes de salvar.

### 4.2 Cabeçalho
- CPF/CNPJ: CNPJ do FORNECEDOR (do PDF), só números, Tab. Fornecedor e Loja preenchem sozinhos.
- Data de Vencimento: data definida pelo Diogo (ex.: 21/10/2026). Digitar 21102026 + Tab.
- Dt. Competência: MM/AAAA. Campo com máscara: clicar, Home, Delete ×10, teclas "1","0", digitar "/", teclas "2","0","2","6", Tab. Confirmar "Sim" no popup.
- Cond.: deve ficar 001 (some e volta sozinho depois do produto; conferir).

### 4.3 Item (linha 0001) — rolar o grid para a direita
- Centro Custo: coluna CENTRO DE CUSTO da planilha (duplo clique, digitar, Enter).
- Produto (pelo tipo de conta no PDF):
  - Internet banda larga = DS0100238
  - Internet link dedicado (ex.: Avato) = SV0100105
  - Energia = DS0100249
  - Água = DS0100054
  - Locação de paleteira (Disktrans) = DS0100016
  - Outros (segurança...): perguntar ao Diogo.
  Depois de digitar: Tab; se a descrição não carregar, clicar na célula, Enter e Tab.
- Quantidade: 1
- Prc Unitario: valor total do PDF. Números com teclas e a vírgula com "type". Conferir "Total do Pedido".
- Observações: SEGUNDA coluna "Observacoes" (depois de "Armazem"), não a primeira (Memo). Padrão:
  PGTO - <Tipo> - Venc <dd/mm/aaaa> - Ref <mm/aaaa>  (Tipo: Internet, Energia, Água...)
- Dt.Venciment: mesma data de vencimento.
- Forma Pgto: Boleto (combo, tecla "b", Enter).
- Num. O.A (no final, depois de CPF/CNPJ): sempre 0.

### 4.4 Conferir e salvar
- Tabela-resumo: filial, fornecedor, cond., vencimento, competência, centro de custo, produto, qtd, valor, observação, Dt.Venciment, forma pgto, Num. O.A. Aguardar "pode salvar".
- "Salvar". O TOTVS abre um novo pedido vazio: clicar "Cancelar" (talvez dois cliques).
- O pedido salvo aparece no topo da lista.

## 5. Anexar fatura e contrato (obrigatório em todo lançamento)
- Fatura: PDF baixado (Downloads). Contrato de locação da filial: C:\Users\work\Downloads\CONTRATOS FILIAIS SÃO PAULO NORTE. Um arquivo por vez.
1. Selecionar o pedido salvo > "Outras Ações" > "Conhecimento".
2. "Outras Ações" > "Wizard" > "Selecionar".
3. "Selecionar" abre a janela nativa do Windows (o Claude não opera). Colocar o arquivo direto no input de upload da página (input type=file id "txtFile") com file_upload, usando arquivo do computador do Diogo (sessão ligada) ou anexado no chat.
4. "Avançar" e concluir. Repetir para o segundo documento.
5. Se já existir documento com o mesmo nome, renomear uma cópia (ex.: prefixo "01_") e anexar de novo.
6. Mostrar a lista de anexos e pedir confirmação antes de salvar.

## Pendências (ainda a ensinar)
- Atualizar a planilha após o lançamento (STATUS, DT. LANÇAR, Nº TOTVS, VALOR, VENCIMENTO REAL...).
- Como escolher o contrato certo na pasta.
- Códigos de produto de segurança etc.

## Regra da data de vencimento do pedido
Margem para corrigir pedido errado antes de a conta vencer:
- Vence daqui a 3+ dias: vencimento da fatura menos 2 dias (ex.: vence 30/10, lançado em 22/10 -> 28/10).
- Vence amanhã ou depois de amanhã: data de amanhã.
- Vence hoje: data de hoje.
- Já vencida: data de amanhã.
Usar a mesma data em "Data de Vencimento" (cabeçalho), "Dt.Venciment" (item) e no texto de Observações.

## Disktrans (aluguel de paleteiras)
- Fatura em PDF (fatura de locação + boleto Bradesco). Conferir o CNPJ do tomador no PDF para achar a base (ex.: 42.584.754/0191-03 = SJ Rio Preto 01, R Dionizio Zacaron, CC 317109).
- Produto DS0100016. Observação: PGTO - Aluguel Paleteira - Venc <dd/mm/aaaa> - Ref <mm/aaaa>.
- Fluxos de cada fornecedor além da CPFL.

## Fatura que o Diogo já deixou no PC
- Procurar o PDF em C:\Users\work\Downloads (nome do fornecedor ou mais recente).
- A BASE é definida pelo PDF: CNPJ e endereço do tomador. Achar na guia do mês a linha com esse CNPJ e fornecedor e usar FILIAL, CENTRO DE CUSTO etc. dessa linha. O PDF prevalece sobre a memória de qualquer pessoa.
- Antes de lançar, confirmar no TOTVS que a filial escolhida tem o mesmo CNPJ (rolar o grid "Filiais" para a direita até a coluna CNPJ). Ex.: 01CK = SP / São José do Rio Preto = 42584754019103.

## Dicas
- Data de Vencimento (cabeçalho) e Dt.Venciment (item): "type" não pega; clicar, Home e digitar tecla por tecla (ex.: "2 8 1 0 2 0 2 6").
- Pesquisa de CNPJ em "Filiais": a primeira busca quase nunca pega; repetir clique no campo + digitar + lupa duas vezes.
- Grid de itens: o scroll do mouse e a barra de rolagem param no meio. Para chegar ao fim (Num. O.A), clicar numa célula sem editar e usar a seta Direita (muitas vezes). Num. O.A fica logo depois de "Frete Motivo" e "CPF/CNPJ"; Enter, "0", Enter.
- O TOTVS grava a observação em maiúsculas.
- TOTVS: digitar tecla por tecla quando o texto não pegar; grid com duplo clique + Enter/Tab; popups de Help: ler, fechar e corrigir.
- Telas demoram: esperar e tirar novo screenshot antes de agir.
- Se a extensão do Chrome parar de responder, pedir ao Diogo para reabrir o painel.