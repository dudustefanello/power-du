# Acesso à dados Trello

### Os seguintes métodos mostram todos os campos permitidos, você só precisa incluir aqueles que você deseja.

Todos retornam promessas que determinam para um objeto com os campos solicitados:

* Obter informações sobre o quadro atual
  * ``t.board ('id', 'nome', 'url', 'shortLink', 'membros');``

* Obter informações sobre a lista atual (disponível somente quando uma lista específica está em contexto), Então, por exemplo, disponível dentro de "anexos-seções" ou "cartões-crachás", mas não 'show-settings' ou 'board-buttons'
  * ``t.list ('id', 'name', 'cards');``

* Obtenha informações sobre todas as listas abertas no quadro atual
  * ``t.lists ('id', 'name', 'cards');``

* Obtenha informações sobre o cartão atual (somente disponível quando um cartão específico está em contexto). Então, por exemplo, disponível dentro de "anexos-seções" ou "cartões-crachás", mas não 'show-settings' ou 'board-buttons'
  * ``t.card ('id', 'name', 'desc', 'due', 'closed', 'cover', 'attachments', 'members', 'labels', 'url', 'shortLink', 'idList ');``

* Obtenha informações sobre todos os cartões abertos no quadro atual
  * ``t.cards ('id', 'nome', 'desc', 'devido', 'fechado', 'capa', 'anexos', 'membros', 'rótulos', 'url', 'shortLink', 'idList ');``

* Obtenha informações sobre o membro Trello ativo atual
  * ``t.member ('id', 'fullName', 'nome de usuário');``

Para acesso ao resto dos dados da Trello, você precisará usar a API RESTful. Isso exigirá que você pergunte ao usuário para autorizar o Power-Up a acessar o Trello em seu nome. Incluímos um exemplo de como faça isso na seção "Autorização Capacidades" na parte inferior.

### Armazenando / Recuperando seus próprios dados
O Power-Up oferece 4096 caracteres de espaço por escopo / visibilidade. Os seguintes métodos retornam Promessas.

* O armazenamento de dados segue o formato:
  * ``t.set ('scope', 'visibility', 'key', 'value');``
Com os escopos, você só pode armazenar dados no escopo do cartão quando um cartão está no escopo. Então, por exemplo, no contexto de "cartões-crachás" ou "anexos-seções", mas não "placas-insígnias" ou "configurações de exibição"
Também tenha em mente que armazenar no escopo da "organização" só funcionará se o usuário ativo for um membro da equipe

* As informações que são privadas para o usuário atual, como tokens, devem ser armazenadas usando 'private' no escopo do 'member'
  * ``t.set('organization', 'private', 'key', 'value');``
  * ``t.set('board', 'private', 'key', 'value');``
  * ``t.set('card', 'private', 'key', 'value');``
  * ``t.set('member', 'private', 'key', 'value');``

* As informações que devem estar disponíveis para todos os usuários do Power-Up devem ser armazenadas como "compartilhadas"
  * ``t.set('organization', 'shared', 'key', 'valor');``
  * ``t.set('board', 'shared', 'key', 'value');``
  * ``t.set('card', 'shared', 'key', 'valor');``
  * ``t.set('member', 'shared', 'key', 'valor');``

* Se você quiser configurar várias chaves ao mesmo tempo você pode fazer isso assim
  * ``t.set('board', 'shared', {key: value, extra: extraValue});``

* Ler seus dados é tão simples quanto
  * ``t.get('organization', 'shared', 'key');``

* Ou quer todos os dados de escopo ao mesmo tempo?
  * ``t.getAll ();``
