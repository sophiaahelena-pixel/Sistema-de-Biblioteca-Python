# 📚 Sistema de Gerenciamento de Biblioteca em Python

Sistema desenvolvido em Python para o controle e gerenciamento de acervo de uma biblioteca, permitindo o cadastro, busca, empréstimo, devolução e contagem de livros com persistência de dados em formato JSON.

---

## 🚀 Funcionalidades

* **Cadastro de Livros:** Adiciona novos títulos ao acervo validando campos vazios, duplicidade de títulos e formato numérico do ano de publicação.
* **Listagem Completa:** Exibe todos os livros cadastrados e seus respectivos status de disponibilidade.
* **Busca Flexível:** Permite localizar obras rapidamente filtrando por **título** ou por **autor**.
* **Gestão de Empréstimos e Devoluções:** Atualiza o status do livro entre "Sim" (disponível) e "Não" (emprestado).
* **Remoção de Acervo:** Exclui registros do sistema de forma segura.
* **Contador Estatístico:** Apresenta um resumo dinâmico do total de obras, exemplares disponíveis e emprestados.
* **Persistência de Dados:** Salva e carrega automaticamente as informações utilizando um arquivo `livros.json`.

---

## 🛠️ Tecnologias Utilizadas

* **Python 3.x**
* Módulo nativo `json` para manipulação de arquivos locais.

---

## ⚙️ Como Executar o Projeto

1. Certifique-se de ter o [Python instalado](https://www.python.org/) na sua máquina.
2. Clone este repositório ou faça o download dos arquivos `código.py` e `livros.json` (o arquivo JSON será gerado automaticamente caso não exista).
3. Abra o terminal na pasta do projeto e execute o script:

```bash
python código.py
