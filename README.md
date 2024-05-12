# imersao-alura-google

Projeto final do curso **Imersão IA** da [Alura](https://www.alura.com.br/) e Google, explorando o uso do [Gemini](https://gemini.google.com), configuração e uso do **AI Studio** e técnicas de engenharia de comandos (**prompting**).

É uma solução para aplicação de IA na classificação de livros e identificação do seu local de armazenamento.

Neste projeto o **Gemini** deverá atuar como um bibliotecário, e armazenar cada livro recebido na estante apropriada, selecionada para armazenar livros de assuntos pré-definidos. Os livros são identificados pelas características que forem fornecidas, por exemplo, Título, Autor, Editora, ISBN, etc.

Aqui inserimos uma situação extraordinária, uma restrição que força a IA a adotar novos critérios para reclassificação considerando apenas 6 estantes com os assuntos:

Estante|Assunto
---|---
1|esportes
2|biografia
3|romance
4|culinária
5|terceiro setor
6|outros

Permite ainda a inclusão de novas instruções, em tempo real, para introduzir novos critérios na reclassificação dos livros, por exemplo fornecendo novas instruções do tipo ```a editora X só publica livros de romance``` ou ```o autor Y escreve sobre esportes```.


# Para executar este projeto

Carregar e executar o arquivo ```imersaoia-alura-google.ipynb``` no seu ambiente do [Colab](https://colab.research.google.com/).

Não esqueça de configurar com sua **API_KEY** antes de executar este projeto, veja como fazer isso [aqui](
https://github.com/google-gemini/cookbook/blob/main/quickstarts/Authentication.ipynb)





