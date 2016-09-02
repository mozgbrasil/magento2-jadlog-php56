![valid XHTML][checkmark]
[checkmark]: https://raw.githubusercontent.com/mozgbrasil/mozgbrasil.github.io/master/assets/images/logos/Red_star_32_32.png "MOZG"
[url-method]: http://www.jadlog.com.br/
[requirements]: http://mozgbrasil.github.io/requirements/
[contact-jadlog]: http://www.jadlog.com.br/faleconosco.html
[tickets]: https://cerebrum.freshdesk.com/support/tickets/new
[preco]: http://www.cerebrum.com.br/preco/
[github-boxpacker]: https://github.com/mozgbrasil/magento-boxpacker-php56#mozgboxpacker
[getcomposer]: https://getcomposer.org/
[uninstall-mods]: http://devdocs.magento.com/guides/v2.1/install-gde/install/cli/install-cli-uninstall-mods.html

# Mozg\Jadlog

## Sinopse

Integração a [Jadlog][url-method]

## Motivação

Atender o mercado de módulos para Magento oferecendo melhorias e um excelente suporte

## Suporte / Dúvidas

Para obter o devido suporte [Clique aqui][tickets], relatando o motivo da ocorrência o mais detalhado possível e anexe o print da tela para nosso entendimento

## Preço

[Clique aqui][preco]

## Recursos

- Definir dimensões para os produtos

- Definir dimensões, peso e valor da Embalagem/Caixa

- Opção para embalar os produtos separadamente ou combinar na mesma Embalagem/Caixa

- Embalagem do produto inteligente, exibe como os produtos serão agrupados e calcula o peso dimensional fazendo o envio fracionado se necessário

- Armazenamento das requisições em Cache

~~- Definir como diferentes combinações de produtos são embalados em conjunto # TODO~~

~~- Atribuir produtos a determinadas caixas (produtos múltiplos podem ser atribuídos à mesma caixa) # TODO~~

## Característica técnica

Atualmente diversos módulos de terceiros relativo a métodos de entrega sempre soma o peso e dimensões dos produtos gerando falha na requisição a transportadora devido não terem um sistema que separa os produtos em sua devida embalagem distribuindo seu peso.

O nosso módulo foi desenvolvido visando total transparência dos processos executados, para efeito de análise visualize os processos armazenado em log.

A extensão permite você definir as dimensões de seus produtos, as dimensões de suas embalagens e regras de como empacotar diferentes combinações de produtos em conjunto.

A extensão escolhe qual embalagem será utilizado para embalar os produtos para o pedido.

A extensão pode distribuir os produtos em diversas embalagens até o peso máximo suportado para a embalagem.

Como será cadastrado a embalagem com as dimensões e peso suportado pelas transportadoras não deve ocorrer falha relativa as dimensões ou peso.

A primeira coisa a se levar em consideração no uso do módulo é o [Gerenciamento de Caixa/Embalagem][github-boxpacker], como já vem alguns registros pré inseridos certifique se de atualizar os registros conforme sua necessidade.

Certifique se ter cadastrado as devidas dimensões para os produtos.

Para cada pacote é feito um acesso ao WebService onde é passado os devidos parâmetros

O módulo possui armazenamento de cache

Na finalização do pedido é armazenado no histórico do pedido um comentário contendo um identificador único que poderá ser usado para consulta no arquivo de log a discriminação dos pacotes seus itens e a visualização de cada pacote com seus itens em 3D

Sempre confira as informações de frete antes de processar cada pedido, caso algo esteja inconsistente será necessário cancelar o pedido até a correção da ocorrência

Para o rastreamento do pacote é feito acesso ao WebService onde é passado os devidos parâmetros e exibido o devido retorno

## Instalação - Atualização - Desinstalação

Este módulo destina-se a ser instalado usando o [Composer][getcomposer]

Antes de executar os processos, [clique aqui][requirements] e leia os pré-requisitos e sugestões

--

### Para instalar o módulo execute o comando a seguir no terminal do seu servidor

	composer require mozgbrasil/magento2-jadlog-php56 && php bin/magento setup:upgrade

Você pode verificar se o módulo está instalado, indo ao backend em:

	STORES -> Configuration -> ADVANCED/Advanced -> Disable Modules Output

--

### Para atualizar o módulo execute o comando a seguir no terminal do seu servidor

	composer update && php bin/magento setup:upgrade

--

### Para [desinstalar][uninstall-mods] o módulo execute o comando a seguir no terminal do seu servidor

	bin/magento module:uninstall --remove-data --backup-code --backup-media --backup-db Mozg_Jadlog

~~composer remove mozgbrasil/magento2-jadlog-php56 && composer clear-cache && composer update && php bin/magento setup:upgrade~~

## Como configurar o método de entrega

Antes de configurar o módulo você deve cadastrar o CEP de origem, indo ao backend em:

	STORES -> Configuration -> Sales/Shipping Settings -> Origin

Para configurar o método de entrega, acesse no backend em:

	STORES -> Configuration -> Sales/Shipping Methods -> Jadlog (powered by MOZG)

Você terá os campos a seguir

### • **Ativar**

Para "ativar" ou "desativar" o uso do método

### • **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

### • **Título**

Nome do método que deve ser exibido

### • **Serviços**

Selecione os serviços desejado, para selecionar mais de um, segure a tecla "Ctrl" e clique nos serviços

### • **Serviço Para Entrega Gratuita**

Quando houver um desconto de frete grátis, esse serviço terá o valor zero

### • **Calcular taxa de manuseio**

Podendo ser fixo ou percentual

### • **Taxa de Manuseio**

Será adicionado o valor ao frete

### • **Mostrar método se não aplicável**

Quando configurado como "Não", caso seja retornado algum serviço com erro, não será exibido o método de entrega

### • **Debug**

Deve ser armazenado os processos do módulo em var/log/

O arquivo 

DATE_mozg.log

se trata de log do módulo sendo um log mais detalhado contendo todos os processos inclusive das execuções realizadas pelas bibliotecas externas do módulo

O arquivo

shipping_METHOD.log

se trata de log nativo do magento relativo ao método de entrega

### • **Enviar para países aplicáveis**

Você pode definir se o método deve funcionar para "Todos os Países aceito" ou "Especificar Países "

### • **Enviar para países específicos**

Você deve selecionar os países que o método deve ser funcional

### • **Remetente**

Preencha nesse campo o Remetente vinculado ao contrato com a Jadlog

### • **CNPJ do cliente que será responsável pelo pagamento**

Preencha nesse campo o número do CNPJ vinculado ao contrato com a Jadlog

### • **Inscrição Estadual**

Preencha nesse campo o número da Inscrição Estadual vinculado ao contrato com a Jadlog

### • **CEP**

Preencha nesse campo o número do CEP vinculado ao contrato com a Jadlog

### • **Endereço**

Informe o seu Endereço

### • **Bairro**

Informe o seu Bairro

### • **Telefone**

Informe o seu Telefone

### • **Tipo de entrega**

Informe o seu Tipo de entrega

### • **Tipo de Seguro**

Informe o seu Tipo do Seguro

### • **Frete a pagar no destino**

Informe o modelo de pagamento do frete

### • **Valor da coleta**

Informe o Valor da coleta

### • **Código do Cliente**

Informe o Código do Cliente

### • **Senha**

Informe a Senha

### • **Mostrar serviço com retorno de erro**

Quando configurado como "Não", caso seja retornado algum serviço com erro, o mesmo não deve ser exibido no método de entrega

## Quais os recursos do módulo

- [✓] Cálculo do frete
- [✓] Rastreamento

## Perguntas mais frequentes "FAQ"

### Como conferir os valores dos fretes junto a transportada

Você pode visualizar no log os parâmetros enviado a transportada

Quando finalizado o pedido é armazenado no historico as dimensões da caixa que foi usada para o obter o frete

### Como aplicar o Frete Grátis

Na configuração do módulo para o método de entrega é possível definir o "Serviço Para Entrega Gratuita" recurso que deve ser aplicado quando definido a ação de "Frete Grátis" nas "Regras da Promoção"

No Backend do Magento, acesse o menu: Promoções -> Regras de Promoção -> Criar regra -> Crie uma regra e defina na aba "Ações" o uso do Frete Grátis

Dessa forma na exibição do cálculo do frete será exibido para o serviço escolhido o valor zerado

Esse recurso se trata de regra nativa do Magento caso tenha algum problema sugiro desativar todas as regras de promoção e ativar uma de cada vez até encontrar o motivo da ocorrência

### Serviço Para Entrega Gratuita pré-selecionado como EXPRESSO

O "Serviço Para Entrega Gratuita" só deve funcionar quando definido na regra de promoção o frete grátis

Sobre o "Serviço Para Entrega Gratuita" já estar pré-selecionado como "EXPRESSO" isso está ocorrendo pois esse serviço tem o seu identificador sendo zero, e o identificador nativo do Magento para "Nenhuma das opções" também é zero ou vazio

Devido a está ocorrência não está sendo possível aplicar o "Serviço Para Entrega Gratuita" para o Serviço "EXPRESSO"

### Sobre o retorno de erro "Could not connect to host"

Se trata de bloqueio imposto no seu servidor de hospedagem para acesso a Jadlog

No Firewall crie uma condição liberando as portas no servidor "80" e "8080" e adicione na WHITE LIST o ip 187.93.97.51 da jadlog

### Dados de contato - Jadlog

Para que sejam encaminhadas as solicitações ao webservice da JADLOG.  
O cliente deverá efetuar o seu cadastro com o Departamento Comercial.  
Telefone: (11) 3563-2000  
Contatos: Vera Ramos / Debora / Simone / Flavia / João Pedro

Comercial - JadLog <comercial@jadlog.com.br>

Suporte - JadLog <helpdesk@jadlog.com.br>

Programador - Ricardo Fernandes <ricardo.fernandes@jadlog.com.br> (11) 3563-2000 ramal 2067

ou acesse

Para entrar em contato com a [Jadlog][contact-jadlog]

## Manual

http://www.youblisher.com/p/641712-Manual-de-integracao-JADLOG/

## Contribuintes

Equipe Mozg

## License

[Comercial License] (LICENSE.txt)

## Badges

[![Join the chat at https://gitter.im/mozgbrasil](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/mozgbrasil/)
[![Latest Stable Version](https://poser.pugx.org/mozgbrasil/magento2-jadlog-php56/v/stable)](https://packagist.org/packages/mozgbrasil/magento2-jadlog-php56)
[![Total Downloads](https://poser.pugx.org/mozgbrasil/magento2-jadlog-php56/downloads)](https://packagist.org/packages/mozgbrasil/magento2-jadlog-php56)
[![Latest Unstable Version](https://poser.pugx.org/mozgbrasil/magento2-jadlog-php56/v/unstable)](https://packagist.org/packages/mozgbrasil/magento2-jadlog-php56)
[![License](https://poser.pugx.org/mozgbrasil/magento2-jadlog-php56/license)](https://packagist.org/packages/mozgbrasil/magento2-jadlog-php56)
[![Monthly Downloads](https://poser.pugx.org/mozgbrasil/magento2-jadlog-php56/d/monthly)](https://packagist.org/packages/mozgbrasil/magento2-jadlog-php56)
[![Daily Downloads](https://poser.pugx.org/mozgbrasil/magento2-jadlog-php56/d/daily)](https://packagist.org/packages/mozgbrasil/magento2-jadlog-php56)

:cat2:
