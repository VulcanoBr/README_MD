# Estrutra de permissionamento RBAC e PBAC (definição de IA)
RBAC (Role-Based Access Control) e PBAC (Policy-Based Access Control) são dois modelos de controle de acesso que regulam quem pode 
acessar recursos em um sistema de TI. Abaixo, cada um desses modelos, sua estrutura e como funcionam.

RBAC (Role-Based Access Control)

O que é:
RBAC é um modelo de controle de acesso no qual as permissões são atribuídas a funções específicas em uma organização, e os usuários 
recebem permissões com base na função ou funções que lhes são atribuídas. Este modelo simplifica a administração de permissões, 
especialmente em organizações grandes.

Como funciona:

    - Definição de funções (roles): A organização define várias funções que correspondem a responsabilidades diferentes. 
    Por exemplo, em uma empresa, pode haver funções como Administrador, Gerente, e Funcionário.
    - Atribuição de permissões às funções: Cada função é associada a um conjunto de permissões que determina o que os 
    usuários naquela função podem fazer. Por exemplo, a função de Administrador pode ter permissões para ler, escrever e 
    apagar dados, enquanto a função de Funcionário pode ter permissões apenas para ler dados.
    - Atribuição de funções aos usuários: Os usuários são atribuídos a uma ou mais funções com base em suas responsabilidades 
    e funções na organização. Um usuário pode ser um Administrador, um Gerente, ou ambos.
    - Acesso baseado em função: Quando um usuário tenta acessar um recurso, o sistema verifica as permissões associadas 
    às funções desse usuário e concede ou nega o acesso com base nessas permissões.

Exemplo prático:

    Função: Administrador
        Permissões: Ler, Escrever, Apagar
    Usuário: João
        Função atribuída: Administrador
        Acesso: João pode ler, escrever e apagar dados.
        
Vantagens do RBAC:

    - Simplicidade: Fácil de implementar e gerenciar, ideal para ambientes com funções e responsabilidades bem definidas.
    - Eficiência: Reduz a necessidade de gerenciamento individual de permissões, otimizando o tempo da equipe de TI.
    - Visão Geral Clara: Permite uma visão clara das permissões de cada usuário, facilitando a auditoria e o controle de acesso.

Desvantagens do RBAC:

    - Falta de Granularidade: Pode ser inflexível para cenários que exigem controle de acesso mais granular, com base em atributos 
    específicos de usuários ou recursos.
    - Dificuldade de Adaptação a Mudanças: Mudanças nas funções ou responsabilidades dos usuários podem exigir a 
    criação de novas funções ou a modificação das existentes, gerando retrabalho.
        
=================================================================================

PBAC (Policy-Based Access Control)

O que é:
PBAC, também conhecido como ABAC (Attribute-Based Access Control), é um modelo de controle de acesso mais dinâmico e 
flexível, onde o acesso a recursos é baseado em políticas definidas usando atributos de usuários, recursos, ações 
e o contexto ambiental.

Como funciona:

    - Definição de atributos: A organização define vários atributos que podem ser utilizados nas políticas de acesso. 
    Esses atributos podem ser relacionados aos usuários (como cargo, departamento), aos recursos (tipo de documento, 
    classificação), às ações (ler, escrever) e ao ambiente (hora do dia, localização).
    - Criação de políticas: As políticas de acesso são formuladas usando combinações desses atributos. Uma política define as 
    condições sob as quais um acesso é permitido ou negado.
    - Avaliação de políticas: Quando um usuário tenta acessar um recurso, o sistema avalia as políticas relevantes, 
    considerando os atributos do usuário, do recurso, da ação solicitada e do contexto ambiental.
    - Decisão de acesso: Com base na avaliação das políticas, o acesso é concedido ou negado. Este modelo permite 
    uma granularidade e flexibilidade muito maiores em comparação com RBAC, pois pode adaptar-se a uma ampla variedade 
    de condições e cenários.

Exemplo prático:

    Atributos do usuário: Cargo = Gerente, Departamento = Vendas
    Atributos do recurso: Tipo = Relatório de Vendas, Classificação = Confidencial
    Política: Os gerentes do departamento de vendas podem acessar relatórios de vendas confidenciais durante o 
              horário de expediente.
    Usuário: Maria
        Cargo: Gerente
        Departamento: Vendas
        Horário de acesso: 10h00
        Recurso: Relatório de Vendas
        Acesso: Maria pode acessar o relatório de vendas porque sua posição, departamento e horário atendem aos 
                critérios definidos na política.
                
Vantagens do PBAC:

    - Granularidade Máxima: Permite um controle de acesso extremamente granular, atendendo às necessidades 
    de cenários complexos com requisitos de segurança específicos.
    - Adaptabilidade: Facilita a adaptação a mudanças nas políticas de acesso, sem a necessidade de modificar 
    funções ou permissões pré-definidas.
    - Automação de Decisões: Automatiza a tomada de decisões de acesso, reduzindo a carga manual sobre a equipe 
    de TI e garantindo consistência nas regras de acesso.

Desvantagens do PBAC:

    - Complexidade: A implementação e o gerenciamento de políticas complexas podem ser mais desafiadores, exigindo 
    conhecimento técnico e expertise em lógica de programação.
    - Desempenho: A avaliação de diversas políticas em tempo real pode impactar o desempenho do sistema, especialmente 
    em cenários com alto volume de solicitações de acesso.

===============================================================================

Comparação entre RBAC e PBAC

    RBAC:
        Simplicidade: Mais fácil de implementar e gerenciar.
        Escalabilidade: Adequado para organizações com estruturas claras de funções.
        Limitação: Menos flexível em situações complexas ou dinâmicas.

    PBAC:
        Flexibilidade: Permite políticas detalhadas e condições complexas.
        Granularidade: Pode adaptar-se a uma ampla variedade de cenários específicos.
        Complexidade: Mais complexo de configurar e manter.

Ambos os modelos são úteis, dependendo das necessidades específicas de controle de acesso da organização. 
Em muitas situações, uma combinação de ambos pode ser empregada para maximizar a segurança e a eficiência operacional.