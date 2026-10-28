# PsiVida 

1. Domínio do Banco de Dados
Sistema de Gestão de Clínica de Psicologia ("PsiVida Consultórios")


2. Contextualização
A PsiVida Consultórios é uma clínica de psicologia com atendimento presencial e online. Sem um SGBD relacional, a empresa enfrentava os seguintes problemas:

Redundância e Inconsistência: Cadastros duplicados de pacientes em fichas de papel e planilhas separadas, gerando confusão de contato e dados desatualizados.

Erros de Agendamento: Ausência de controle unificado entre horários das consultas, psicólogos disponíveis e pacientes, causando choques de horário.

Falta de Histórico Centralizado: Dificuldade para acompanhar a frequência de sessões por paciente e calcular o faturamento individual dos psicólogos.


3. Proposta de Melhoria
Adoção do SGBD MySQL, garantindo:

Registro centralizado de pacientes, psicólogos, convênios/planos e consultas.

Integridade dos dados via chaves primárias (PK) e chaves estrangeiras (FK).

Controle preciso de agendamentos e geração de relatórios operacionais e financeiros.


4. Modelagem Lógica do Banco de Dados
Tabelas e Tipos:

4.1-Paciente

id_paciente (INT, PK, AUTO_INCREMENT)

nome (VARCHAR(100), NOT NULL)

cpf (VARCHAR(14), UNIQUE, NOT NULL)

telefone (VARCHAR(15), NOT NULL)

email (VARCHAR(100))


4.2-Psicologo

id_psicologo (INT, PK, AUTO_INCREMENT)

nome (VARCHAR(100), NOT NULL)

crp (VARCHAR(20), UNIQUE, NOT NULL)

especialidade (VARCHAR(50))

4.3-Convenio

id_convenio (INT, PK, AUTO_INCREMENT)

nome (VARCHAR(50), NOT NULL)

percentual_desconto (DECIMAL(5,2), DEFAULT 0.00)

4.4-Consulta

id_consulta (INT, PK, AUTO_INCREMENT)

data_hora (DATETIME, NOT NULL)

valor (DECIMAL(10,2), NOT NULL)

status (VARCHAR(20))

id_paciente (INT, FK -> paciente.id_paciente)

id_psicologo (INT, FK -> psicologo.id_psicologo)

id_convenio (INT, FK -> convenio.id_convenio)

5-sessao_procedimento (Tabela associativa $N:M$)

id_consulta (INT, PK, FK -> consulta.id_consulta)

id_servico (INT, PK)

observacao (VARCHAR(200))

valor_aplicado (DECIMAL(10,2), NOT NULL)

5. Formas Normais
   
1FN: Atributos atômicos e sem grupos repetidores (telefones, endereços e dados profissionais divididos em colunas individuais).

2FN: A tabela associativa possui chave primária composta e seus atributos não-chave dependem inteiramente de ambas as partes da chave.

3FN: Eliminação de dependências transitivas (atributos de paciente/psicologo pertencem estritamente às suas tabelas originais, não à tabela de consulta).

4FN: Ausência de dependências multivaloradas independentes no modelo.
