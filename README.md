# Atividade Somativa 2 - Jesus Wildes - Banco de Dados Aplicado à BIG Data

Esse trabalho visa contemplar nota para a Atividade Somativa 2 da Disciplina de Banco de Dados Aplicado à BIG Data da Pontifícia Universidade Católica do Paraná (PUC-PR).

## Desafio
>Esta atividade deve ser realizada individualmente.
>
>Para demonstrar seus conhecimentos, usando o Neo4J, nesta atividade, propomos a criação de um sistema de cadastros de vendedores de uma empresa de cosméticos. Nesse sentido, observe os tópicos a seguir e suas dependências.
>
> 1. Regiões:
>
> - Central
>    - Região Sul
>       - Curitiba
>       - Florianópolis
>       - Porto Alegre
>    - Região Norte
>       - Manaus
>       - Belém
>       - Porto Velho
>    - Região Oeste
>       - Brasília
>       - Goiânia
>       - Campo Grande
>    - Região Leste
>       - São Paulo
>       - Rio de Janeiro
>       - Belo Horizonte
>
>Partindo da central, você deve criar um nó para cada região e depois para cada cidade e depois fazer as ligações de dependência até chegar na central. Após isso, você fará o cadastro do supervisor. Um supervisor para cada cidade (Insira informações fictícias para cada supervisor). Esse nó deve estar ligado como pertencente à sua cidade. E nele deve conter as seguintes informações de cadastro:
>
> - Nome completo.
> - CPF.
> - Endereço com bairro
> - Telefone
>
>Por fim, você precisa cadastrar para cada supervisor um número aleatório entre 1 e 3 vendedores, que por sua vez, são ligados em relação aos seus supervisores. Você precisa cadastrar para cada vendedor as seguintes informações fictícias:
>
> - Nome completo.
> - CPF
> - Telefone
> - Endereço.
> - E-mail.
>
>Ao finalizar a atividade, para a entrega, encaminhe os scripts gerados por um arquivo .txt ou PDF, e uma imagem contendo a rede de grafos da sua atividade. Você pode gerar um único PDF contendo tudo, ou criar um arquivo .ZIP com o texto e imagem.
>
>Desejamos uma ótima atividade!

## Resolução
```cypher
CREATE
  // --- REGIÕES ---
  (central:Região {Nome: 'Central'}),
  (sul:Região {Nome: 'Sul'})-[:Pertence]->(central),
  (norte:Região {Nome: 'Norte'})-[:Pertence]->(central),
  (oeste:Região {Nome: 'Oeste'})-[:Pertence]->(central),
  (leste:Região {Nome: 'Leste'})-[:Pertence]->(central),

  // --- CIDADES ---
  // Região Sul
  (curitiba:Cidade {Nome: 'Curitiba'})-[:Pertence]->(sul),
  (florianopolis:Cidade {Nome: 'Florianópolis'})-[:Pertence]->(sul),
  (portoAlegre:Cidade {Nome: 'Porto Alegre'})-[:Pertence]->(sul),

  // Região Norte
  (manaus:Cidade {Nome: 'Manaus'})-[:Pertence]->(norte),
  (belem:Cidade {Nome: 'Belém'})-[:Pertence]->(norte),
  (portoVelho:Cidade {Nome: 'Porto Velho'})-[:Pertence]->(norte),

  // Região Oeste
  (brasilia:Cidade {Nome: 'Brasília'})-[:Pertence]->(oeste),
  (goiania:Cidade {Nome: 'Goiânia'})-[:Pertence]->(oeste),
  (campoGrande:Cidade {Nome: 'Campo Grande'})-[:Pertence]->(oeste),

  // Região Leste
  (saoPaulo:Cidade {Nome: 'São Paulo'})-[:Pertence]->(leste),
  (rioDeJaneiro:Cidade {Nome: 'Rio de Janeiro'})-[:Pertence]->(leste),
  (beloHorizonte:Cidade {Nome: 'Belo Horizonte'})-[:Pertence]->(leste),

  // --- SUPERVISORES ---
  // Região sul
  (superCuritiba:Supervisor 
    {Nome: 'Alberto Fagundes', CPF: '111.111', Telefone: '(41) 98888-1111', Endereço: 'Rua A, 1, Centro'})-
    [:Supervisiona]->
  (curitiba),
  (superFlorianopolis:Supervisor 
    {Nome: 'Bruna Marquez', CPF: '222.222', Telefone: '(48) 98888-2222', Endereço: 'Rua B, 2, São Tadeu'})-
    [:Supervisiona]->
  (florianopolis),
  (superPortoAlegre:Supervisor 
    {Nome: 'Carlos Telles', CPF: '333.333', Telefone: '(51) 98888-3333', Endereço: 'Rua C, 3, Braz'})-
    [:Supervisiona]->
  (portoAlegre),

  // Região Norte
  (superManaus:Supervisor 
    {Nome: 'Daniela Souza', CPF: '444.444', Telefone: '(92) 98888-4444', Endereço: 'Rua D, 4, Ahú'})-
    [:Supervisiona]->
  (manaus),
  (superBelem:Supervisor 
    {Nome: 'Eduardo Lima', CPF: '555.555', Telefone: '(91) 98888-5555', Endereço: 'Rua E, 5, Bairro Alto'})-
    [:Supervisiona]->
  (belem),
  (superPortoVelho:Supervisor 
    {Nome: 'Fernanda Nogueira', CPF: '666.666', Telefone: '(69) 98888-6666', Endereço: 'Rua F, 6, Alvorada'})-
    [:Supervisiona]->
  (portoVelho),

  // Região Oeste
  (superBrasilia:Supervisor 
    {Nome: 'Gabriel Castro', CPF: '777.777', Telefone: '(61) 98888-7777', Endereço: 'Rua G, 7, Paraíso'})-
    [:Supervisiona]->
  (brasilia),
  (superGoiania:Supervisor 
    {Nome: 'Helena Moraes', CPF: '888.888', Telefone: '(62) 98888-8888', Endereço: 'Rua H, 8, Flamengo'})-
    [:Supervisiona]->
  (goiania),
  (superCampoGrande:Supervisor 
    {Nome: 'Igor Rocha', CPF: '999.999', Telefone: '(67) 98888-9999', Endereço: 'Rua I, 9, Mutuá'})-
    [:Supervisiona]->
  (campoGrande),

  // Região Leste
  (superSaoPaulo:Supervisor 
    {Nome: 'Juliana Paes', CPF: '123.123', Telefone: '(11) 98888-0000', Endereço: 'Rua J, 10, Cidade Nova'})-
    [:Supervisiona]->
  (saoPaulo),
  (superRioDeJaneiro:Supervisor 
    {Nome: 'Kleber Toledo', CPF: '124.124', Telefone: '(21) 98888-1010', Endereço: 'Rua K, 11, Jorge Teixeira'})-
    [:Supervisiona]->
  (rioDeJaneiro),
  (superBeloHorizonte:Supervisor 
    {Nome: 'Laura Mendes', CPF: '125.125', Telefone: '(31) 98888-2020', Endereço: 'Rua L, 12, Educandos'})-
    [:Supervisiona]->
  (beloHorizonte),

  // --- VENDEDORES ---
  // Região Sul
  // Curitiba (2 Vendedores)
  (v1:Vendedor
    {
      Nome: 'Carlos Almeida',
      CPF: '159753',
      Telefone: '(41) 99123-4567',
      Endereço: 'Rua XV de Novembro, 100, Curitiba',
      `E-mail`: 'carlos.almeida@email.com'
    })-
    [:Responde_A]->
  (superCuritiba),
  (v2:Vendedor
    {
      Nome: 'Mariana Costa',
      CPF: '753159',
      Telefone: '(41) 99876-5432',
      Endereço: 'Av. Visconde de Guarapuava, 500, Curitiba',
      `E-mail`: 'mariana.costa@email.com'
    })-
    [:Responde_A]->
  (superCuritiba),

  // Florianópolis (1 Vendedor)
  (v3:Vendedor
    {
      Nome: 'Felipe Rocha',
      CPF: '258456',
      Telefone: '(48) 99111-2222',
      Endereço: 'Av. Beira Mar Norte, 200, Florianópolis',
      `E-mail`: 'felipe.rocha@email.com'
    })-
    [:Responde_A]->
  (superFlorianopolis),

  // Porto Alegre (2 Vendedores)
  (v4:Vendedor
    {
      Nome: 'Juliana Mendes',
      CPF: '369852',
      Telefone: '(51) 99333-4444',
      Endereço: 'Rua dos Andradas, 300, Porto Alegre',
      `E-mail`: 'juliana.mendes@email.com'
    })-
    [:Responde_A]->
  (superPortoAlegre),
  (v5:Vendedor
    {
      Nome: 'Roberto Nunes',
      CPF: '147258',
      Telefone: '(51) 99555-6666',
      Endereço: 'Av. Borges de Medeiros, 400, Porto Alegre',
      `E-mail`: 'roberto.nunes@email.com'
    })-
    [:Responde_A]->
  (superPortoAlegre),

  // Região Norte
  // Manaus (2 Vendedores)
  (v6:Vendedor
    {
      Nome: 'Amanda Silva',
      CPF: '951357',
      Telefone: '(92) 99777-8888',
      Endereço: 'Av. Djalma Batista, 500, Manaus',
      `E-mail`: 'amanda.silva@email.com'
    })-
    [:Responde_A]->
  (superManaus),
  (v7:Vendedor
    {
      Nome: 'Lucas Oliveira',
      CPF: '357159',
      Telefone: '(92) 99999-0000',
      Endereço: 'Av. Eduardo Ribeiro, 600, Manaus',
      `E-mail`: 'lucas.oliveira@email.com'
    })-
    [:Responde_A]->
  (superManaus),

  // Belém (1 Vendedor)
  (v8:Vendedor
    {
      Nome: 'Camila Santos',
      CPF: '852456',
      Telefone: '(91) 99222-3333',
      Endereço: 'Av. Nazaré, 700, Belém',
      `E-mail`: 'camila.santos@email.com'
    })-
    [:Responde_A]->
  (superBelem),
  // Porto Velho (2 Vendedores)
  (v9:Vendedor
    {
      Nome: 'Diego Ferreira',
      CPF: '741852',
      Telefone: '(69) 99444-5555',
      Endereço: 'Av. Sete de Setembro, 800, Porto Velho',
      `E-mail`: 'diego.ferreira@email.com'
    })-
    [:Responde_A]->
  (superPortoVelho),
  (v10:Vendedor
    {
      Nome: 'Patricia Lima',
      CPF: '963852',
      Telefone: '(69) 99666-7777',
      Endereço: 'Av. Carlos Gomes, 900, Porto Velho',
      `E-mail`: 'patricia.lima@email.com'
    })-
    [:Responde_A]->
  (superPortoVelho),

  // Região Oeste
  // Brasília (2 Vendedores)
  (v11:Vendedor
    {
      Nome: 'Ricardo Pereira',
      CPF: '123789',
      Telefone: '(61) 98888-9999',
      Endereço: 'Eixo Monumental, Bloco A, Brasília',
      `E-mail`: 'ricardo.pereira@email.com'
    })-
    [:Responde_A]->
  (superBrasilia),
  (v12:Vendedor
    {
      Nome: 'Fernanda Gomes',
      CPF: '987321',
      Telefone: '(61) 98111-2222',
      Endereço: 'SQS 102, Bloco B, Brasília',
      `E-mail`: 'fernanda.gomes@email.com'
    })-
    [:Responde_A]->
  (superBrasilia),

  // Goiânia (3 Vendedores)
  (v13:Vendedor
    {
      Nome: 'Eduardo Martins',
      CPF: '456123',
      Telefone: '(62) 98333-4444',
      Endereço: 'Av. Anhanguera, 1000, Goiânia',
      `E-mail`: 'eduardo.martins@email.com'
    })-
    [:Responde_A]->
  (superGoiania),
  (v14:Vendedor
    {
      Nome: 'Beatriz Ribeiro',
      CPF: '654789',
      Telefone: '(62) 98555-6666',
      Endereço: 'Praça Cívica, 50, Goiânia',
      `E-mail`: 'beatriz.ribeiro@email.com'
    })-
    [:Responde_A]->
  (superGoiania),
  (v15:Vendedor
    {
      Nome: 'Tiago Alves',
      CPF: '321654',
      Telefone: '(62) 98777-8888',
      Endereço: 'Av. T-63, 1200, Goiânia',
      `E-mail`: 'tiago.alves@email.com'
    })-
    [:Responde_A]->
  (superGoiania),

  // Campo Grande (1 Vendedor)
  (v16:Vendedor
    {
      Nome: 'Larissa Barros',
      CPF: '789123',
      Telefone: '(67) 99111-0000',
      Endereço: 'Av. Afonso Pena, 1500, Campo Grande',
      `E-mail`: 'larissa.barros@email.com'
    })-
    [:Responde_A]->
  (superCampoGrande),

  // --- Região Leste ---
  // São Paulo (3 Vendedores)
  (v17:Vendedor
    {
      Nome: 'Marcelo Castro',
      CPF: '321987',
      Telefone: '(11) 99222-1111',
      Endereço: 'Av. Paulista, 2000, São Paulo',
      `E-mail`: 'marcelo.castro@email.com'
    })-
    [:Responde_A]->
  (superSaoPaulo),
  (v18:Vendedor
    {
      Nome: 'Aline Moura',
      CPF: '654321',
      Telefone: '(11) 99444-2222',
      Endereço: 'Av. Faria Lima, 3000, São Paulo',
      `E-mail`: 'aline.moura@email.com'
    })-
    [:Responde_A]->
  (superSaoPaulo),
  (v19:Vendedor
    {
      Nome: 'Thiago Mendes',
      CPF: '159263',
      Telefone: '(11) 99666-3333',
      Endereço: 'Rua Augusta, 400, São Paulo',
      `E-mail`: 'thiago.mendes@email.com'
    })-
    [:Responde_A]->
  (superSaoPaulo),

  // Rio de Janeiro (2 Vendedores)
  (v20:Vendedor
    {
      Nome: 'Carolina Dias',
      CPF: '852963',
      Telefone: '(21) 99888-4444',
      Endereço: 'Av. Atlântica, 100, Rio de Janeiro',
      `E-mail`: 'carolina.dias@email.com'
    })-
    [:Responde_A]->
  (superRioDeJaneiro),
  (v21:Vendedor
    {
      Nome: 'Rodrigo Silva',
      CPF: '741258',
      Telefone: '(21) 99111-5555',
      Endereço: 'Av. Nossa Senhora de Copacabana, 200, Rio de Janeiro',
      `E-mail`: 'rodrigo.silva@email.com'
    })-
    [:Responde_A]->
  (superRioDeJaneiro),

  // Belo Horizonte (2 Vendedores)
  (v22:Vendedor
    {
      Nome: 'Vanessa Teixeira',
      CPF: '369147',
      Telefone: '(31) 99333-6666',
      Endereço: 'Av. Afonso Pena, 3000, Belo Horizonte',
      `E-mail`: 'vanessa.teixeira@email.com'
    })-
    [:Responde_A]->
  (superBeloHorizonte),
  (v23:Vendedor
    {
      Nome: 'Bruno Vieira',
      CPF: '258369',
      Telefone: '(31) 99555-7777',
      Endereço: 'Av. do Contorno, 4000, Belo Horizonte',
      `E-mail`: 'bruno.vieira@email.com'
    })-
    [:Responde_A]->
  (superBeloHorizonte)
```

## Imagem da Rede de Grafos
![alt](grafos.svg)
