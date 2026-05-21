# Sis_Ferramentaria - Controle de Ferramentaria & Auxiliar Engeman 🛠️

O **Sis_Ferramentaria** é um ecossistema multiplataforma (Desktop, Web e Mobile) projetado para automatizar o controle de estoque, gerenciamento de demandas e a rastreabilidade em tempo real de ferramentas e ativos em ambientes metalúrgicos industriais. O sistema atua de forma satélite, servindo como um braço de execução rápida para softwares de PCM (Planejamento e Controle de Manutenção), como o **Engeman**.

Este projeto foi desenvolvido de forma 100% autoral para consolidar de forma prática as disciplinas de **Análise e Modelagem de Sistemas**, **Design de Interação Móvel** e **Lógica de Programação**.

---

## 📌 Status do Projeto: `Fase de Desenvolvimento (Back-end)`
*   [x] **Análise de Requisitos & Regras de Negócio**
*   [x] **Modelagem de Dados e Arquitetura**
*   [x] **Design de Interação (UX/UI) e Wireframes no Figma**
*   [ ] **Desenvolvimento do Motor Lógico (Python)** `<- Atual Etapa`
*   [ ] **Integração com Banco de Dados & Hardware (MariaDB / SDK Biométrico)**

---

## 🎯 O Problema & A Solução Industrial

No chão de fábrica, o tempo gasto para retirar uma ferramenta ou a perda de rastreabilidade de um item em manutenção gera paradas na linha de produção e falhas no planejamento do PCM.

O **Sis_Ferramentaria** resolve essa fricção através de um fluxo focado em eficiência operacional:
1. **Operação Multiplataforma:** Interface Desktop (Windows) no balcão integrada ao hardware, Tablet para movimentações dinâmicas e Web para relatórios de atraso e demandas de manutenção.
2. **Dupla Autenticação Biométrica:** Segurança e auditoria total. O empréstimo exige a validação digital do Controlador (credor) e do Colaborador (beneficiário), eliminando fraudes ou assinaturas manuais em papel.
3. **Fluxo de Contingência Inteligente:** Caso a biometria do colaborador apresente falha de leitura (comum na indústria por sujeira ou desgaste), o sistema libera uma trava de segurança que permite ao Controlador assinar digitalmente o empréstimo por meio de uma senha mestra de contingência.

---

## 🏗️ Engenharia e Modelagem do Sistema

Os artefatos de engenharia de software criados para guiar o desenvolvimento do sistema estão mapeados na pasta `/docs/diagramas`:

*   **Regras de Transição de Estados:** Rastreabilidade estrita do ciclo de vida dos ativos através de três estados fixos e imutáveis: `Ferramentaria` (Disponível), `Fábrica` (Em uso) e `Manutenção` (Indisponível).
*   **Diagrama de Classes:** Mapeamento das entidades `Colaborador`, `Ativo` (Ferramentas/Consumíveis) e `HistoricoMovimentacao` para posterior persistência em banco de dados relacional.
*   **Mecanismo de Prevenção de Erros (Poka-Yoke):** Bloqueio lógico a nível de software que impede que ferramentas com status `Manutenção` sejam associadas a ordens de serviço ativas na fábrica.

---

## 🎨 Design de Interação (UX/UI) - Concluído no Figma

A interface foi projetada seguindo os conceitos de **Mobile-First** e **Design de Alta Fricção Controlada** (onde a interface guia o usuário passo a passo para evitar erros de operação com as mãos ocupadas). Os arquivos de design e justificativas de usabilidade estão localizados em `/docs/design`.

### Diretrizes de UX Industrial Aplicadas:
*   **Thumb Zone (Área do Polegar):** Botões críticos de confirmação e acionamento de leitores posicionados na metade inferior das telas mobile para operação com apenas uma mão.
*   **Código de Cores de Alta Visibilidade:** Uso de contrastes severos para indicar o status imediato do ativo na listagem (Verde: Disponível, Amarelo: Em Uso, Vermelho: Manutenção/Bloqueado).
*   **Interface Baseada em Etapas:** Telas limpas que exibem apenas uma ação por vez (Ex: Tela 1: Identificar Item -> Tela 2: Biometria Controlador -> Tela 3: Biometria Colaborador) minimizando a carga cognitiva do operador.

> 💡 *Os links e capturas de tela dos protótipos navegáveis do Figma podem ser visualizados detalhadamente no arquivo especificado na pasta `/docs/design/README.md`.*

---

## 💻 Desenvolvimento do Core Lógico (Python)

A implementação atual na pasta `/src` foca na construção das regras de negócio puras em Python antes do acoplamento com interfaces visuais ou banco de dados. O motor implementa:

*   Algoritmos de validação de permissões e hierarquia de usuários.
*   Tratamento de exceções para tentativas de leitura biométrica inválidas.
*   Lógica de controle de saldo mínimo para materiais consumíveis.

---

> ⚠️ **Nota de Privacidade e Direitos Autorais:** Este projeto é uma iniciativa estritamente autoral, acadêmica e independente. Todas as regras de negócio, interfaces de usuário no Figma e códigos foram desenvolvidos do zero. Nomes de empresas, dados de funcionários, identidades visuais corporativas ou qualquer conteúdo privado de instituições parceiras foram completamente omitidos ou descaracterizados para estrito cumprimento das leis de propriedade intelectual e sigilo de mercado.
