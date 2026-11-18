<div align="center">

# 🧵 Threadit — Software Architecture Document

**Análise e documentação da arquitetura de software da API Threadit**

![Data](https://img.shields.io/badge/Data-Dezembro%202025-blue)
![Curso](https://img.shields.io/badge/MEI-FCUL-darkgreen)
![Go](https://img.shields.io/badge/Go-gRPC-00ADD8?logo=go&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-GKE-326CE5?logo=kubernetes&logoColor=white)
![SonarQube](https://img.shields.io/badge/SonarQube-An%C3%A1lise%20est%C3%A1tica-4E9BCD?logo=sonarqube&logoColor=white)

</div>

---

## 📌 Sobre o projeto

Este repositório contém o **Software Architecture Document (SAD)** do **Threadit**, uma API *cloud-native* que reproduz as funcionalidades de um fórum online: comunidades, *threads*, comentários, votos, pesquisa e conteúdo popular.

> 🔗 **Projeto analisado:** [github.com/ThreaditApp/Threadit](https://github.com/ThreaditApp/Threadit)
>
> O Threadit **não foi desenvolvido pelos autores deste repositório**. Este trabalho consiste apenas na **análise e documentação da sua arquitetura**.

O documento segue o modelo ***Views and Beyond*** (SEI) e foi produzido no âmbito da unidade curricular de **Design de Software**.

| | |
|---|---|
| 🎓 **Curso** | Mestrado em Engenharia Informática |
| 📚 **Unidade Curricular** | Design de Software (2025/26) |
| 🏛️ **Instituição** | Faculdade de Ciências da Universidade de Lisboa |
| 📅 **Data** | Dezembro de 2025 |

---

## 👥 Autores

| Nome | Número |
|---|:---:|
| **Eduardo Proença** | 57551 |
| **Pedro Rosa** | 60294 |
| **Tiago Martins Silva** | 66494 |

---

## 📂 Conteúdo do repositório

```
SAD_Threadit/
├── README.md                              # Este ficheiro
└── SAD_Threadit_57551_60294_66494.pdf     # Software Architecture Document
```

### 📄 O que está no SAD

- **Roadmap da documentação** — stakeholders (programadores, testers, gestor de projeto, utilizadores finais) e definição dos *viewpoints*.
- **Contexto arquitetural** — requisitos de qualidade (modularidade, desempenho, escalabilidade, segurança) e abordagens adotadas.
- **Vistas arquiteturais**
  - 🧩 **Decomposition View** — organização do código (`code/kubernetes`, `code/services`, `grpc-gateway`, `models`, `gen`, `dataset`).
  - 🔄 **Runtime View** — interação entre serviços via **REST** e **gRPC**.
  - ☁️ **Deployment View** — *deploy* em **Kubernetes (GKE)** com **Traefik**, **MongoDB** com volume persistente e *pipeline* CI/CD com **GitHub Actions**.
- **Relações entre vistas**
- **Análise SonarQube** — problemas de qualidade, segurança e manutenibilidade identificados, e correções aplicadas.
- **Glossário e acrónimos**

---

## 🏗️ Visão geral da arquitetura

```
              Cliente (HTTP/REST)
                     │
                     ▼
          ┌─────────────────────┐
          │  Traefik (Ingress)  │
          └──────────┬──────────┘
                     ▼
          ┌─────────────────────┐
          │    gRPC-Gateway     │   REST ➜ gRPC
          └──────────┬──────────┘
                     │ gRPC
   ┌────────┬────────┼────────┬────────┬────────┐
   ▼        ▼        ▼        ▼        ▼        ▼
community thread  comment   vote   search  popular
 service  service service service service service
   └────────┴────────┴────┬───┴────────┴────────┘
                          ▼
                   ┌────────────┐
                   │ db-service │
                   └─────┬──────┘
                         ▼
                   ┌────────────┐
                   │  MongoDB   │  (volume persistente)
                   └────────────┘
```

---

## 📖 Como consultar

O documento completo está no ficheiro [`SAD_Threadit_57551_60294_66494.pdf`](SAD_Threadit_57551_60294_66494.pdf), que pode ser aberto diretamente no GitHub ou em qualquer leitor de PDF.

---

## 🛠️ Tecnologias do sistema analisado

| Camada | Tecnologia |
|---|---|
| Linguagem | Go |
| Comunicação | gRPC, REST (gRPC-Gateway), Protocol Buffers |
| API Gateway / Ingress | Traefik |
| Base de dados | MongoDB |
| Orquestração | Kubernetes · Google Kubernetes Engine |
| CI/CD | GitHub Actions |
| Qualidade de código | SonarQube |

---

<div align="center">

**Design de Software · FCUL · Dezembro de 2025**

Eduardo Proença · Pedro Rosa · Tiago Martins Silva

</div>
