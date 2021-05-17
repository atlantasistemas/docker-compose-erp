# docker-compose-erp

Contêm arquivos de configuração do servidor para colocar a aplicação SaaS funcionando

## Colocar para funcionar a API

1. Primeiro passo é instalar o docker e o docker-compose no servidor através desses links https://docs.docker.com/engine/install/ https://docs.docker.com/compose/install/
2. Criar a pasta `/opt/atlanta/` e dentro dela baixar os dois arquivos desse repositório
3. Configurar as variáveis do arquivo .env, veja no tópico Comandos Úteis como editar um arquivo no linux
	- As variáveis que começar com `SERVER_DB_` contêm as configurações do banco de dados que a API vai usar para comunicar
	- `FRONTEND_VERSION` e `API_VERSION` são as variáveis que define a versão do front-end e do back-end respectivamente
	- `FRONTEND_PORTA_EXTERNA` e `API_PORTA_EXTERNA` é a porta que vai que vai ser exposta, a porta que for configurado em `FRONTEND_PORTA_EXTERNA` é a porta que o usuário vai acessar a aplicação
	- `API_TOKEN` é a variável que contêm o token de identificação do front-end ele precisa ser o mesmo do registro de código 1 da tabela `api` do banco de dados, `SELECT * FROM api WHERE codigo = 1`, observar que se for a primeira vez que configura a API nesse banco de dados gerar um token aleatório com a mesma quantidade de caracteres e subistituir no registro de código 1 da tabela de API
4. Após tudo configurado rodar o comando `docker-compose up`, a API já vai estar funcionando
5. As versões das APIs e FRONT-END pode ser encontradas em https://hub.docker.com/r/atlantasistemas/atlapi/tags e https://hub.docker.com/r/atlantasistemas/atlfrontend/tags

## Atualizar uma API

1. Editar o arquivo `/opt/atlanta/.env` e alterar as variáveis `FRONTEND_VERSION` e `API_VERSION` para a versão desejada
2. Dentro da pasta execute o comando `docker-compose up` e será baixado a nova versão e colocado para funcionar

## Comandos úteis

- `nano NomeArquivo`: abre um arquivo para edição, observe os atalhos por baixo, o comando `Ctrl + X` para fechar o arquivo por exemplo
- `ls -a`: lista todos os arquivos da pasta atual inclusive os ocultos
- `docker-compose up`: inicia a API e o front-end, tem de ser executado dentro da pasta onde estão os arquivos de configuração
- `docker-compose down`: para a API e o front-end, tem de ser executado dentro da pasta onde estão os arquivos de configuração
- `docker container ls`: lista os containers que estão em execução, usado para ver se a API está funcionando