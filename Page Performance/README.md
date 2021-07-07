# PAGE PEFORMANCE INSIGHTS
## Documentation: https://developers.google.com/speed/docs/insights/BlockingJS?hl=pt-BR
```
Entre o pedido do cliente para mostrar uma página na web e a renderização completa dessa página, muitas coisas acontecem. Temos muitas métricas para determinar o quão otimizada é esta página, algumas delas são: FCP (First Contentful Paint), LCP (Largest Contentfull Paint), CLS (Communative Layout Shift), SEO, etc.

FCP - First Contentfull Paint

É o tempo que se da entre o click do usuário entrando na URL da página e a aparição do primeiro conteúdo mostrado na tela. (A primeira div não vazia, ou não branca).

LCP - Largest Contentfull Paint

Durante o tempo de carregando muitas partes diferentes serão desenhadas. Essa métrica mede o tempo até a maior porcentagem da tela já ter sido renderizada, ou o tempo até que o usuário veja a maior parte da página e acredite que ela está (quase) pronta.

Por exemplo: em muitos casos o conteúdo que maior preenche a tela são as imagens, ou um vídeo, ou um iframe. Logo se esse tipo de conteúdo for grande (em tamanho de arquivo) ou vier de uma fonte externa que precise ser baixada antes de renderizada, o LCP vai aumentar e isso contribuirá negativamente para a pontuação de otimização pois o usuário irá ver grandes espaços em branco que sem conteúdo no local.

"The user came to your site for a rease, show that reason as fast you can".

CLS - Content Layout Shift

O conteúdo deve se ajustar aos mais variados tamanhos de tela, e em vários momentos os elementos são deslocados quando há mudanças no tamanho da tela. Esta métrica mede a porcentagem da página que foi deslocada. 

FID - First Input Delay

Mede o tempo que se dá entre o click (pedido) do usuário para abrir a página, a execução do código da página pelo browser e a interação do usuário com o sistema.

Em resumo...

A performance esta relacionada a:

- Sua máquina
- Sua rede
- Ao tamanho da janela do navegador
- A prioridade de aplicação do navegador


```
## COMO MELHORAR O FCP
```
Para isso precisamos reduzir o número de bytes trafegando pela rede para chegar até o navegador do usuário. A otimização do FCP depende de 5 fatores, que por sua vez dependem da estratégia e tecnologias utilizados no servidor:

- [ ]  Conteúdo dimensionado corretamente
- [ ]  Minimização do processamento
- [ ]  Largura de banda da rede
- [ ]  Tamanho do conteúdo
    - [ ]  O tamanho total do conteúdo servido pelo servidor deve estar entre 80 a 100 K
- [ ]  Estratégia/utilitário de compressão
    - [ ]  Pode ser usado Gzip para plataformas "antigas" e para browsers mais modernos pode ser utilizado estratégias mais modernas.
- [ ]  É importante reduzir a distancia entre os nós do servidor de origem até o cliente
    - [ ]  Utilizar um CDN mais próximo
```

## COMO MELHORAR O LCP
```
Aqui precisamos mostrar a maior porcentagem de conteúdo o mais rápido possível. Uma vez reduzido o número de bytes trafegando pela rede até o navegador do usuário, como podemos ter certeza de que os bytes que estamos enviando no carregamento da página são os corretos para chegar renderizar o mais rápido possível? 

Ao receber o arquivo html do servidor, o browser irá lê-lo e a cada recurso externo (recurso não presente no próprio arquivo), o browser precisará realizar uma request ao servidor onde esta hospedado o recurso.

Por exemplo:

- Se é encontrado um stylesheet sendo importado, o browser para a leitura do HTML, pede o stylesheet e depois continua.
- Se é encontrado uma imagem, o browser para, pede a imagem ao servidor e depois continua.
- Se é encontrado uma importação de script, o browser para, pede a imagem ao servidor e depois continua.

Otimizar o LCP é reduzir o trabalho que o browser faz até poder mostrar a maior parte do conteúdo da tela, ou algo que dê a impressão para o usuário que o conteúdo esta (ou esta quase) pronto.

A 3 coisas para se focar quando vamos melhorar o LCP:

- [ ]  Adiar recursos para mais tarde (Defer resources until later)
    - [ ]  Usar **defer** nos scripts não necessários para uso imediato na renderização (usar async nesses casos não é uma boa opção, o async faz o browser executar o script a qualquer momento que ele quiser, o defer, garante que só vai ser executado após a renderização do conteúdo).
    - [ ]  Criar um arquivo **lazyloader.js** implementando um **lazyloader** otimizado de acordo com a documentação: [https://web.dev/fast/#lazy-load-images-and-video](https://web.dev/fast/#lazy-load-images-and-video)

        Exemplo de arquivo: [https://github.com/toddhgardner/perf-training-website/blob/main/public/assets/js/util/lazyloader.js](https://github.com/toddhgardner/perf-training-website/blob/main/public/assets/js/util/lazyloader.js)

    - [ ]  Usar **rel="preload"** e **rel="preconnect"** para os arquivos css, fonts e assets necessários na renderização.
- [ ]  Otimizar Imagens

    NOTE: Usar loading="lazy" em imagens não tem efetividade para otimizar o LCP, pois o LCP mede quão rápido o browser lê e mostra o conteúdo, o atributo loading="lazy" faz o browser ler a tag, mas só depois que o usuário foca aquela área a imagem é pedida do servidor e então ao termino download ela é mostrada, isso tonar o tempo entre a leitura e renderização muito maior. Obs: No Safari (android e ios), Internet Explorer e Firefox Android

    - [ ]  Usar Imagens diferentes para cada tamanho de dispositivo e responsive attributes como **srcset** ou e **sizes**. Assim economizamos a banda do usuário fazendo o navegador baixar imagens mais leves em resoluções mais baixas
```

        ```html
        <html>
        	<body>
        		<img 
        				src="picture-1200.jpg" 
        				srcset="picture-600.jpg 600w, 
        								picture-900.jpg 900w,
        								picture-1200.jpg 1200w" 
        				sizes="(max-width: 600px) 600px, 
        							 (max-width: 900px) 900px,
        								1200px"
        		/>
        	</body>
        </html>
        ```
```
    - [ ]  Para imagens ou vídeos pesados, carregue a imagem com qualidade baixa primeiro e depois atualizei a imagem com a qualidade total

- [ ]  Reduzir sobrecarga de requisições (reduce request overhead)
    - [ ]  Se você utiliza **bootstrap** ou outra biblioteca e na página não houver **modals**, **dropdowns** ou outro componente que utiliza javascript, você pode remover os scripts do **jquery**, **popper** e do **bootstrap** reduzindo o trabalho do browser ao ler o HTML, assim o browser não precisa baixar todos esses scripts que ficarão inutilizados.
    - [ ]  Se possível, prefira utilizar o **href** apontando para o **id do elemento** invés de adicionar um modal ou dropdown na página
```
    ```html
    <html>
    	<body>
    		<a href="#form">CADASTRAR AGORA</a>
    		<form id="form">
    			<input type="email"></input>
    		</form>
    	</body>
    </html>
    ```
```
- [ ]  Adicionar um "fake loading" quando utilizar iframes. A ideia aqui é preencher o espaço vazio que o iframe deixaria, com um loading que avisa ao usuário que algo aparecerá ali, mas que passa a ideia para o algoritmo que a tela foi preenchida. Se você utiliza bootstrap, segue abaixo um pequeno truque que pode ser usado com  a classe embed-responsive.
```
    ```html
    <div class="embed-responsive embed-responsive-16by9">
    	<!-- fake loading code -->
      <div 
        id="loading"
        style="position:absolute;top:0;bottom:0;right:0;left:0;"
        class="bg-secondary d-flex justify-content-center align-items-center">
        <h1 class="text-light">...</h1>
      </div>
    	<!-- fake loading code -->
      <iframe
        class="embed-responsive-item"
        src="https://www.youtube.com/embed/AnThftVbKSw?controls=0"
        frameborder="0"
        allow="autoplay; fullscreen; accelerometer; modestbranding; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
        onload="hideLoading()"
        id="vimeo_id_0"
        ></iframe>
    </div>
    ```
## COMO MELHORAR O CSL

- [ ]  Usar **height** e **width** explícitos na tag IMG nos elementos que sabemos que não vão mudar de tamanho a depender do tamanho do dispositivo
- [ ]  Usar **position: fixed** para garantir que o elemento não vai mudar as disposições e tamanho da tela, isso contribuirá na pontuação do light house pois indica que aquele conteúdo não vai ter mudanças de layout.

## Objetivos da melhoria de performance a nível de negócio

- **Captação** (A página precisa ser encontrada e mostrada da melhor forma nos diferentes ambientes)
- **Conversão** (A página deve eliminar todos as objeções de conversão possíveis para aumentar a conversão)
- **Retenção** (A página deve cooperar para que os usuários não deixem a página ou o negócio
- **Competição** (A página deve cooperar para a melhor performance na competição do mercado)