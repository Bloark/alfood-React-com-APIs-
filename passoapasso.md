# Passo á Passo

1. Criado projeto base.
2. npm install
3. npm start (Iniciar projeto.)
4. Acessar atraves do http://localhost:3000/
5. Rodar Api resturantes_api-master
6. Dentro da pasta restaurantes_api-master docker-compose build
7. Para subir api docker-compose up
8. Instalação do npm i axios (Fazer requisções entre API)
9. Obtendo restaurantes via api
10. Configuração incial para testra api:
```js
    useEffect(() => {
        //Obter restaurantes
        axios.get('http://localhost:8000/api/v1/restaurantes/')
        .then(resposta => {
        console.log(resposta)
        })
        .catch(erro => {
        console.log(erro)
        })
    }, [])
```
11. Configurando para obter dados através de api

```js
    const [restaurantes, setRestaurantes] = useState<IRestaurante[]>([])
    
    useEffect(() => {
        //Obter restaurantes
        axios.get('http://localhost:8000/api/v1/restaurantes/')
        .then(resposta => {
            setRestaurantes(resposta.data.results)
        })
        .catch(erro => {
        console.log(erro)
        })
    }, [])
```
12. Paginação devidamente tratada devidamente tratada.
13. Criando interface de paginação
```js
    export interface IPaginacao<T> {
        count: number
        next: string
        previous: string
        results: T[]
    }
```

14. Criado Paginação e função de paginação de restaurantes.

```js
    const verMais = () => {
        axios.get<IPaginacao<IRestaurante>>(proximaPagina)
        .then(resposta => {
            setRestaurantes([...restaurantes, ...resposta.data.results])
            setProximaPagina(resposta.data.next)
        })
        .catch(erro => {
            console.log(erro)
        })
    }

    return (<section className={style.ListaRestaurantes}>
        <h1>Os restaurantes mais <em>bacanas</em>!</h1>
        {restaurantes?.map(item => <Restaurante restaurante={item} key={item.id} />)}
        {proximaPagina && <button onClick={verMais}>
        Ver Mais
        </button>}
    </section>)
```
15. 
