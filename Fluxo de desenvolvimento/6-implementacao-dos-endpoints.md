# Implementação dos endpoints

## Users

- [**GET all users**](https://drive.google.com/file/d/1_g-0xAogjBVjFhHQYmolnb57SnFGfOnV/view?usp=share_link)
    - é comum existir um query params para mudar o comportamento da busca

- [**POST user**](https://drive.google.com/file/d/10tvbMzeg9CkH5UIH5LJs_5pH8ZAzLDJ1/view?usp=share_link)
    - dados de entrada são obrigatórios
    - validação > funcionalidade
    - é importante tipar a tabela do banco de dados

- [**DELETE user by id**](https://drive.google.com/file/d/1UBSqhzs9t5Fhnk2x5k5tImvhEQIKp7Lp/view?usp=share_link)
    - path params é sempre string
    - validamos se a id já existe
    - *correção acerca do vídeo:
        - para validar se a id recebida começa com a letra “f” precisamos olhar para a posição [0] e não a [1]
    - [**refatorando para garantir a constraint Foreign Key**](https://drive.google.com/file/d/1_ckUh0SmCy3uAU9gUxJNBXqaoxhmm82b/view?usp=share_link)

