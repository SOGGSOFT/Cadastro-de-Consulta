# API REST - CADASTRO DE CONSULTA

### Autenticação

API baseada na arquitetura REST.
Todas as requisições devem ser enviadas com um token de autenticação no header da requisição HTTP. (Entre em contato com a SOGG SOFT). Ex:

```php 
$request->setHeaders(array(
          'content-type' => 'application/json',
          'Authorization' => {token}
        ));
```

                  
## Enviar Pesquisa

EndPoint: https://homologacao.soggsoft.com.br/ws/combo

Objeto Motorista
| Parâmetro     | Obrigatorio   |
| ------------- |--------------:|
| pesquisa_avancada      | SIM|
| perfil_id      | SIM|
| documento      | SIM|
| nome      | SIM|
| sexo      | SIM|
| nascimento| SIM|
| naturalidade| SIM|
| rg| SIM|
| rg_uf| SIM|
| rg_emissao| NÃO|
| cnh| SIM|
| cnh_uf| SIM|
| cnh_emissao| NÃO|
| cnh_validade| SIM|
| cnh_seguranca| SIM|
| cnh_categoria_id| SIM|
| cnh_prontuario| NÃO|
| filiacao_materno| SIM|
| filiacao_paterno| NÃO|
| contato_telefone| NÃO|
| contato_celular| NÃO|
| contato_email| NÃO|
| anexos| NÃO| 

Request:

Tipo de requisição: `POST`

```json
{
   "motorista":{
      "pesquisa_avancada":"N",
      "perfil_id":"1",
      "documento":"60677546068",
      "nome":"MOTORISTA TESTE",
      "sexo":"M",
      "nascimento":"1992-06-17",
      "naturalidade":"Campo Grande",
      "rg":"21445591",
      "rg_uf":"MT",
      "rg_emissao":"2010-01-01",
      "cnh":"22222222",
      "cnh_uf":"MT",
      "cnh_emissao":"2010-01-01",
      "cnh_validade":"2010-10-01",
      "cnh_seguranca":"33333333",
      "cnh_categoria_id":"4",
      "cnh_prontuario":"2",
      "filiacao_materno":"MAE",
      "filiacao_paterno":"PAI",
      "contato_telefone":"66999999999",
      "contato_celular":"66999999999",
      "contato_email":"CONTATO@SOGGSOFT.COM.BR",
      "anexos":[
         "ImageBase64",
         "ImageBase642"
      ]
   },
   "proprietarios":[
      {
         "perfil_id":"1",
         "doc_proprietario":"25231510068",
         "nome":"PROPRIETARIO 01",
         "sexo":"M",
         "uf":"MT",
         "filiacao_materno":"Mae",
         "filiacao_paterno":"Pai",
         "contato_email":"email@motorista.com.br",
         "contato_celular":"066 9 9695-4545",
         "contato_telefone":"066 3421-5485",
         "documento_proprietario_anexo":"ImageBase64",
         "veiculos":[
            {
               "perfil_id":"1",
               "renavam":"999999999",
               "placa":"CCC1234",
               "chassi":"2222222222",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CAVALO",
               "anexo":"ImageBase64"
            },
            {
               "perfil_id":"1",
               "renavam":"8888888888",
               "placa":"VVV8888",
               "chassi":"333333",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CARRETA",
               "anexo":"ImageBase64"
            }
         ]
      },
      {
         "perfil_id":"1",
         "doc_proprietario":"60677546068",
         "nome":"PROPRIETARIO 02",
         "sexo":"M",
         "uf":"MT",
         "filiacao_materno":"Mae",
         "filiacao_paterno":"Pai",
         "contato_email":"email@motorista.com.br",
         "contato_celular":"066 9 9695-4545",
         "contato_telefone":"066 3421-5485",
         "documento_proprietario_anexo":"ImageBase64",
         "veiculos":[
            {
               "perfil_id":"1",
               "renavam":"999999999",
               "placa":"YYY8989",
               "chassi":"2222222222",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CAVALO",
               "anexo":"ImageBase64"
            },
            {
               "perfil_id":"1",
               "renavam":"8888888888",
               "placa":"YYY9090",
               "chassi":"333333",
               "antt":"8888888",
               "uf":"MT",
               "categoria":"CARRETA",
               "anexo":"ImageBase64"
            }
         ]
      }
   ]
}
```

Response:
Será retornado o código da nova pesquisa gerada, é necessário armarzena-lo para pesquisar o status da consulta posteriormente.

HTTP CODE `201` 
```json
{
   "codigo":"afe6ca1d-f6e2-465f-849c-d93108d428f4",
   "message":"success"
}
```

## Consultar Pesquisa

EndPoint: https://homologacao.soggsoft.com.br/ws/combo/{{idPesquisa}}

Request:

Tipo de requisição: `GET`

Response:
```json
{
   "pesquisa":{
      "id":"fb1e0238-fff1-4d8e-b012-98c6f708c99d",
      "protocolo":"0802.1612818859/2021",
      "status":"HOMOLOGADO",
      "pesquisa_avancada":"N",
      "validade":"2021-02-09",
      "categoria":"COMBO",
      "motorista":{
         "status":"HOMOLOGADO",
         "documento":"60677546068",
         "nome":"MOTORISTA TESTE",
         "sexo":"M",
         "nascimento":"1992-06-17",
         "naturalidade":"Campo Grande",
         "rg":"21445591",
         "rg_uf":"MT",
         "rg_emissao":"2010-01-01",
         "cnh":"22222222",
         "cnh_uf":"MT",
         "cnh_validade":"2010-10-01",
         "cnh_seguranca":"33333333",
         "cnh_categoria_id":"4",
         "cnh_prontuario":"2",
         "filiacao_materno":"MAE",
         "filiacao_paterno":"PAI",
         "contato_telefone":"66999999999",
         "contato_celular":"66999999999",
         "contato_email":"CONTATO@SOGGSOFT.COM.BR",
         "anexos":[
            "https://dev-app.soggsoft.com.br/files/analise_perfil/api/combo/1-6021a571c59a6.png",
            "https://dev-app.soggsoft.com.br/files/analise_perfil/api/combo/1-6021a571c4314.png"
         ]
      },
      "proprietarios":[
         {
            "perfil_id":"1",
            "doc_proprietario":"25231510068",
            "nome":"PROPRIETARIO 01",
            "sexo":"M",
            "uf":"MT",
            "filiacao_materno":"Mae",
            "filiacao_paterno":"Pai",
            "contato_email":"email@motorista.com.br",
            "contato_celular":"066 9 9695-4545",
            "contato_telefone":"066 3421-5485",
            "anexo":"https://dev-app.soggsoft.com.br/files/analise_perfil/api/combo/1-6021a571c898e.png",
            "veiculos":[
               {
                  "perfil_id":"1",
                  "renavam":"8888888888",
                  "placa":"VVV8888",
                  "chassi":"333333",
                  "antt":"8888888",
                  "uf":"MT",
                  "categoria":"COMBO",
                  "anexo":"https://dev-app.soggsoft.com.br/files/analise_perfil/api/combo/1d341635-aced-49e3-9ca1-2fcce8327e19-6021a571d01ad.png"
               },
               {
                  "perfil_id":"1",
                  "renavam":"999999999",
                  "placa":"CCC1234",
                  "chassi":"2222222222",
                  "antt":"8888888",
                  "uf":"MT",
                  "categoria":"COMBO",
                  "anexo":"https://dev-app.soggsoft.com.br/files/analise_perfil/api/combo/50403061-1e8a-4590-8bd0-5b1b670fbe8c-6021a571cc3b0.png"
               }
            ]
         },
         {
            "perfil_id":"1",
            "doc_proprietario":"60677546068",
            "nome":"PROPRIETARIO 02",
            "sexo":"M",
            "uf":"MT",
            "filiacao_materno":"Mae",
            "filiacao_paterno":"Pai",
            "contato_email":"email@motorista.com.br",
            "contato_celular":"066 9 9695-4545",
            "contato_telefone":"066 3421-5485",
            "anexo":"https://dev-app.soggsoft.com.br/files/analise_perfil/api/combo/1-6021a571d36f5.png",
            "veiculos":[
               {
                  "perfil_id":"1",
                  "renavam":"8888888888",
                  "placa":"YYY9090",
                  "chassi":"333333",
                  "antt":"8888888",
                  "uf":"MT",
                  "categoria":"COMBO",
                  "anexo":"https://dev-app.soggsoft.com.br/files/analise_perfil/api/combo/2b223ce5-7a43-45bf-a9d1-b1b9b8ffab1f-6021a571daeb9.png"
               },
               {
                  "perfil_id":"1",
                  "renavam":"999999999",
                  "placa":"YYY8989",
                  "chassi":"2222222222",
                  "antt":"8888888",
                  "uf":"MT",
                  "categoria":"COMBO",
                  "anexo":"https://dev-app.soggsoft.com.br/files/analise_perfil/api/combo/fe2dc4af-d62b-4cf1-ab7c-bc1a9e0324c3-6021a571d757a.png"
               }
            ]
         }
      ]
   }
}
```
# Parâmetros

#### Parâmetros Perfil_id
| Descrição     | Valor   |
| ------------- |--------------:|
| FROTA         | 1|
| AGREGADO      | 2|
| TERCEIRO      | 3|
| AJUDANTE      | 4|




