# Conhecendo o Supabase

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

O **Supabase** é uma plataforma de desenvolvimento de backend como serviço (BaaS) de código aberto, que oferece soluções completas para criar rapidamente a infraestrutura necessária em um aplicativo. Ele se destaca por usar tecnologias já consolidadas, como o **PostgreSQL** (como banco de dados) e o **PostgREST** (para criar automaticamente uma API RESTful a partir do banco). Isso facilita o desenvolvimento, especialmente em projetos como aplicativos móveis.

Vamos entender três funcionalidades principais que o Supabase oferece:

## Authentication

O módulo de **Authentication** do Supabase permite a criação e gerenciamento de usuários, autenticação com provedores externos e verificação de segurança em uma aplicação. Em um app React Native, isso é particularmente útil para criar funcionalidades de login, logout e autenticação de usuários.

* **Criação de Conta e Login**: Supabase permite que os usuários criem contas usando e-mail e senha, e oferece autenticação de provedores externos (como Google, GitHub, Facebook, etc.).
* **Autenticação de Sessão**: Ao fazer login, o Supabase gera um token JWT para gerenciar a sessão do usuário, permitindo o acesso seguro a dados e funcionalidades.
* **Recuperação de Senha e Verificação de E-mail**: Ferramentas para reset de senha e verificação de e-mail estão disponíveis, o que melhora a segurança e a experiência do usuário.

## Database

O Supabase usa o **PostgreSQL** como banco de dados, oferecendo uma experiência de banco de dados SQL relacional, com a vantagem de ser altamente escalável. Esse banco suporta dados complexos, como JSON, e conta com funcionalidades avançadas de SQL.

* **CRUD e Real-time**: Com o Supabase, é possível realizar operações de CRUD (Create, Read, Update, Delete) diretamente pela API REST ou por meio de consultas SQL. Um dos diferenciais é o **real-time** — qualquer atualização no banco é transmitida em tempo real para o cliente, facilitando a atualização automática de dados em apps.
* **Controle de Acesso**: O Supabase permite configurar regras de segurança (Row Level Security - RLS) no nível das linhas do banco, essencial para limitar o acesso aos dados com base na autenticação do usuário.
* **Consultas Avançadas**: Oferece suporte para consultas complexas, incluindo junções (JOINs) e filtros, e é otimizado para desempenho.

## Storage

O **Supabase Storage** é um sistema para armazenamento de arquivos e mídia, permitindo o upload e gerenciamento de arquivos, como imagens, vídeos e documentos. Em aplicativos móveis, é útil para armazenar imagens de perfil, documentos ou qualquer arquivo que precise ser mantido no servidor.

* **Upload e Download de Arquivos**: Supabase oferece uma API para fazer upload de arquivos e organizá-los em pastas, como uma estrutura de buckets.
* **Controle de Permissão**: O Supabase permite definir o acesso aos arquivos de forma pública ou privada, ideal para proteger documentos sensíveis e tornar públicas somente as mídias autorizadas.
* **Integração com o Database**: É possível armazenar metadados dos arquivos no banco de dados, relacionando o armazenamento com as informações do usuário, como dados de perfil.

## Conclusão

O Supabase é uma plataforma robusta para construir o backend de aplicativos com React Native, com funcionalidades integradas que facilitam a criação de apps com autenticação de usuários, banco de dados em tempo real e armazenamento seguro de arquivos. Como é open source, pode ser adaptado e escalado conforme as necessidades do projeto.
