# Same Origin Policy (SOP)

### O que é?
O SOP é um mecanismo de segurança que restringe como documentos e scripts de uma origem interagem com os dados de outra origem, ou seja ele isola as duas origens diminuindo a chance de ter um potencial documento ou script malicioso sendo um vetor de ataque.

### O que define origem?
Uma origem é definida por três componentes, o seu protocolo, a sua porta e o seu host.  
Por exemplo em https://example.com:443/directory  
O host seria o example.com  
O protocolo seria o https://  
A porta seria 443  

http://web.example.com/dir/inner/another.html  
http://docs.example.com/dir/page.html  
https://web.example.com/page.html  
http://web.example.com/dir2/other.html  

Quais desses são da mesma origem?

### Acessos entre origens
* Cross-origin writes são tipicamente permitidos. Exemplos são links, redirects, and form submissions. Some HTTP requests require preflight.
    * Existe a partir disso uma vulnerabilidade, conhecida como cross-site request forgery (CSRF).
    * Preflight é o envio de um HTTP com o método OPTIONS antes do “real” request.
* Cross-origin embedding é tipicamente permitido.
    * Exemplos de embedding são JavaScripts com ```<script src="…"></script>```
* Cross-origin reads são tipicamente **não** permitidos, mas alguns casos pode ser permitido pelo embedding. Por exemplo, pode ser lido as dimensões de imagens, ações de scripts a disponibilidade de um recurso.

### Como liberar acessos entre origens?
**Cross-origin resource sharing** é um mecanismo baseado nos headers do HTTP, que libera o acesso de recursos entre origens diferentes.

O CORS	 é feito através de alguns headers, mas os principais são os headers:	
* Access-Control-Allow-Origin
	* As origens especificadas nesse header tem o direito dos acessos aos recursos entre origens
* Access-Control-Allow-Credentials
	* Um booleano, caso seja True, ele utiliza as credenciais, como cookies e HTTP Authentication ao fazer o request cross-origin

### Como fazer request entre origens?

Uma forma muito comum de fazer request entre origens é através da classe de JavaScript [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) nessa classe, existem muitos metodos para configurar o request, vale ressaltar também que não só retorna dados XML, mas qualquer dado.

#### Vamos as práticas?
[Exercicios](https://portswigger.net/web-security/cors)


**Referências**  
[Vulnerabilidade e Exercicios](https://portswigger.net/web-security/cors)  
[Same Origin Policy](https://developer.mozilla.org/pt-PT/docs/Web/Security/Same-origin_policy)  
[Cross Origin Resource Sharing](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)  

![Logo Tebas](https://github.com/rcrs4/Tebas/blob/novas-aulas/LogoIcon.png)

Feito por Rafael Carneiro Reis de Souza
