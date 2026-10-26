# Sistema-de-Biblioteca-Python
import json
ARQUIVO = "livros.json"
livros = []


def carregar_livros():
    """Lê o arquivo JSON e coloca os livros na lista."""
    global livros
    try:
        arquivo = open(ARQUIVO, "r", encoding="utf-8")
        livros = json.load(arquivo)
        arquivo.close()
    except FileNotFoundError:
        # Se o arquivo ainda não existe, começa com a lista vazia
        livros = []

def salvar_livros():
    """Grava a lista de livros no arquivo JSON."""
    arquivo = open(ARQUIVO, "w", encoding="utf-8")
    json.dump(livros, arquivo, ensure_ascii=False, indent=4)
    arquivo.close()

def mostrar_livro(livro):
    """Mostra os dados de um livro."""
    print("Título:", livro["titulo"])
    print("Autor:", livro["autor"])
    print("Ano:", livro["ano"])
    print("Disponível:", livro["disponivel"])
    print("-" * 30)

def procurar_livro(titulo):
    """Procura um livro pelo título. Devolve o livro ou None."""
    for livro in livros:
        if livro["titulo"].lower() == titulo.lower():
            return livro
    return None

  def cadastrar_livro():
    """Cadastra um novo livro."""
    print("\n--- Cadastrar livro ---")
 
    titulo = input("Título: ").strip()
    autor = input("Autor: ").strip()
    ano = input("Ano: ").strip()
 
    # Validação: nenhum campo pode ficar vazio
    if titulo == "" or autor == "" or ano == "":
        print("Erro: preencha todos os campos.")
        return
 
    # Validação: o ano precisa ser um número
    if not ano.isdigit():
        print("Erro: o ano deve conter apenas números.")
        return
 
    # Não deixa cadastrar dois livros com o mesmo título
    if procurar_livro(titulo) is not None:
        print("Erro: esse livro já está cadastrado.")
        return
 
    livro = {
        "titulo": titulo,
        "autor": autor,
        "ano": int(ano),
        "disponivel": "Sim"
    }
 
    livros.append(livro)
    salvar_livros()
    print("Livro cadastrado com sucesso!")
 
def listar_livros():
    """Mostra todos os livros cadastrados."""
    print("\n--- Lista de livros ---")
 
    if len(livros) == 0:
        print("Nenhum livro cadastrado.")
        return
 
    for livro in livros:
        mostrar_livro(livro)
 
 
def buscar_livro():
    """Busca livros pelo título ou pelo autor."""
    print("\n--- Buscar livro ---")
    print("1 - Buscar por título")
    print("2 - Buscar por autor")
    opcao = input("Escolha: ").strip()
 
    if opcao != "1" and opcao != "2":
        print("Opção inválida.")
        return
 
    texto = input("Digite o que deseja buscar: ").strip().lower()
    encontrou = False
 
    for livro in livros:
        if opcao == "1":
            campo = livro["titulo"].lower()
        else:
            campo = livro["autor"].lower()
 
        # "in" verifica se o texto aparece dentro do campo
        if texto in campo:
            mostrar_livro(livro)
            encontrou = True
 
    if not encontrou:
        print("Nenhum livro encontrado.")
 
def emprestar_livro():
    """Muda a disponibilidade do livro de Sim para Não."""
    print("\n--- Emprestar livro ---")
    titulo = input("Título do livro: ").strip()
    livro = procurar_livro(titulo)
 
    if livro is None:
        print("Livro não encontrado.")
    elif livro["disponivel"] == "Não":
        print("Esse livro já está emprestado.")
    else:
        livro["disponivel"] = "Não"
        salvar_livros()
        print("Empréstimo realizado!")
 
 
def devolver_livro():
    """Muda a disponibilidade do livro de Não para Sim."""
    print("\n--- Devolver livro ---")
    titulo = input("Título do livro: ").strip()
    livro = procurar_livro(titulo)
 
    if livro is None:
        print("Livro não encontrado.")
    elif livro["disponivel"] == "Sim":
        print("Esse livro já está disponível.")
    else:
        livro["disponivel"] = "Sim"
        salvar_livros()
        print("Devolução registrada!")
 
 
def remover_livro():
    """Remove um livro do acervo."""
    print("\n--- Remover livro ---")
    titulo = input("Título do livro: ").strip()
    livro = procurar_livro(titulo)
 
    if livro is None:
        print("Livro não encontrado.")
    else:
        livros.remove(livro)
        salvar_livros()
        print("Livro removido!")
 
 
def contar_acervo():
    """Mostra quantos livros existem, disponíveis e emprestados."""
    total = len(livros)
    disponiveis = 0
    emprestados = 0
 
    for livro in livros:
        if livro["disponivel"] == "Sim":
            disponiveis = disponiveis + 1
        else:
            emprestados = emprestados + 1
 
    print("\n--- Contador do acervo ---")
    print("Total de livros:", total)
    print("Disponíveis:", disponiveis)
    print("Emprestados:", emprestados)
 
 
def mostrar_menu():
    """Mostra as opções do menu."""
    print("\n===== BIBLIOTECA =====")
    print("1 - Cadastrar livro")
    print("2 - Listar livros")
    print("3 - Buscar livro")
    print("4 - Emprestar livro")
    print("5 - Devolver livro")
    print("6 - Remover livro")
    print("7 - Contador do acervo")
    print("0 - Sair")
 
 
def main():
    """Função principal: carrega os dados e repete o menu."""
    carregar_livros()
 
    while True:
        mostrar_menu()
        opcao = input("Escolha uma opção: ").strip()
 
        if opcao == "1":
            cadastrar_livro()
        elif opcao == "2":
            listar_livros()
        elif opcao == "3":
            buscar_livro()
        elif opcao == "4":
            emprestar_livro()
        elif opcao == "5":
            devolver_livro()
        elif opcao == "6":
            remover_livro()
        elif opcao == "7":
            contar_acervo()
        elif opcao == "0":
            print("Saindo... Até logo!")
            break
        else:
            print("Opção inválida. Tente novamente.")

main()
