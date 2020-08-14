# ArquiteturainternanoNodeefilas.md
Entender como o ecossistema do node trabalha!!! 
-tomar cuidado para nao blockar a thread principal 
- usar o worker 
- usar fila 
- dificilmente vc vai ter um controller que cai ou uma api que nao funciona 
- quantos async await vc tem ? 
- delay de Ram ,delay de rede ... (tempo de requisitao) 
- overflow , heap de memoria um pequeno ajuste worker consegue resolver e escalar a aplicação 
- só o golang consegue ganhar do node em processamento de IO, mas precisa entender a arquitetura do node 
- mais de cinco metodos já quebra em outro controle 
- botar pra background 
- evitar a aglomeração de requisições 


Arquitetura interna no Node e filas
- Motor V8 
- como o node abstraiu o ES 
- filas e workers 
- js é mais lento que golang  e c++ 
- otimizar processos no kubernets 

- ES é um padrão , não se deve dizer eu programa em ES 
- Tc39 aprova ou desapova features para o Es
- Chrome é uma engine do JS 
- v8 pega as features do Es e implementa em c++ 
- o node roda no v8 e faz a interface 
- o node faz o parse do c++ 
-> JS code ->(transpilado para  v8)  c++ -> machine code 

-node tem uma thread principal (single thread - event loop) 
- joga pra uma stack 
- tudo é transpilado dentro do v8 para c++ 
- via libuv pega o código Js abre um processo de c++ processa a fila e devolve em JS 

- event loop tem um limite de hardware físico , a  thread principal blocka se vc por exemplo faz muitas escritas em log no disco . Foi feita uma refatoração para desocupar o event loop. 

![](https://github.com/luizrosalba/ArquiteturainternanoNodeefilas.md/blob/master/Capturar222222222.PNG?raw=true)

- a thread principal eh single
![](https://github.com/luizrosalba/ArquiteturainternanoNodeefilas.md/blob/master/Capturar33333.PNG?raw=true)

- utilizaçãode workers : Consulta cpf (receita) -> 1 minuto de tempo consulta o servidor cai 
- o cadasatro está em aprovação 
- microjob feito dentro da thread do worker 
- depois responde para o client 

-> rabbit MQ client worker message interessante se vc tiver muitas mensagens para nao derrubar o server ou tomar overhead de tempo de processamento 

![](https://github.com/luizrosalba/ArquiteturainternanoNodeefilas.md/blob/master/Capturarccccc.PNG?raw=true)





