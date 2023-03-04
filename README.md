# json-server-base

Esse repositório usou como base o JSON-Server + JSON-Server-Auth do tsunode(https://github.com/Kenzie-Academy-Brasil-Developers/json-server-base).

## Endpoints

Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 3 endpoints que podem ser utilizados para cadastro e 2 endpoints que podem ser usados para login.

### Importar todas as requisições no Insomnia

[![Run in Insomnia}](https://insomnia.rest/images/run.svg)](https://insomnia.rest/run/?label=YourSchool%20FakeAPI&uri=https%3A%2F%2Fyourschool-api.onrender.com%2Finsomnia.json)

### Cadastro

POST /register <br/>
POST /signup <br/>
POST /users

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

### Login

POST /login <br/>
POST /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"

### Aluno - buscar aluno e suas notas (requer token)

GET /users/${studentId}

As notas são do tipo string pois inicialmente os alunos não tem notas e colocar 0 para inicializar confundiria com um real 0 na matéria.

### Responsável - buscar filhos e suas notas (requer token)

GET /users?cpfParent=${parentCpf}

### Professor - buscar alunos e suas notas (requer token)

GET /users?class=${professorClass}

A classe (className) representa um nome, que pode tanto ser um "número" quanto um texto, por isso é inicialmente do tipo string.

### Professor - adicionar aluno a turma / remover aluno da turma / alterar nota (requer token)

PATCH /users/${studentId}

Adicionar aluno a turma:
Alterar a chave class do aluno para ser a mesma do professor e adicionar a chave grades com as matérias baseado na turma (você pode descobrir as matérias na requisição de buscar matérias da turma), pelo insomnia acredito que colocar diretamente as máterias e notas (chave grades) é mais fácil.

Remover aluno da turma:
Basta enviar a chave class com valor de string vazia.

Alterar nota:
Basta enviar a chave grades com as alterações desejadas, mas atenção, precisa enviar todas as matérias, até as que não forem alteradas.

### Buscar matérias da turma (requer token)

GET /classes?class=${className}

Com essa requisição você consegue ver as matérias daquela turma.


### Professor - pesquisar aluno pelo nome (requer token)

GET /users?class=${className}&name_like=${inputValue}

Na hora da requisição passar como parâmetro o valor do campo (input), dessa forma pesquisando como um filter dentro da fake API.