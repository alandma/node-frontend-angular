# Node Angular + Nginx

Criação de containers em docker para utilizar em projetos `node` em `javascript` e `typescript`.

## Criando/Adicionando o projeto
Adicione seu projeto na raiz desse repositorio ficando com os "**Dockerfiles**", algo assim;

```
node-frontend-angular
├── angular.json
├── browserslist
├── .env
├── configs
├── docker-compose.yml
├── Dockerfile.dev
├── Dockerfile.prd
├── e2e
├── karma.conf.js
├── package.json
├── README.md
├── src
├── tsconfig.app.json
├── tsconfig.json
├── tsconfig.spec.json
├── tslint.json
└── yarn.lock
```
## Alterações e variaveis
As variaveis da app ficam na pasta `.env` e há duas criadas como exemplo, mas pode ser alteradas conforme desejado.

Na pasta `configs` fica o arquivo de _configuração do nginx_ (**nginx.conf**), que irá processar o frontend compilado, no caso de produção, se quiser efetuar alguma alteração no container nginx processado no `Dockerfile.prd` é aqui que se deve alterar.

Outro arquivo que contem variaveis que dever ser alteradas de acordo com o projeto é o `docker-compose.yml`, segue elas;

* **BUILD_ENV**: Aqui ficará o paramentro de "estado" do projeto, conforme definido na hora de efetuar o _build_ da app (prod, dev ou staging).
* **NODE_TAG**: Definirá a versão do _node_ que será utilizado, criando a _imagem docker_ para a subir o _container_.
  >Para verificar todas as versões disponiveis (`TAGs`), consultar [Tags Node](https://hub.docker.com/_/node/?tab=tags) no dockerhub oficial.
* **NGINX_TAG**: Mesmo conceito anterior, Definirá a versão do _nginx_ que irá criar a _imagem docker_ para a crianção no _container_.
  >Para verificar todas as versões disponiveis (`TAGs`), consultar [Tags NGINX](https://hub.docker.com/_/nginx/?tab=tags) no dockerhub oficial.

Mais informações sobre adicionar as variaveis no _Compose_ que alteram os `Dockerfiles` consultar o parametro [args](https://docs.docker.com/compose/compose-file/compose-file-v3/#args) na documentação.

## Executando o projeto
Com tudo definido vamos executar o projeto.

No `docker-compose.yml` temos duas possibilidades de execução, `desenvolvimento` (**frontend-angular-dev**) e para efetuar o _build_ de `produção` (**frontend-angular**).

### Executar o ambiente de "**dev**";
```console
docker-compose up frontend-angular-dev
```
dessa forma a saida ficará "travada" no terminal, para observação dos logs.

### Compilando (_build_) o projeto para "**produção**";
```console
docker-compose up --build -d frontend-angular
```
>O `Dockerfile.prd` foi criado com [multi-stage](https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds), primeiro ele irá fazer o _build_ do projeto, pegar o "**resultado**" e copiar para o "**estagio**" dois que é a criação do container do _nginx_.

#### Referencias:

- https://docs.docker.com/compose/compose-file/compose-file-v3/
- https://hub.docker.com/_/node/
- https://hub.docker.com/_/nginx/
- https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds