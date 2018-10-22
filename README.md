
#### Projeto de mineração de dados do Twitter

# Instalação

    git clone git://github.com/andersoonluan/twitter_python.git
    
## Dependencias
- [Twython](https://github.com/ryanmcgrath/twython)

Rode o comando:

    pip install -r requirements.txt

# Como usar

* Criar conta de Developer e registrar o app pelo link: https://dev.twitter.com/apps.
* Após o registro, criar o Access Token para obter informações de  ``Consumer Key``, ``Consumer Secret``, ``Access token`` e ``Access token secret``.Inserir informações no arquivo ``config.json`` e ``apikeys`` (Exemplo abaixo).

```json
{
        "apikeys": {
                "config-application": {
                        "app_key": "SEU APP KEY",
                        "app_secret": "SUA APP SECRET",
                        "oauth_token": "SUA OAUTH TOKEN",
                        "oauth_token_secret": "SUA SECRET OAUTH TOKEN"
                }
        }
}

```

## Opções de Comandos

In general,
* `-c`: Arquivo de configuração das API
* `-o`: Pasta de saída dos dados
* `-cmd`: Comando que você deseja executar
* `-cc`: Arquivo de configuração do comando
* `-wait`: aguardar `x` segundos entre as chamadas.


### Filtrar por `geolocalização`
- [statuses/filter](https://developer.twitter.com/en/docs/tweets/filter-realtime/api-reference/post-statuses-filter)
- `-cmd`: `locations`
- `-cc`: e.g., `test_data/geo/US_BY_STATE_1.json` 
```bash
# Streaming API: get tweets within geo boundries defined in -cc test_data/geo/US_BY_STATE_1.json
python twitter_streamer.py -c ./config.json -o /mnt/data2/twitter/US_BY_STATE -cmd locations -cc test_data/geo/US_BY_STATE_1.json

```

## REST APIs


### Pesquisar por keywords
- [search/tweets](https://developer.twitter.com/en/docs/tweets/search/api-reference/get-search-tweets.html)
- `-cmd`: `search`
- `-cc`: `test_data/search.json` 

```json
{  
   "keyword_list_0":{  
      "geocode":null,
      "terms":[  
         "\"gremio\"",
         "\"gremio libertadores\"",
         "\"gremio #gremio\"",
         "\"#gremio inter\"",
         "\"gremiocampeao\"",
         "\"#gremiocampeao\""
      ],
      "since_id":1,
      "querystring":"(\"gremio\") OR (\"gremio campeao\") OR (\"gremio #gremiocampeao\") OR (\"#gremio internacional\") OR (\"gremiocampeao\") OR (\"#gremiosim\")"
   }, 
   "keyword_list_1": {
      "geocode": [
      "dona_ana_nm",
      "32.41906196127472,-106.82334114385034,51.93959956432837mi"
      ],
      "querystring": "(\"gremiocampeao #gremiocampeao\") OR (\"gremiocampeao\") OR (\"#cancercervical\")",
      "since_id": 0,
       "terms": [
         "gremiocampeao #gremiocampeao",
         "gremiocampeao",
         "#gremiocampeao"
       ]
   }
}
```
```bash
# Pesquise utilizando o código abaixo.
python twitter_tracker.py -c ./config.json -cmd search -o data/search_query -cc test_data/search.json -wait 5
```
