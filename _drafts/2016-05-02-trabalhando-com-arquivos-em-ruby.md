---
layout: post
title: Trabalhando com arquivos em Ruby
date:   2016-05-02 12:48:00
categories: iniciante
---

> "You seek the one not willing to be found"

A frase acima é um verso da música Pyramid God da banda grega de death metal sinfônico  [Septic Flesh](http://www.septicflesh.com/). Essa  pe a música que estou ouvindo enquanto escrevo esse post.

![alttext](https://i.ytimg.com/vi/AFY_RuQQgYU/0.jpg)

Este é meu primeiro post sobre a linguagem Ruby e nele vou falar um pouco sobre API File. 
A classe File da API do Ruby é uma abstração de objetos que são criados para representar um arquivo. Com essa api podemos manipular arquivos, por exemplo saber o tamanho de um arquivo.


{% highlight bash %}
[1] pry(main)> f = File.new("newfile.txt",  "w+")                                                                                                                         
=> #<File:newfile.txt>
[2] pry(main)> f.size                                                                                                                                                     
=> 0

{% endhighlight %}

No primeiro parametro passamos o arquivo e no segundo passamos 
o  modo como desejamos abrir o arquivo. As maneiras mais comuns são:

 -  r abre o arquivo somente para leitura;
 -  w abre o arquivo somente para escrita (sobrescreve todo o con-
teúdo do arquivo se o mesmo existir);
 - w+ abre o arquivo tanto para leitura quanto para escrita (sobre-
screve todo o conteúdo do arquivo se o mesmo existir);
 -  a abre o arquivo somente para escrita (começa a escrita no final
da última linha existente se o arquivo já existir).
