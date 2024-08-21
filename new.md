classDiagram
    Usuario <|-- Administrador
    Usuario <|-- Operador
    Usuario <|-- UsuárioNormal

    class Usuario {
    <<abstract>>
    - nome: String[50]
    - email: String[50]
    - senha: String[64]
    - dataCadastro: DateTime
    + autenticar(): Boolean
    + realizarLogin(email: String, senha: String): Boolean
    + realizarLogoff(): void
    }

    class Administrador {
    - tipo: String = "Administrador"
    + criarConta(usuario: Usuario): void
    + editarConta(usuario: Usuario): void
    + excluirConta(usuario: Usuario): void
    + listarContas(): List<Usuario>
    + gerarRelatorioDeConsumo(): Relatorio
    + monitorarDesperdicio(): void
    }

    class Operador {
    - tipo: String = "Operador"
    + criarCardapio(cardapio: Cardapio): void
    + editarCardapio(cardapio: Cardapio): void
    + excluirCardapio(cardapio: Cardapio): void
    + listarCardapios(): List<Cardapio>
    + visualizarCardapioDoDia(): Cardapio
    + registrarPreparoEDistribuicao(refeicao: Refeicao): void
    + visualizarRelatorioDeDesperdicioEEstoque(): Relatorio
    }

    class UsuárioNormal {
    - tipo: String = "UsuárioNormal"
    }

    class Cardapio {
    - id: int
    - nome: String[100]
    - descricao: String[255]
    - data: Date
    }

    class Relatorio {
    - id: int
    - tipo: String
    - conteudo: String
    - dataGeracao: DateTime
    }

    class Refeicao {
    - id: int
    - descricao: String[255]
    - quantidade: int
    }

    class EstoqueAlimentos {
    - id: int
    - nome: String[100]
    - quantidade: int
    - descricao: String[255]
    }

    Usuario "1" o-- "0..*" Relatorio : gera
    Usuario "1" o-- "0..*" Refeicao : registra
    Operador "1" o-- "0..*" Cardapio : cria
    Operador "1" o-- "0..*" Cardapio : edita
    Operador "1" o-- "0..*" Cardapio : exclui
    Operador "1" o-- "0..*" EstoqueAlimentos : cria
    Operador "1" o-- "0..*" EstoqueAlimentos : edita
    Operador "1" o-- "0..*" EstoqueAlimentos : exclui
    Operador "1" o-- "0..*" EstoqueAlimentos : lista
    Operador "1" o-- "0..*" Relatorio : visualiza
    Administrador "1" o-- "0..*" Usuario : gerencia
    Administrador "1" o-- "0..*" Relatorio : gera
    Administrador "1" o-- "0..*" EstoqueAlimentos : monitoriza
    Operador "1" o-- "0..*" Refeicao : registra
