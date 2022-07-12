## Backend

Utilizei o Mongoose para fazer a conexão da API com um banco de dados mongoDB, para isso criei um esquema o qual define os atributos de um documento dentro de uma coleção. O esquema criado representa um veículo no banco de dados e seus atributos são os seguintes:
 ```sh
   {
    name: String,
    brand: String,
    description: String,
    plate: String,
    isFavorite: Boolean,
    year: Number,
    color: String,
    price: Number,
    createdAt: { type: Date, default: Date.now }
  }
   ```

Através do esquema, eu criei um modelo, o qual é uma classe com a qual eu posso construir (instanciar) novos documentos, salvar esses documentos no banco de dados e fazer consultas. À classe criada foi dado o nome de Vehicle e é através dela que faremos toda a comunicação com o banco de dados.  

Utilizei o express para construir as rotas da api:

### /vehicles
##### METHOD = GET
Esta rota devolve todos os veículos cadastrados no banco de dados. Para isso utilizamos a Classe Vehicle e o método find; este devolve todos os registros dentro da coleção.
Se tudo correr bem, então uma resposta com status 200 e todos os veículos cadastrados no banco de dados são enviados.

### /save_vehicle
##### METHOD: POST
Esta rota espera receber um objeto no body de requisição e a partir deste objeto, cria um novo documento a partir da classe Vehicle e o salva no banco de dados através do método save. 

### /vehicle/:id
##### METHOD=DELETE
Esta rota é responsável por deletar o objeto cujo id foi passado no url, para isso, utiliza-se a classe Vehicle com o método “findByIdAndDelete”, passando o id como parâmetro.

### /favorite/:id
##### METHOD=PUT
Esta rota altera o estado do atributo “isFavorite” do objeto cujo id foi passado na url, para isso, encontra-se o objeto através da classe Vehicle e do método “findById”, depois, altera-se o atributo e salva-se o objeto de novo no banco de dados.

### vehicle/:id
##### METHOD = PUT
Esta rota atualiza os atributos do objeto cujo id foi passado no url pelos valores dos atributos do objeto passado no body da requisição.


## Rodando a aplicação

1. Clone o repositório e navegue até o diretório

2. Primeiro rode um container com mongodb
   ```sh
   docker run -d -p 27017:27017 --name some-mongo mongo
   ```
3. Crie a imagem docker da aplicação
```sh
   docker build . -t node/corelab-api
```

4. Rode um container da imagem da aplicação
    ```sh
   docker run -p 3333:3333 --link some-mongo:some-mongo node/corelab-api
   ```
   A aplicação deve estar rodando na porta 3333


