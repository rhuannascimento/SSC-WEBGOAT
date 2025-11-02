# WebGoat – Relatório (Injection › SQL Injection)

#### Nome: Rhuan Nascimento Ferreira
#### Matrícula: 202176033

Relatório breve das atividades do módulo SQL Injection no WebGoat, incluindo como executar o ambiente, o que foi realizado, payloads utilizados, resultados e recomendações.

## Objetivo
- Preparar e executar o WebGoat localmente.
- Completar as lições do tópico Injection → SQL Injection (intro, advanced e mitigation).


## Ambiente e execução

```bash
# subir os serviços
docker-compose up -d

# acessar no navegador
open http://127.0.0.1:8080/WebGoat
```

## Escopo das lições concluídas e evidências
As capturas de tela de cada etapa estão anexadas à submissão (ver prints). Abaixo, um resumo das lições e payloads demonstrados:

1) SQL Injection (intro)
- DML: atualização de dados com `UPDATE employees SET department = 'Sales' WHERE first_name = 'Tobi' AND last_name = 'Barnett';`
- DDL: alteração de esquema com `ALTER TABLE employees ADD COLUMN phone VARCHAR(20);`
- DCL: concessão de privilégios com `GRANT ALL PRIVILEGES ON TABLE grant_rights TO unauthorized_user;`
- String SQLi: obtenção de todos os usuários com `...' or '1'='1` (fechamento de string + condição sempre verdadeira).
- Numeric SQLi: bypass numérico com `0 or 1 = 1`.
- Confidencialidade: leitura de dados sensíveis usando `Employee Name: ' OR '1'='1` e `TAN: 3SL99A' OR '1'='1`.
- Integridade (query chaining): uso de `; UPDATE ...` para alterar salário (encadeando nova instrução após `;`).
- Disponibilidade: deleção de tabela de logs com `%', DROP TABLE access_log;--` (ou equivalente `'; DROP TABLE access_log;--`).

2) SQL Injection (advanced)
- Login como o usuário Tom por meio de SQLi (formulário vulnerável a injeção). Resultado: “You have successfully completed the assignment”.
- Quiz avançado: todas as questões respondidas corretamente (print com todas em verde).

3) SQL Injection (mitigation)
- Prepared Statements (JDBC): uso de placeholders `?` e `setString` para nome e e‑mail, prevenindo concatenação direta.
- Exercício “Writing safe code”: consulta imune a SQLi usando `prepareStatement("SELECT status FROM users WHERE name=? AND mail=?")` + `setString`.
- Desafio ORDER BY/injection controlada: identificação do IP do `webgoat-prd` → 104.130.219.202.
- Quiz de mitigação: todas as respostas corretas (print em verde).
