# 🛡️ TaskForce (Offline-First)

![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![BLoC](https://img.shields.io/badge/State-BLoC-blue?style=for-the-badge)
![Offline First](https://img.shields.io/badge/Strategy-Offline_First-green?style=for-the-badge)

> **Gerenciador de tarefas robusto com sincronização automática.**
> Este projeto demonstra a implementação de uma arquitetura **Offline-First** real, onde a aplicação funciona plenamente sem internet e sincroniza dados quando a conexão é restabelecida.

---

## 🏗️ Arquitetura e Tecnologias

O projeto segue o padrão **MVVM (Model-View-ViewModel)** com **Clean Architecture** simplificada.

-   **Gerência de Estado:** Flutter BLoC.
-   **Banco de Dados Local:** SQLite (via pacote **Drift**) ou Isar.
-   **Sincronização:** Queue de requisições e UUIDs locais.
-   **Conectividade:** Monitoramento de rede em tempo real.
-   **Injeção de Dependência:** GetIt + Injectable.

### 🔄 Estratégia Offline-First

A "Fonte da Verdade" (Single Source of Truth) neste app é o **Banco de Dados Local**.

1.  **Leitura:** A UI sempre exibe dados do banco local.
2.  **Escrita:**
    -   O usuário cria/edita uma tarefa.
    -   O dado é salvo imediatamente no banco local (com uma flag `isSynced = false`).
    -   O app tenta enviar para a API em background.
    -   Se falhar (sem internet), o dado permanece local.
    -   Um "SyncManager" monitora a conexão e envia os dados pendentes quando possível.

---

## 📂 Estrutura de Pastas

```text
lib/
├── core/                # Utilitários, constantes e serviços globais (NetworkInfo)
├── data/                # Repositories e Datasources
│   ├── local/           # Banco de Dados (Drift/Isar)
│   ├── remote/          # API Client (Dio)
│   └── repositories/    # Implementação da lógica de sincronização
├── domain/              # Entidades e Interfaces (Contratos)
├── presentation/        # UI (Blocs, Pages, Widgets)
└── main.dart
```

---

👨‍💻 Autor
Desenvolvido por Sancho18 como estudo de caso para arquiteturas resilientes.