# Aula 3 | Infraestrutura de aplicações web

## Requisitos de infraestrutura para aplicações web


### Perfil do Site

- Identifique qual o perfil do seu site 
 - Portal de Notícias, Comercio Eletrônico, Redes Sociais, Clubes de Descontos, etc... 
- Estimativa de acesso por dia 
 - 10, 100, 1.000, 100.000 acessos por dia 
- Tempo da sessão ativa, quanto tempo o usuário permanece autenticado com os dados armazenados no servidor 
- Quantidade de impressões de páginas, quantas vezes um página foi impressa na tela 


### Picos de Acessos 

- Identifique se o site pode ter picos de acesso 
 - Portais de Notícias 
  - Notícias relacionados a eventos importantes trazem grande volume de acesso aos sites 
- Comercio Eletrônico 
 - Promoções como "blackfriday" ou liquidações 
- Venda de Ingressos para grandes Shows 


### Espaço em Disco e Transferência de dados

- Identifique o volume de registros ou conteúdos gerados pelo site 
 - Redes Sociais tem grandes volumes de registros e espaço em disco para imagens 
 - Hoje o Facebook é o maior repositório de imagens2
- Analise o tamanho de páginas do site 
 - Cada requisição de uma página consome em "bytes" tamanho da página acessada 
 - Upload e Downlod consomem "bytes" de transferencia de página


## Infraestrutura básica

- Windows Server com os seguintes softwares instalados: 
 - Servidor web responsável por delegar o processamento de páginas dinamicas para o servidor de aplicação e pela entrega de conteúdos estáticos, como imagens, css, javascript e etc. 
 - Servidor de aplicação responsável pelo processamento dos conteúdos dinamicos 
 - Software de banco de dados responsável pelo armazenamento dos dados dos usuários ou da aplicação
- Em um ambiente produtivo existem outros equipamentos antes de chegar ao servidor: 
 - Roteadores, Switch, Firewall, Balanceadores, etc.. 
- Link de acesso a Internet 
- O servidor deve estar disponível na Internet 
- Cada acesso ao servidor corresponde a transferências de dados ("bytes"). 
- Cada acesso a um recurso, consome-se um volume de bytes, desta forma o link de acesso a internet é um ponto de limite de estrutura ou custo


## Balanceamento do "link" de acesso a internet

- O roteador pode estar ligado a um ou mais "links" de internet 
- Cada "link" pode ser adiquirido de provedores diferentes 
- Caso ocorra algum problema em um dos "links", o outro assume todo o tráfego 
- Caso tenha um pico de acesso o trafego é divido 
- Pode-se utilizar somente um dos "links" e utilizar o outro somente quando houver necessidade 
 - Neste caso pode gerar uma economia se o pagamento está viculado a bytes transferidos 


## Servidor de banco de dados

- Ao decidir ter um outro servidor para banco de dados: 
 - Ocorre uma liberação de processamento do servidor principal 
 - Os dados dos clientes ficam mais seguros pois não estão espostos diretamente na internet 
 - Somente o servidor principal tem acesso ao servidor de banco de dados em uma porta específica 
 - No caso de necessidade de mais processamento ou maior disponibilidade do serviço de dados são disponibilizados dois ou mais servidores de banco de dados e cofigurados para trabalhar como cluster
 
 
 ## Servidores de aplicações web
 
- Os servidores de aplicações web podem ser configurados para trabalhar em Cluster: 
 - Cluster é um conjunto de instancia de servidores de aplicações configurados para agir em conjunto, de forma a oferecer maior escalabilidade e disponibilidade de uma única instancia. 
 - Compartilham os mesmos recursos 
 - O usuário acessa diversos servidores durantea sua sessão 
 
'''
Caso uma das máquinas do cluster caia, o usuário continua com acesso a aplicação. 
'''

JKmound (jboss)

- Ou em *Paralelo*: 
 - Não estão configurados para agir em conjunto. 
 - São idependentes um dos outros. 
 - Cria um isolamento entre os ambientes. 
 - O usuário somente acessa um único servidor de aplicação durante a sua sessão.

'''
Neste caso quando uma das máquinas do cluster cair, os usuário conectados também caem. 
'''

## Servidores web

- São responsáveis em delegar as páginas dinâmicas para os servidores de aplicações e entregar os conteúdos estáticos. 
- Quando duplicamos os servidores de aplicações estamos aumentando a garantia da disponibilidade. 
- E aumenta a capacidade de resposta dos recursos acessados pelos usuários.

## Validação da infraestrutura

- A validação da infraestrutura é uma peça importante para conhecer o limite de sua estrutura 
- Outro ponto é identificar se os pontos de redundância estão funcionando adequadamente 
- E se as configurações dos equipamentos estão corretas 
- Essa validação pode ser feita através de empresas especializadas em testes de carga 
 - http://www.compuware.com/en_us/application-performance-management.html
 - http://www.neotys.com/product/overview-neoload.html


#### Outra forma de fazer testes específicos é utilizar 
ferramentas locais 

##### Apache AB 
 Ferramenta especializada para exibir o número de requisição por segundo da sua infra estrutura 

##### jMeter 
Ferramenta especializada em testes de performance de recursos estáticos e dinâmicos 

## Mecanismo de cache
