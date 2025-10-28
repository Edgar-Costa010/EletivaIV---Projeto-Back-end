# tcc

classDiagram
    direction TB
    class Paciente {
        +UUID id
        +String nome
        +String cpf
        +Date data_nascimento
        +String genero
        +String telefone
        +String email
        +String endereco
        +String convenio
    }
    class Profissional {
        +UUID id
        +String nome
        +String crm
        +String especialidade
        +String telefone
        +String email
        +Enum perfil
    }
    class Agenda {
        +UUID id
        +Date data
        +Time hora_inicio
        +Time hora_fim
        +Enum status
    }
    class Consulta {
        +UUID id
        +UUID paciente_id
        +UUID profissional_id
        +Date data
        +Time horario
        +Enum tipo   // presencial | telemedicina
        +String status
    }
    class Prontuario {
        +UUID id
        +UUID paciente_id
        +Text anotacoes
        +Date criado_em
    }
    class Prescricao {
        +UUID id
        +UUID consulta_id
        +Text medicamentos
        +Text posologia
        +Date emitida_em
    }
    class Leito {
        +UUID id
        +String codigo
        +Enum estado  // livre | ocupado | em_limpeza
    }
    class Estoque {
        +UUID id
        +String item
        +Integer quantidade
        +String unidade
    }
    class Usuario {
        +UUID id
        +String username
        +String senha_hash
        +Enum role
    }
    class LogAuditoria {
        +UUID id
        +UUID usuario_id
        +String acao
        +Text detalhe
        +DateTime timestamp
    }

    Paciente "1" -- "0..*" Consulta : realiza
    Profissional "1" -- "0..*" Consulta : presta
    Paciente "1" -- "0..*" Prontuario : possui
    Consulta "1" -- "0..1" Prontuario : referencia
    Consulta "1" -- "0..*" Prescricao : gera
    Leito "1" -- "0..1" Paciente : aloca
    Usuario <|-- Profissional
    Usuario <|-- Recepcionista
    Usuario "1" -- "0..*" LogAuditoria : gera
    Estoque "1" -- "0..*" Leito : abastece
