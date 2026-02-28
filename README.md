# 🎬 Codeflix: Microsserviço Admin do Catálogo de Vídeos

Este repositório contém o back-end do módulo de Administração do Catálogo de Vídeos do projeto Codeflix, desenvolvido como aplicação prática do curso Full Cycle.

O objetivo principal deste microsserviço é gerenciar o catálogo de vídeos (incluindo categorias, gêneros e membros do elenco), servindo como a fonte de verdade (source of truth) para esses dados no ecossistema da plataforma.

---

## 🏗️ Arquitetura e Padrões

O projeto foi construído utilizando forte embasamento em Engenharia de Software, garantindo um código desacoplado, testável e escalável. Os principais conceitos aplicados são:

* **Clean Architecture:** Separação clara de responsabilidades através de camadas concêntricas (Entities, Use Cases, Gateways/Presenters e Interfaces Externas).
* **Screaming Architecture:** A estrutura de diretórios (`application`, `domain`, `infrastructure`) "grita" o propósito do negócio antes mesmo de revelar os frameworks utilizados.
* **Domain-Driven Design (DDD):** Modelagem estratégica focada no coração do negócio.
    * **Tactical Patterns:** Uso extensivo de *Value Objects* (Identifier, Name, Money, Date), *Aggregates/Entities* e *Domain Services*.
    * **Principais Agregados:** `Category`, `Genre`, `Cast Member` e `Video`.

---

## 🛠️ Stack Tecnológica (The Big Picture)

* **Linguagem:** Java 17
* **Framework:** Spring Boot (Expondo APIs REST)
* **Build System:** Gradle (Kotlin DSL)
* **Banco de Dados:** MySQL (para persistência do catálogo)
* **Mensageria/Eventos:** RabbitMQ (para integração assíncrona com outros microsserviços, como o Encoder de vídeos)
* **Storage:** Google Cloud Storage (Bucket de vídeos brutos)
* **Sincronização de Dados:** Kafka Connect (com Debezium MySQL) replicando os dados para o Elasticsearch (usado pela API de Catálogo).

---

## 🧪 Estratégia de Testes

A qualidade da aplicação é garantida através do conceito da **Pirâmide de Testes**:

1. **Testes Unitários (Base):** Testam a menor parte testável (métodos, classes e funções) de forma isolada e extremamente rápida, sem depender de frameworks.
2. **Testes de Integração (Meio):** Verificam a interação entre duas ou mais unidades e a integração com o framework (ex: bind de requisições, queries em repositórios, chamadas HTTP). Encontram-se majoritariamente na camada de infraestrutura.
3. **Testes E2E / End-to-End (Topo):** Testam a API de ponta a ponta. No contexto deste microsserviço, os testes sobem toda a aplicação e simulam chamadas reais nos endpoints.
