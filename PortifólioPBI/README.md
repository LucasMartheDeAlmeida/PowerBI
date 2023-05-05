#Power Bi linguagem M

Linguagem M é a linguagem de consulta e transformação de dados utilizada pelo Power Query, uma ferramenta de ETL (Extract, Transform and Load) que permite a conexão, importação e manipulação de dados em diversas fontes de dados, incluindo planilhas, bancos de dados, arquivos de texto e fontes de dados na nuvem. Nessa linguagem, é possível escrever consultas e expressões para transformar e limpar dados, criar colunas calculadas, agrupar, filtrar e classificar dados, e até mesmo desenvolver funções personalizadas.

Para editar um código em lingagem M no power BI é necessário primeiro abrir o PowerBI e em seguida:

```Transformar Dados > Nova fonte > Consulta nula```

1. Abrir o Power BI;
2. Ir para a guia "Transformar Dados";
3. Selecionar "Nova Fonte";
4. Selecionar "Consulta Nula";
5. Selecionar a guia "Página Inicial";
6. Clicar em "Editor Avançado".

Com isso é necessário abrir o editor avançado, através da guia Página Inicial e cliacno em **Editor avançado*. Logo após isso é possível assimilar que exite a declaração de duas variáveis associadas no bloco ```let``` e por conseguinte no bloco in que associa as mesmas na guia "Etapas aplicadas", com isso o bloco de linguagem M foi alterado para exibir a seguinte consulta:

```
let
    Var1=
            let
                a= "Power"
            in
                a,
    Var2=
            let
                b= "Query"
            in
                b
in
    Var1

```

com a modificação do bloco em questão é possível assimilar que está sendo axibida a palara "Power" no editor power query que está contida em ```Var1``` as variáveis definidas no primeiro bloco let são denominadas *Variáveis globais*.


##Concatenação de strings

Para concatenar as strings é possível utilizar o operador & entre as variáveis que precisam ser concatenadas, resultando no seguinte techo de código:

```
let
    Var1=
            let
                a= "Power"
            in
                a,
    Var2=
            let
                b= "Query"
            in
                b
in
    Var1 & Var2
```

Tal código resulta na concatenação das Strings "Power" e "Query".


Como em qualquer linguagem de programação tipada a linguagem M possui alguns tipos primitivos bem definidos e distindos entre sí, alguns deles são


* ``` type null ```: que classifica o valor nulo.
* ```type logical ```: que classifica os valores true e false.
* ```type number ```: que classifica valores numéricos.
* ```type time ```: que classifica valores de tempo.
* ```type date ```: que classifica valores de data.
* ``` type datetime ```: que classifica valores de datetime.
* ```type datetimezone ```:que classifica valores de datetimezone.
* ``` type duration```: que classifica valores de duração
* ``` type text```:  que classifica valores de texto
* ```type type ```: que classifica valores de tipo
* ```type list ```:  que classifica valores de lista.
* ```type record ```:que classifica valores de registro.
* ```type table```: que classifica valores de tabela
* ```type function ```: que classifica valores de função.
* ``` type anynonnull```: que classifica todos os valores, exceto o nulo. O tipo abstrato none não classifica nenhum valor.

Curiosamente, os tipos primitivos abordam não apenas os valores primitivos como binary, date, list, number, etc, como também valores abstratos como: function, table, none e o próprio any.


## Listas

Para armazenar valores em uma lista é necessário armazena-los em uma variável por meio do operador {}, resultando em uma declaração da seguinte forma: 
```
numero = {1,2,3,4,5}
```

para liscar os números de forma mais eficiênte quando se trata de grandes intervalos numéricos, pode ser utilizado o operador ```..``` da seguinte maneira:

```
= {1,..99}

```
A consulta acima retorna uma listagem em colunas acima lista valores de 1 a 99 em forma de  tabela, sendo o título da tabela delcarado como Lista enumerados com um índice de 1 a 99.


É possível também retornar o alfabeto com a seginte consulta

```
= {"A"..."Z}
```

Com isso pode-se retornar as duas listas fazendo uma lista de listas
```
mistura = {numeros,alfabeto}

```

retornando uma tabela contendo a lista 0 e lista 1, para acessalas basta definir no retorno ```mistura{1}``` ou ```mistura{0}```


Agora criando uma tabela pela interface gráfica é possível atribuir colunas e linhas, e alterando o código M da mesma pode-se atribuir a tabela pelo seguinte código:

```

let
    Fonte = Table.FromRows(Json.Document(Binary.Decompress(Binary.FromText("i45WclTSUTJUitWJVnICsoyUYmMB", BinaryEncoding.Base64), Compression.Deflate)), let _t = ((type nullable text) meta [Serialized.Text = true]) in type table [Texto = _t, Numero = _t]),
    TipoAlterado = Table.TransformColumnTypes(Fonte,{{"Texto", type text},{"Numero",Int64.Type}})
in
    TipoAlterado

```
Com o intuito de retornar uma tabela com a coluna do tipo Texto contendo os caracteres A e B no formato texto e 1 e 2 no formato Int64, é possível também acessar uma coluna específica, alterando a chamada da variável no retorno com colchetes ```TipoAlterado[Texto]``` e acessar os elemnentos das colunas com chaves ```TipoAlterado[Texto]{0}```


# Criando uma Tabela

Para criar uma tabela é possível iniciar uma consulta nula, na qual pode-se declarar uma tabela de maneira análoga a um array de arrays JSON da seguinte maneira:

```
let
    Table = #table(
    {
        "Nome","Data","Idade","CRM"
    },
    {
        {
            "Lucas Marthe","01/01/2022",20,2234
        },
                {
            "Lucas Almeida","01/01/2022",20,2235
        },
                {
            "Lucas Silva","01/01/2022",20,2238
        },
                {
            "Lucas Cunha","01/01/2022",20,2239
        }
    }
),
    #"Tipo Alterado" = Table.TransformColumnTypes(Table,{{"Nome", type text}})
in
    #"Tipo Alterado"

```

Com o intuito de entrar em padrão complience serão alterados os tipos das outras variáveis, utiliando numeros inteiros e a função ````#date``` da seguinte forma:
```
= #table(
        type table
        [
            Nome = text,
            Data = date,
            Idade = number,
            CRM = number
        ],
    {
        {
            "Lucas Marthe",#date(2022,01,01),20,2234
        },
                {
            "Lucas Almeida",#date(2022,01,01),20,2235
        },
                {
            "Lucas Silva",#date(2022,01,01),20,2238
        },
                {
            "Lucas Cunha",#date(2022,01,01),20,2239
        }
    }
)
```
# Funções

para criar uma função basta criar uma consulta nunla e interir a seguinte sintaxe:

```
() =>
    "Hello Word"

```

pode-se inserir parâmetros para concatenr e somar valores, os quais podem ser inseridos por interface gráfica no Power Query

```
(a , b) =>
    a+b

```

no entando no caso desta função não podem ser passados valore não numéricos, e para tal é possível restringir a entrada de valores para evitar o acionamento de gatilhos de erro

```
(a as number , b as number) =>
    a+b

```

Agora podemos declarar uma tabela de temperaturas da seguinte maneira:
```
    TabelaTemperaturas = List.Generate(
        () => [Temperatura = -37],
        each [Temperatura] <= 68,
        each [Temperatura = [Temperatura] + 1],
        each [Temperatura]
    ),
    #"Converteu em Tabela" = Table.FromList(TabelaTemperaturas, Splitter.SplitByNothing(), {"Temperatura"}),
    #"Função Personalizada Invocada" = Table.AddColumn(#"Converteu em Tabela", "temp", each temp([Temperatura]))
```

e classificar as temperaturas dessa tabela de forma com que ao lado da temperatura a mesma seja classificada como quente, amena ou frio com a função abaixo:

```
(temp as number)=>

let  
        messege = 
                    if temp > 37 then "Quente"
                    else if temp <= 0 then"Frio"
                    else "Ameno"
                    
in  
    messege


```
