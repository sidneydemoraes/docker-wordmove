# Docker-Wordmove

Fork de mfuezesi/docker-wordmove que foi abandonado há mais de 2 anos.
Wordmove é um projeto ainda ativo que pode ser encontrado em welaika/wordmove com documentação.

## Como usar
Veja em https://medium.com/cluetip/wordpress-development-made-easy-440b564185f2.

Ou um post mais recente em https://medium.com/@KentaKodashima/wordpress-wordpress-development-with-docker-compose-and-wordmove-cf720d2618d

## Troubleshoot

### `invalid byte sequence in UTF 8` ao tentar usar `push` ou `pull` do db
1. Caso seu wordpress tenha o WordFence instalado, procure o arquivo `config/Movefile` neste projeto e remova o caracter de comentário da opção `mysqldump_options`.

2. Esta solução pode corromper dados do seu banco caso ele realmente tenha caracteres de outros `charset`, então use com cuidado. Se a opção 1 não tiver resolvido, edite o arquivo abaixo no container do wordmove. _Obs: utilizo o vim no exemplo, mas pode ser qualquer editor._
```
$ vim `find / -type d -name 'wordmove'`/sql_adapter/default.rb
```
Adicione o seguinte bloco de código acima da linha 45.
```
sql_content.encode!('UTF-16', 'UTF-8', :invalid => :replace, :replace => '')
sql_content.encode!('UTF-8', 'UTF-16')
sql_content.force_encoding("UTF-8")
```
