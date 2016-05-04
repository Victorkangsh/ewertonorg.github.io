---
layout: post
title: Trabalhando com arquivos em Ruby
date:   2016-05-02 12:48:00
categories: iniciante
---

> "You seek the one not willing to be found"

A frase acima é um verso da música Pyramid God da banda grega de death metal sinfônico  [Septic Flesh](http://www.septicflesh.com/).É banda estou ouvindo enquanto escrevo esse post.

![alttext](https://upload.wikimedia.org/wikipedia/en/f/fa/Septicflesh-the-great-mass-artwork.jpg)

Este é meu primeiro post sobre a linguagem Ruby e nele vou falar um pouco sobre manipulçãoes de arquivo. 
A classe File da API do Ruby é uma abstração de objetos que são criados para representar um arquivo. Com essa api podemos manipular arquivos, por exemplo saber o tamanho de um arquivo.


{% highlight bash %}
[1] pry(main)> f = File.new("newfile.txt",  "w+")                                                                                                                         
=> #<File:newfile.txt>
[2] pry(main)> f.size                                                                                                                                                     
=> 0
[3] pry(main)> f=File.open('newfile.txt','w') do |f|                            
[3] pry(main)*   f.puts 'sdjlashdkahsdlç'                                       
[3] pry(main)* end   

[1] pry(main)> f=File.open('newfile.txt','r')                                                                                                                     
[2] pry(main)> f.size                                                           
=> 17


{% endhighlight %}

No primeiro parametro passamos o arquivo e no segundo passamos 
o  modo como iremos manipular o arquivo. As maneiras mais comuns são:

 -  r abre o arquivo somente para leitura;
 -  w abre o arquivo somente para escrita (sobrescreve todo o con-
teúdo do arquivo se o mesmo existir);
 - w+ abre o arquivo tanto para leitura quanto para escrita (sobre-
screve todo o conteúdo do arquivo se o mesmo existir);
 -  a abre o arquivo somente para escrita (começa a escrita no final
da última linha existente se o arquivo já existir).


Agora irei irei criar um projeto onde irei adicionar as bandas que ando escultando ultimamente.
Criando uma pasta chamda playlist e dentro dela uma pasta chamada lib.

{% highlight bash %}
mkdir -p playlist/lib 
{% endhighlight %}


Vou cirar um projeto chamado playlist que salva as músicas que irei ouvir em um arquivo yaml.
O primeiro arquivo que vou cirar é o arqivo reponsável por carregar todas as classes desse projeto.

{% highlight bash %}
cd playlist/lib 

touch load_playlist.rb
	
touch music.rb
{% endhighlight %}
Em  load_playlist.rb

{% highlight bash %}
require File.expand_path('lib/track')
require File.expand_path('lib/playlist')

{% endhighlight %}

Em track.rb
{% highlight ruby %}
class Track
  def initialize name, album, release, band
	  @name=name
	  @band=band
	  @album=album
	  @release=release
  end
  
	def to_s
	  "Album: #{@album}, name: #{@name}, band: #{@band},release#{@release}"
	end
end

{% endhighlight %}
em playlist.rb

{% highlight ruby %}
class Playlist
	def save_tracks track
		File.open('playlist.yaml', 'a') do |file|
			file.puts YAML.dump track
			file.puts ""
		end	
	end
end
{% endhighlight %}
{% highlight bash %}

[1] pry(main)> require File.expand_path('lib/load_playlist')                                                                                                   
=> true

pry(main)> Playlist.new.save_tracks Track.new "Pyramid God", "The Great Mass", '2011', 'Septicflesh'

pry(main)> Playlist.new.save_tracks Track.new "Thanatolatria", "Life", '2012', 'Kataphero'

pry(main)> Playlist.new.save_tracks Track.new "O Father O Satan O Sun!", "The Satanist", '2014', 'Behemoth'                                                                            


{% endhighlight %}

{% highlight yaml %}

--- !ruby/object:Track
name: Pyramid God
band: Septicflesh
album: The Great Mass
release: '2011'

--- !ruby/object:Track
name: Thanatolatria
band: Kataphero
album: Life
release: '2012'


--- !ruby/object:Track
name: O Father O Satan O Sun!
band: Behemoth
album: The Satanist
release: '2014'




{% endhighlight %}
