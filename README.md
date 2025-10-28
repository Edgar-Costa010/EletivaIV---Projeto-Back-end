#Projeto Bask-end
```erDiagram
    PACIENTE {
        UUID id PK
        varchar nome
        varchar cpf
        date data_nascimento
        varchar telefone
        varchar email
    }
    PROFISSIONAL {
        UUID id PK
        varchar nome
        varchar crm
        varchar especialidade
    }
    USUARIO {
        UUID id PK
        varchar username
        varchar senha_hash
        varchar role
    }
    CONSULTA {
        UUID id PK
        UUID paciente_id FK
        UUID profissional_id FK
        timestamp data_hora
        varchar tipo
        varchar status
    }
    PRONTUARIO {
        UUID id PK
        UUID paciente_id FK
        text anotacoes
        timestamp criado_em
    }
    PRESCRICAO {
        UUID id PK
        UUID consulta_id FK
        text medicamentos
        text posologia
    }
    LEITO {
        UUID id PK
        varchar codigo
        varchar estado
    }
    ESTOQUE {
        UUID id PK
        varchar item
        integer quantidade
        varchar unidade
    }
    LOG_AUDITORIA {
        UUID id PK
        UUID usuario_id FK
        varchar acao
        text detalhe
        timestamp timestamp
    }

    PACIENTE ||--o{ CONSULTA : "possui"
    PROFISSIONAL ||--o{ CONSULTA : "realiza"
    PACIENTE ||--o{ PRONTUARIO : "possui"
    CONSULTA ||--o{ PRESCRICAO : "gera"
    USUARIO ||--o{ LOG_AUDITORIA : "gera"
