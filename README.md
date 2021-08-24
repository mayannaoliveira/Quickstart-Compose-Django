
#  Tutorial de Django com Docker e Postgres
Tutorial realizado seguindo as oreetações encontradas no documentação do Docker na página [Quickstart: Compose and Django]. Esse projeto foi criado para estudo do [Django] juntamente com o [Docker] e o [Postgres].

**Observação:** *Sugiro o uso do [Visual Studio Code] com a extensão do [Docker pela Microsoft], pois é mais fácil de visualizar e entender o comportamento do Docker durante o projeto.*

#### Docker Hub
Exemplo de como criar um repositório e subir para o Docker Hub.
Comandos a serem utilizados:
```bash
# Efetuar login via terminal
docker login docker
# Baixar imagem:
docker pull [nome_usuário]/[nome_repositório]
# Exemplo de como criar uma imagem:
docker build -t [nome_usuário]/[nome_repositório] .
#  Exemplo de como enviar imagem para o Docker Hub
docker push [nome_usuário]/[nome_repositório]

```

### Resumo dos passos do tutorial
Caso queira colocar ou baixar a imagem no [Docker Hub] veja o exemplo abaixo:
```
# Efetuar login no Docker Hub
docker login docker
# Baixar imagem:
docker pull mayannaoliveira/projeto-django
# Exemplo de como criar uma imagem:
docker build -t mayannaoliveira/projeto-django .
#  Exemplo de como enviar imagem para o Docker Hub
docker push mayannaoliveira/projeto-django
```
**Observação:** *Lembre de trocar mayannaoliveira pelo nome de seu usuário.*
 

docker-compose run --rm app django-admin python3 manage.py startapp appexample

Criar projeto:
docker-compose run --rm app django-admin startproject projeto .

Construir:
docker-compose build

Rodar: 
docker-compose up --build
docker-compose up

### Passo-a-passo do tutorial:
1. Criar uma pasta para armazenar o projeto
```
cd quickstart-compose-django
```
2. Instalar o docker compose com o comando:
```
pip install docker-compose
``` 
3. Na raiz do projeto criar um arquivo chamado Dockerfile
```
FROM python:3
ENV PYTHONUNBUFFERED=1
WORKDIR /code
COPY requirements.txt /code/
RUN pip install -r requirements.txt
COPY . /code/
```
1. Na raiz do projeto criar um arquivo requirements.txt
```
Django>=3.0,<4.0
psycopg2-binary>=2.8
```
5. Rodar o comando: RUN pip install -r requirements.txt
6. Na raiz do projeto criar um arquivo docker-compose.yml
```
version: "3.9"
   
services:
  db:
    image: postgres
    volumes:
      - ./data/db:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - "8000:8000"
    depends_on:
      - db
```
7. Inicie um projeto com o comamndo:

```
sudo docker-compose run web django-admin startproject composeexample . 
```
8. Cheque a lista de arquivos do projeto com o comando:
```
ls -l
```
9.  Se você estiver executando o Docker no Linux, os arquivos criados pelo django-admin são de propriedade do root. Altere a propriedade dos novos arquivos com o comando: 
``` 
sudo chown -R $USER:$USER .
```
10. Acesse a pasta do projeto *composeexample* e edite o arquivo [settings.py](composeexample/settings.py) trocando os dados do banco de dados como mostra abaixo:
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
}
```
**Observação:** *Acesse o site do [Postgres] para verificar os passos de instalação do Banco de Dados. Recomendo o uso também da extenção para o [Visual Studio Code] chamada [SQL Tools] juntamente com o driver PostgreSQL.*

11. Rodar o projeto e verificar que está abrindo a página de localhost
```
docker-compose up
```
#### Tecnologias utilizadas:
![Docker](https://shields.io/badge/Docker-gray?logo=Docker&logoColor=blue&style=for-the-badge)
![Django](https://shields.io/badge/Django-gray?logo=Django&logoColor=green&style=for-the-badge)
![Python](https://shields.io/badge/Python-gray?logo=Python&logoColor=yellow&style=for-the-badge)
![Html5](https://shields.io/badge/HTML5-gray?logo=html5&logoColor=red&style=for-the-badge)
![Css3](https://shields.io/badge/css3-gray?logo=css3&logoColor=blue&style=for-the-badge)
![Css3](https://shields.io/badge/SQLITE-gray?logo=sqlite&logoColor=blue&style=for-the-badge)

#### Sugestões ou dúvidas essas são minhas redes sociais
Siga-me nas redes sociais, eu estarei sempre a disposíção para conversar e trocar idéias. Sempre que eu puder estarei postando novidades!

[![github](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/mayannaoliveira)
[![gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white&link=mailto:mayannait@gmail.com)](mailto:mayannait@gmail.com)
[![whatsapp](https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://api.whatsapp.com/message/5XLG4UPSFCNWP1)
[![linktree](https://img.shields.io/badge/linktree-39E09B?style=for-the-badge&logo=linktree&logoColor=white)](https://linktr.ee/mayannaoliveira)
[![instagram](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/oliveiramayanna/)
[![twitter](https://img.shields.io/badge/twitter-blue?style=for-the-badge&logo=twitter&logoColor=white)](ttps://twitter.com/oliveiramayanna/)
</div>

<!-- Links de referência -->
[Postgres]: https://www.postgresql.org/
[SQL Tools]:https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools
[Visual Studio Code]: https://marketplace.visualstudio.com/vscode
[Docker Hub]: https://hub.docker.com/
[Quickstart: Compose and Django]: https://docs.docker.com/samples/django/
[Docker]: https://docs.docker.com/
[Django]: https://www.djangoproject.com/
[Docker pela Microsoft]: https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker

