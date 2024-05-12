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

Para testar a chave usando o ```curl```
```DOS
curl -H "Content-Type: application/json" \ -d "{\"contents\":[{\"parts\":[{\"text\":\"Explain how AI works"\}]}]}" -X POST "https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=GOOGLE_API_KEY"
```


# Execução

Este projeto apresenta um prompt interativo para receber as instruções do usuário:
```
Digite informações do livro a ser armazenado, o número da estante para conferir os livros armazenados, ou 0 para sair:
```

Algumas perguntas feitas no início da execução do projeto:

>**Quais são as estantes disponíveis para armazenar os novos livros?**
```
1: Esportes
2: Biografia
3: Romance
4: Culinária
5: Terceiro Setor
6: Outros
```

>**Quais são os livros armazenados na estante 2?**
```
Nenhum livro foi armazenado até o momento, pois ainda não recebi nenhuma lista de livros para classificação.
Assim que você fornecer a lista de livros, classificarei cada um deles e informarei em qual prateleira o livro foi armazenado, incluindo os livros que devem ser armazenados na estante 2: Biografia.
```

Após algum tempo, a pergunta foi refeita:

>**Quais são os livros armazenados na estante 2?**
```
Até o momento, apenas um livro foi armazenado na estante 2:
* **A Segunda Guerra Mundial** de Antony Beevor
Outros livros podem ser armazenados nesta estante se forem classificados como biografias.
```


A cada livro fornecido, a localização do mesmo (e a justificativa da reclassificação) é informada, por exemplo:

> **A Segunda Guerra Mundial (Antony Beevor)**
```
**Título:** A Segunda Guerra Mundial
**Autor:** Antony Beevor
**Prateleira:** 2 (Biografia)

**Justificativa:** O livro é uma biografia da Segunda Guerra Mundial, portanto, deve ser armazenado na estante de Biografia
```


Novas instruções foram fornecidas durante a execução para ajustar o comportamento da IA:

>**considerar, a partir deste momento, que todos os livros da Editora Harlequin são romance.**
```
Entendido. A partir de agora, todos os livros da **Editora Harlequin** serão considerados **Romance** e armazenados na **estante 3**.
Isso significa que, se você receber um livro da Editora Harlequin, ele será automaticamente classificado como Romance e armazenado na estante 3, independentemente do título, autor ou qualquer outra informação.
```

>**quando receber um novo livro, armazena e informe em qual estante ele foi armazenado, assim:<br><br>titulo diario de anne frank<br>editora record<br>isbn 8501044458<br><br>resposta: Estante 2**
```
**Título:** Diário de Anne Frank
**Editora:** Record
**ISBN:** 8501044458
**Prateleira:** 2 (Biografia)

**Justificativa:** O livro é um diário escrito por Anne Frank durante a Segunda Guerra Mundial e conta a história de sua família se escondendo dos nazistas. Portanto, o livro pode ser classificado como uma biografia histórica e deve ser armazenado na estante de Biografia.

**Observação:** Embora a Editora Record tenha publicado o livro, a Editora Harlequin não é mencionada como editora. Portanto, a regra de considerar todos os livros da Editora Harlequin como Romance não se aplica neste caso.
```

Alguns exemplos de reclassificação para se adequar aos assuntos disponíveis:

>**O Menino do Pijama Listrado (John Boyne)**
```
**Título:** O Menino do Pijama Listrado
**Autor:** John Boyne
**Prateleira:** 2 (Biografia)

**Justificativa:** Embora o livro seja uma obra de ficção, ele é baseado em eventos reais do Holocausto e conta a história de dois meninos de origens muito diferentes que se tornam amigos em um campo de concentração. Portanto, o livro pode ser classificado como uma biografia histórica e deve ser armazenado na estante de Biografia.
```

>**Perigoso! Histórias emocionantes (Tim Warnes)**
```
**Título:** Perigoso! Histórias Emocionantes
**Autor:** Tim Warnes
**Prateleira:** 6 (Outros)

**Justificativa:** O livro é uma coleção de contos que não se encaixam em nenhuma das outras categorias disponíveis (Esportes, Biografia, Romance, Culinária, Terceiro Setor). Portanto, o livro deve ser armazenado na estante "Outros".
Digite informações do livro a ser armazenado, o número da estante para conferir os livros armazenados, ou 0 para sair
```

>**a coragem de ser imperfeito (brené broen)**
```
**Título:** A Coragem de Ser Imperfeito
**Autor:** Brené Brown
**Prateleira:** 6 (Outros)

**Justificativa:** Embora o livro aborde temas de psicologia e desenvolvimento pessoal, ele não se encaixa perfeitamente em nenhuma das outras categorias disponíveis (Esportes, Biografia, Romance, Culinária, Terceiro Setor). Portanto, o livro deve ser armazenado na estante "Outros".
```

>**tcc expressa (mcclure, friedberg, thordarson, keller) editora artmed**
```
**Título:** TCC Expressa
**Autores:** McClure, Friedberg, Thordarson e Keller
**Editora:** Artmed
**Prateleira:** 6 (Outros)

**Justificativa:** Embora o livro seja sobre terapia cognitivo-comportamental (TCC), ele é voltado para profissionais da saúde mental e não para o público em geral. Portanto, o livro deve ser armazenado na estante "Outros", que abrange livros que não se encaixam perfeitamente em nenhuma das outras categorias disponíveis.
```

