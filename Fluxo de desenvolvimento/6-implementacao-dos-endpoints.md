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

## Tasks

- [**GET all tasks**](https://drive.google.com/file/d/1xs2jwRWlIPcWGTZhquS-tRZ1WKWbNK14/view?usp=share_link)
    - é comum existir um query params para mudar o comportamento da busca

- [**POST task**](https://drive.google.com/file/d/1Z2ZwTp_WK-Sp7I4ZaV4LnrpeZaDH9tUv/view?usp=share_link)
    - dados de entrada são obrigatórios
        - porém algumas colunas no banco de dados são preenchidas automaticamente
    - validação > funcionalidade
    - é importante tipar a tabela do banco de dados

- [**PUT task by id**](https://drive.google.com/file/d/1I1SdpmlAMe_8DP1sy3V-bfBZcQDljMX5/view?usp=share_link)
    - dados de entrada são opcionais
    - **[refatorando para garantir a constraint Foreign Key](https://drive.google.com/file/d/12nvoDUwOPvOSLNCD-WNu2NajJCtIk_gy/view?usp=share_link)**
    
- [**DELETE task by id**](https://drive.google.com/file/d/1aEbhrxH2KcpYEJU99LBAn-jsxrj2KgO4/view?usp=share_link)
    - path params é sempre string
    - validamos se a id já existe
    - **[refatorando para garantir a constraint Foreign Key](https://drive.google.com/file/d/1gFBW1s79jbRNLC8D13i8x8evqWXpxGtv/view?usp=share_link)**
    
## Users + Tasks

- **[POST user to task by ids](https://drive.google.com/file/d/11fEy0kNmyunSFTLsefIrTMbGw18Cnc-l/view?usp=share_link)**
    - recebendo as ids via path params

- **[DELETE user from task by ids](https://drive.google.com/file/d/1d8qdzMiwll6xGfZFhnB3evwAvjqvlCNz/view?usp=share_link)**
    - recebendo as ids via path params