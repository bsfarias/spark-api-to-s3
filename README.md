# SPARK API TO S3

## Introdução
Este projeto foi criado com a finalidade de extrair os dados de uma API e persistir os dados em um storage. A [API da Nasa](https://api.nasa.gov/) foi utilizada e um job spark foi desenvolvido para acessá-la, processar o retorno e persistir o resultado em um bucket S3 da AWS.

## Pré-requisitos:
* [docker](https://www.docker.com/products/docker-desktop)
* Chave para acessar a [API](https://api.nasa.gov/)
* Ter um [Bucket](https://docs.aws.amazon.com/pt_br/AmazonS3/latest/user-guide/create-configure-bucket.html) S3 na AWS
* Usuário no [IAM](https://docs.aws.amazon.com/pt_br/IAM/latest/UserGuide/id_users_create.html) com Access Key e Secret Key
* Usuário no IAM com permissão de gravação no S3

## Construção do ambiente através do docker compose:
   - No terminal, Execute o seguinte comando:
```
cd spark-api-to-s3/docker/
docker-compose up
```   

## Execução do job spark:
   - Acesse o container e faça o submit do job spark:
```
docker exec -i -t spark-api-to-s3 /bin/bash

spark-submit --master local[*] --packages  org.apache.hadoop:hadoop-aws:3.1.0 \
/home/jovyan/scripts/spark_api_to_s3.py \
<Nasa API Key> \
<Start Date> \
<End Date> \
<Bucket name> \
<Aws Access Key> \
<Aws Secret Key>
```