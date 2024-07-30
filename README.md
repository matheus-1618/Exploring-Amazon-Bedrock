# Exploring-Amazon-Bedrock

O Amazon Bedrock é um serviço totalmente gerenciado que oferece várias opções de modelos de base (FMs) de alta performance das principais empresas de IA, como AI21 Labs, Anthropic, Cohere, Meta, Mistral AI, Stability AI e Amazon, por meio de uma única API, além de um amplo conjunto de recursos necessários para criar aplicações de IA generativa com segurança, privacidade e IA responsável. Usando o Amazon Bedrock, é fácil experimentar e avaliar os principais FMs para o seu caso de uso, personalizá-los de maneira privada com seus dados.

<div align=center>
  
![image](https://github.com/user-attachments/assets/1245d8de-3069-4023-aee1-957216173f6e)

</div>

## O que é um prompt?

Um prompt é um texto em linguagem natural que solicita que a IA generativa execute uma tarefa específica. A IA generativa é uma solução de inteligência artificial que cria novos conteúdos, como histórias, conversas, vídeos, imagens e músicas. Ela é alimentada por modelos muito grandes de machine learning (ML) que usam as redes neurais profundas que foram pré-treinadas em grandes quantidades de dados.

### Estrutura de um (bom) prompt

1. Contexto da tarefa 
2. Contexto do tom / roleplay
3. Dados, documentos e imagens de background 
4. Descrição detalhada da tarefa e regras 
5. Exemplos 
6. Histórico da conversa 
7. Descrição imediata da tarefa ou solicitação 
8. Pensando passo a passo
9. Formatação da saída

## Prompt Engineering
Prompt Engineering é o processo em que você orienta as soluções de inteligência artificial generativa (IA generativa) para gerar os resultados desejados. Embora a IA generativa tente imitar os humanos, ela requer instruções detalhadas para criar resultados relevantes e de alta qualidade. Na engenharia de prompt, você escolhe os formatos, frases, palavras e símbolos mais adequados para orientar a IA a interagir com seus usuários de forma mais significativa. Os engenheiros de prompt usam a criatividade e tentativa e erro para criar uma coleção de textos de entrada, para que a IA generativa de uma aplicação funcione conforme o esperado.

Algumas técnicas podem ser utilizadas para melhorar respostas do modelo. São elas:
* Few Shot Prompt
* COT (Cadeira de pensamentos)
* ReAct

E muitas outras

## Explorando Prompt Engineering no Amazon Bedrock

Abra o seu console AWS e direcione para o Amazon Bedrock. Nele, entre no playground e selecione a opção de chat.

## Zero Shot prompt
Não passamos nenhum exemplo para que o modelo consiga entender como responder (formato, tom, informações).

Coloque no na entrada o seguinte prompt:

> Por favor forneça um resumo financeiro da Apple Inc.

A resposta do modelo não foi muito legal, certo? E se adicionarmos um pouco de contexto? Adicione o seguinte prompt:

> Aqui está um contexto: Apple Inc. é uma grande empresa de tecnologia que produz eletrônicos para consumidores finais como iPhone, iPad, computadores Mac. Por favor, forneça um resumo da Apple Inc.

Ainda assim, vemos que ao comparar com análises reais e escritas por humanos, não temos uma saída interessante. Podemos então dar exemplos ao modelo de como uma saída adequada pode ser redigida. Isso é o que definimos como few shot prompt.


## Few Shot prompt

Agora iremos passar alguns exemplos para o modelo para que ele possa entender as nuances da tarefa solicitada. Coloque no playground o seguinte prompt:

> Forneça um breve sumário financeiro para as seguintes empresas: 
>
>  Microsoft: Microsoft relatou uma renda bruta recorde de $51.9 bilhões em seu ultimo relatório de quartil, um aumento de 20% ano sobre ano. Sua renda líquida de $16.7 bilhões, aumentando 21% comparado com o ano anterior. O crescimento da receita da Microsoft foi derivado de sua área de negócio Azure e ferramentas de produtividade Office 365.
>
>  Amazon: Em seu resultado mais recente, a Amazon relatou vendas de $96.1 bilhões, um auemnto de 15% comparado ao mesmo período do ano passado. A renda líquida da Amazon diminuiu para $2.9 bilhões, reduzindo 58% ano a ano, conforme a empresa sofre aumento de custos devido a inflração e problemas de cadeia de suprimentos. A Amazon Web Services, seu segmento de computação de nuvem, continuou a ter crescimento robusto com venda aumentou 33%.
>
>  Agora forneça um sumário financeiro da Apple Inc. baseado no seguintes fatos:
 > - Renda bruta dos últimos 12 meses: $260 bilhões
 > - Renda líquida: $55 bilhões
 > - Total de ativos: $321 bilhões
 > - Valor de mercado: $2.2 trilhões
  
Vemos que os resultados já ficaram melhores certo? 

Vamos ver isso explorando quando queremos que nosso modelo responda em um formato específico, digamos em JSON. 

Caso não sejamos específicos ao modelo, ele provavelmente não trará os resultados esperados. Coloque o prompt abaixo no playground:

> Me chamo Larissa Ferreira, sou natural de Salvador, Bahia. Atualmente, resido em Brasília, onde atuo como advogada em um conceituado escritório de advocacia. Minha formação acadêmica foi realizada na Universidade Federal da Bahia (UFBA), onde obtive o grau de Bacharel em Direito. Após me formar, decidi sair de minha cidade natal em busca de novas oportunidades profissionais na capital federal.
>
>Identifique no texto acima, nome, cidade atual, cidade natal, universidade, curso e trabalho

Nada de uma saída em formato JSON, correto? E se ensinarmos ao modelo sobre como ele pode capturar essas informações e gerar esse output com alguns exemplos? Use o seguinte prompt com few shot prompt para conferir os resultados:
>Meu nome é Rafaela Santos. Atualmente, resido na cidade de São Paulo, onde trabalho como gerente de marketing em uma empresa de tecnologia. Nasci em Belo Horizonte, Minas Gerais, e me formei em Administração de Empresas pela Universidade Federal de Minas Gerais (UFMG). Após concluir meus estudos, mudei-me para a capital paulista em busca de novas oportunidades profissionais. 
>
>Saida: 
>{ "nome": "Rafaela Santos", "cidade_atual": "São Paulo", "cidade_natal": "Belo Horizonte", "universidade": "Universidade Federal de Minas Gerais (UFMG)", "curso": "Administração de Empresas", "trabalho": "gerente de marketing em uma empresa de tecnologia" }
>
>Sou Pedro Oliveira, natural de Porto Alegre, Rio Grande do Sul. Atualmente, moro em Curitiba, onde trabalho como engenheiro civil em uma construtora de renome. Minha formação acadêmica foi realizada na Universidade Federal do Rio Grande do Sul (UFRGS), onde obtive o título de Bacharel em Engenharia Civil. Após concluir a graduação, decidi mudar de ares e buscar novos desafios profissionais na capital paranaense.
>
>Saida: 
{ "nome": "Pedro Oliveira", "cidade_atual": "Curitiba", "cidade_natal": "Porto Alegre", "universidade": "Universidade Federal do Rio Grande do Sul (UFRGS)", "curso": "Engenharia Civil", "trabalho": "engenheiro civil em uma construtora de renome" }
>
>Me chamo Larissa Ferreira, sou natural de Salvador, Bahia. Atualmente, resido em Brasília, onde atuo como advogada em um conceituado escritório de advocacia. Minha formação acadêmica foi realizada na Universidade Federal da Bahia (UFBA), onde obtive o grau de Bacharel em Direito. Após me formar, decidi sair de minha cidade natal em busca de novas oportunidades profissionais na capital federal.
>
>Qual seria a saída:

Vemos então que o modelo já consegue trazer os resultados mais próximos do que imaginavamos, o que pode nos possibilitar, por exemplo, de garantir uma maior reprodutibilidade e confiabilidade na saída deste, podendo ser usado em algumas aplicações.

## COT (Cadeia de Pensamentos) 
Large Language Models ainda não capazes totalmente de reasoning, isto é, entender empiricamente a significância de operações lógicas igual seres humanos. O que temos em seus outputs são tokens de maior probabilidade de acordo com o contexto de entrada. Dessa forma, se perguntamos algo mais complexo do ponto de vista lógico, é bem provável que o modelo possa vir a trazer uma resposta incorreta caso não o ajudemos.

Dessa forma, encadear pensamentos, isto é, ensinar o modelo a pensar em pequenas etapas pode melhorar a capacidade de resolução de problemas simples e permitindo que ele execute tarefas um pouco mais complexas com uma maior taxa de acerto. Vamos fazer um teste:

Para a seguinte pergunta, qual seria sua resposta?

> João tem 5 pêras, come 2 e compra mais 5, depois dá 3 ao seu amigo, compra 2 sacos com 5 cada um, quantas peras ele tem agora? Responda sucintamente.

15, concorda?  Em uma expressão numérica simples: (5-2+5-3 + 2*5) = 15

Agora, coloque essa entrada no modelo e veja a resposta:

> João tem 5 pêras, come 2 e compra mais 5, depois dá 3 ao seu amigo, compra 2 sacos com 5 cada um, quantas peras ele tem agora? Responda sucintamente em uma linha.

Acredito que tenha respondido errado... 
Como vimos, ele não "raciocinou" para chegar a resposta, dessa forma, podemos pedir para que ele pense em etapas (como um ser humano em tendência faria) para conseguir reduzir a tendência de erro.

>João tem 5 pêras, come 2 e compra mais 5, depois dá 3 ao seu amigo, compra 2 sacos com 5 cada um, quantas peras ele tem agora? Responda pensando etapa por etapa explicando sua linha de raciocínio em cada etapa.

Agora vemos que ele conseguiu chegar com maior confiabilidade a resposta correta, visto que dividiu em pequenas etapas. Isso mostra que mesmo para contextos mais complexos, um bom prompt pode ajudar a resolver.

## Passando contexto para o modelo

Um dos grandes limitadores de um LLM é sua janela temporal de treinamento. Isto é, além de não conseguir se interar de contextos atuais, como jogos Olímpicos 2024, também pode responder informações desatualizadas devido a atualização destas desde que o modelo foi inteiramente treinado.

Assim, passar contexto para o modelo durante o prompt pode ser uma maneira interessante de garantir confiabilidade em sua saída.

Vejamos:

#### Sem contexto
> O que você sabe sobre o Projeto Snerdgrass?

#### Com contexto
> Use o seguinte contexto:
> "O Projeto Snerdgrass é uma instalação residencial de tubos de vácuo para descarte de lixo. Custa $200 por mês e pode ser usado para compostagem, reciclagem e lixo. "
> que você sabe sobre o Projeto Snerdgrass?

Vemos que com uma simples "injeção" no prompt, permitimos que ele possa obter contexto em "real-time" o que nos permite tentar mante-lo atualizado e até mesmo "customiza-lo" com nossos dados. 

Mais um exemplo:

> Qual foi a ultima medalha de Rayssa Leal nas olimpiadas?

Sabemos que é errado...

Adicionando contexto:
> Use o seguinte contexto:
> "Rayssa Leal foi medalha de Bronze nas Olimpiadas de Paris 2024 na modalidade de Skateboard feminino "
> Qual foi a ultima medalha de Rayssa Leal nas olimpiadas?

Isso é a base do que definimos como RAG, Retrieval Augmented Generation, na qual temos dinamicamente contextos atualizados (documentos, PDFs, arquivos, JSONs) que são passados ao modelo em tempo de inferência, o que permite que ele possa ter quase sempre respostas adequadas e atualizadas.


<div align=center>
  
![image](https://github.com/user-attachments/assets/b3d91c62-7282-40a2-bd83-8d1b78a5da45)

</div>

## Interagindo com modelos multimodais

No Amazon Bedrock, muito mais do que apenas conversar com modelos, podemos também realizar tarefas de interações com nossos arquivos, imagens e muito mais, podendo retirar ainda mais insights.

Vamos fingir a seguinte situação: Estamos criando uma aplicação que nos ajudará a identificar se funcionários estão vestindo todos os EPIs necessãrios (capacete, oculos e luvas de proteção), e ainda listar aqueles que ele está vestindo atualmente. 
Dessa forma, vamos baixar as 3 imagens a seguir:

[Imagem 1](https://blog.mills.com.br/wp-content/uploads/2022/03/02-epi-para-trabalho-altura2.png)

[Imagem 2](https://www.pontotel.com.br/local/wp-content/uploads/2024/05/epi-para-que-servem-os-epis-de-seguranca-1024x529.webp)

[Imagem 3](https://medilogics.pt/home/wp-content/uploads/2022/12/pexels-photo-8961155-1880x1200.jpeg)

Assim, faça o input da imagem para o modelo Claude 3 Sonnet, e adicione o seguinte prompt:

>Voce é um auxiliar de verificacao de EPIs em um centro industrial.
>Identifique se funcionários estão vestindo todos os EPIs necessarios no caso: capacete, oculos e luvas de proteção
>Liste os faltantes caso necessario. Olhe com atencao a todos os detalhes.

Vemos que rapidamente podemos construir uma aplicação simples que analisa imagens seguindo comando de texto.

#### Realizando OCR com imagens
Podemos também usar esses modelos para transcrição de texto em imagens, detecção de entidades e muito mais.
Suponha que queremos uma forma de obter texto de notas fiscais que são digitalizadas por funcionários.

Faça download da imagem a seguir:
[Imagem 4](https://static.cobrefacil.com.br/assets/base/20c/9f5/700/modelo-cupom-fiscal-tradicional.png)

E novamente para o Claude 3 Sonnet faça o input da iamgem acompanhado pelo prompt:
> Transcreva o texto desta imagem de maneira clara e organizada.

Vemos que em poucos segundos o modelo consegue gerar os resultados de transcrição de maneira direta e clara.

## Conversando com seus documentos

Podemos também retirar insights de documentos (PDFs, docx), chegando perto do que definimos como RAG. 
Assim, vamos experimentar a funcionalidade de "Chat with your Documents" do Bedrock, onde iremos ver a capacidade do modelo de interagir com uma Shareholder de 2022 da Amazon, e podemos assim para entender aspectos chaves sem ter que ler o documento de 10 páginas.

Realize o download do PDF aqui:

[Documento](https://s2.q4cdn.com/299287126/files/doc_financials/2023/ar/2022-Shareholder-Letter.pdf)

Realize o upload. 
Podemos então perguntar ao modelo, assuntos relacionados ao texto, e vemos que este além de responder, nos oferece referências diretas de sua resposta.
Alguns prompts:

> Quais sao os aspectos chaves destacados aqui?


>O que a Amazon tem realizado no campo de IA Generativa?


>O que é o projeto Kuiper?

> Resuma o documento para mim de maneira objetiva e concisa.

## Gerando imagens com modelos de difusão

No Bedrock também é possível explorar outro branch de modelos fundacionais, os modelos de difusão. 
Eles permitem que possamos gerar imagens, realizar pequenas edições, correções de maneira prática e efetiva.

Aqui, deixamos a criatividade aflorar. Por exemplo, podemos pedir:

> Imagine um Bulldog correndo na praia de Copacobana.

E receber como resposta:

![image](https://github.com/user-attachments/assets/cc446989-db49-4848-9f49-8bfa4e418749)

#### Referências
https://github.com/aws-samples/amazon-bedrock-workshop/tree/main/01_Text_generation
https://catalog.us-east-1.prod.workshops.aws/workshops/4c28c535-249d-44dc-939b-9f0942078336/en-US/05-prerequisites/02-self-paced
https://aws.amazon.com/pt/bedrock/
