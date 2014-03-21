# Aula 3 | Infraestrutura de aplicaÃ§Ãµes web

## Requisitos de infraestrutura para aplicaÃ§Ãµes web


### Perfil do Site

- Identifique qual o perfil do seu site 
 - Portal de NotÃ­cias, Comercio EletrÃ´nico, Redes Sociais, Clubes de Descontos, etc... 
- Estimativa de acesso por dia 
 - 10, 100, 1.000, 100.000 acessos por dia 
- Tempo da sessÃ£o ativa, quanto tempo o usuÃ¡rio permanece autenticado com os dados armazenados no servidor 
- Quantidade de impressÃµes de pÃ¡ginas, quantas vezes um pÃ¡gina foi impressa na tela 


### Picos de Acessos 

- Identifique se o site pode ter picos de acesso 
 - Portais de NotÃ­cias 
  - NotÃ­cias relacionados a eventos importantes trazem grande volume de acesso aos sites 
- Comercio EletrÃ´nico 
 - PromoÃ§Ãµes como â€œblackfridayâ€ ou liquidaÃ§Ãµes 
- Venda de Ingressos para grandes Shows 


### EspaÃ§o em Disco e TransferÃªncia de dados

- Identifique o volume de registros ou conteÃºdos gerados pelo site 
 - Redes Sociais tem grandes volumes de registros e espaÃ§o em disco para imagens 
 - Hoje o Facebook Ã© o maior repositÃ³rio de imagens2
- Analise o tamanho de pÃ¡ginas do site 
 - Cada requisiÃ§Ã£o de uma pÃ¡gina consome em â€œbytesâ€ tamanho da pÃ¡gina acessada 
 - Upload e Downlod consomem â€œbytesâ€ de transferencia de pÃ¡gina


## Infraestrutura bÃ¡sica

- Windows Server com os seguintes softwares instalados: 
 - Servidor web responsÃ¡vel por delegar o processamento de pÃ¡ginas dinamicas para o servidor de aplicaÃ§Ã£o e pela entrega de conteÃºdos estÃ¡ticos, como imagens, css, javascript e etc. 
 - Servidor de aplicaÃ§Ã£o responsÃ¡vel pelo processamento dos conteÃºdos dinamicos 
 - Software de banco de dados responsÃ¡vel pelo armazenamento dos dados dos usuÃ¡rios ou da aplicaÃ§Ã£o
- Em um ambiente produtivo existem outros equipamentos antes de chegar ao servidor: 
 - Roteadores, Switch, Firewall, Balanceadores, etc.. 
- Link de acesso a Internet 
- O servidor deve estar disponÃ­vel na Internet 
- Cada acesso ao servidor corresponde a transferÃªncias de dados (â€œbytesâ€). 
- Cada acesso a um recurso, consome-se um volume de bytes, desta forma o link de acesso a internet Ã© um ponto de limite de estrutura ou custo


## Balanceamento do â€œlinkâ€ de acesso a internet

- O roteador pode estar ligado a um ou mais â€œlinksâ€ de internet 
- Cada â€œlinkâ€ pode ser adiquirido de provedores diferentes 
- Caso ocorra algum problema em um dos â€œlinksâ€, o outro assume todo o trÃ¡fego 
- Caso tenha um pico de acesso o trafego Ã© divido 
- Pode-se utilizar somente um dos â€œlinksâ€ e utilizar o outro somente quando houver necessidade 
 - Neste caso pode gerar uma economia se o pagamento estÃ¡ viculado a bytes transferidos 


## Servidor de banco de dados

- Ao decidir ter um outro servidor para banco de dados: 
 - Ocorre uma liberaÃ§Ã£o de processamento do servidor principal 
 - Os dados dos clientes ficam mais seguros pois nÃ£o estÃ£o espostos diretamente na internet 
 - Somente o servidor principal tem acesso ao servidor de banco de dados em uma porta especÃ­fica 
 - No caso de necessidade de mais processamento ou maior disponibilidade do serviÃ§o de dados sÃ£o disponibilizados dois ou mais servidores de banco de dados e cofigurados para trabalhar como cluster
 
 
 ## Servidores de aplicaÃ§Ãµes web
 
- Os servidores de aplicaÃ§Ãµes web podem ser configurados para trabalhar em Cluster: 
 - Cluster Ã© um conjunto de instancia de servidores de aplicaÃ§Ãµes configurados para agir em conjunto, de forma a oferecer maior escalabilidade e disponibilidade de uma Ãºnica instancia. 
 - Compartilham os mesmos recursos 
 - O usuÃ¡rio acessa diversos servidores durantea sua sessÃ£o 
 
'''
Caso uma das mÃ¡quinas do cluster caia, o usuÃ¡rio continua com acesso a aplicaÃ§Ã£o. 
'''

JKmound (jboss)

- Ou em *Paralelo*: 
 - NÃ£o estÃ£o configurados para agir em conjunto. 
 - SÃ£o idependentes um dos outros. 
 - Cria um isolamento entre os ambientes. 
 - O usuÃ¡rio somente acessa um Ãºnico servidor de aplicaÃ§Ã£o durante a sua sessÃ£o.

'''
Neste caso quando uma das mÃ¡quinas do cluster cair, os usuÃ¡rio conectados tambÃ©m caem. 
'''

## Servidores web

- SÃ£o responsÃ¡veis em delegar as pÃ¡ginas dinÃ¢micas para os servidores de aplicaÃ§Ãµes e entregar os conteÃºdos estÃ¡ticos. 
- Quando duplicamos os servidores de aplicaÃ§Ãµes estamos aumentando a garantia da disponibilidade. 
- E aumenta a capacidade de resposta dos recursos acessados pelos usuÃ¡rios.

## ValidaÃ§Ã£o da infraestrutura

- A validaÃ§Ã£o da infraestrutura Ã© uma peÃ§a importante para conhecer o limite de sua estrutura 
- Outro ponto Ã© identificar se os pontos de redundÃ¢ncia estÃ£o funcionando adequadamente 
- E se as configuraÃ§Ãµes dos equipamentos estÃ£o corretas 
- Essa validaÃ§Ã£o pode ser feita atravÃ©s de empresas especializadas em testes de carga 
 - http://www.compuware.com/en_us/application-performance-management.html
 - http://www.neotys.com/product/overview-neoload.html


#### Outra forma de fazer testes especÃ­ficos Ã© utilizar 
ferramentas locais 

##### Apache AB 
 Ferramenta especializada para exibir o nÃºmero de requisiÃ§Ã£o por segundo da sua infra estrutura 

##### jMeter 
Ferramenta especializada em testes de performance de recursos estÃ¡ticos e dinÃ¢micos 

## Mecanismo de cache
