# Estudo Dirigido --- PATRI-TECH

## PARTE 1 --- Leitura e Interpretação Crítica

### 1. Problema central do sistema

O problema central é a falta de controle, precisão e agilidade no inventário dos bens da Secretaria Municipal de Educação.

### 2. Consequências

1.  Perdas e extravios.\
2.  Inventários demorados.\
3.  Informações desatualizadas.

### 3. Verbos e Adjetivos

**Verbos (funcionais):** identificar, classificar, contabilizar\
**Adjetivos (não funcionais):** ágil, preciso, seguro

### 4. Restrições

Infraestrutura limitada, tempo curto, equipe pequena, orçamento reduzido.

------------------------------------------------------------------------

## PARTE 2 --- Requisitos e Atores

### 5. Priorização MoSCoW

**Must Have:** login seguro, ler RFID, cadastrar bens, atualizar status\
**Should Have:** gerar relatórios, exportar PDF\
**Could Have:** integrações futuras\
**Won't Have:** app mobile offline

### 6. Diferença

**Requisito funcional:** o que o sistema faz\
**Requisito não funcional:** como ele se comporta

### 7. Atores

-   Servidor\
-   Administrador\
-   Diretor\
-   Professor\
-   Leitor RFID

### 8. Fluxo lógico

Login → leitura RFID → identificação → atualização → relatório

### usuário faz login, o sistema valida suas credenciais e libera o acesso ao inventário. Em seguida, as etiquetas dos bens são lidas pelo leitor RFID, que envia o código para o sistema. Esse código é então identificado e associado ao bem correto no banco de dados. Após a identificação, o sistema atualiza automaticamente o status do bem, registrando que ele foi encontrado, sua localização e eventuais divergências. Por fim, todas as informações coletadas durante o processo são reunidas e o sistema gera um relatório completo, mostrando os bens localizados, os ausentes e possíveis inconsistências no inventário.

------------------------------------------------------------------------

## PARTE 3 --- Modelagem e Decisões Técnicas

### 9. Casos de uso

1.  Registrar leitura RFID\

### Usuário inicia o inventário e aciona o leitor RFID. O leitor captura o código da etiqueta e envia ao sistema. O sistema verifica se o código existe no banco. Se existir, identifica o bem correspondente. O sistema atualiza o status do bem (ex.: encontrado, divergente). O registro é salvo no histórico de leituras. O sistema exibe a confirmação para o usuário

2.  Cadastrar bem\

### Usuário acessa o menu de cadastro. Preenche dados do bem (nome, categoria, setor etc.). Associa uma etiqueta RFID ao bem. O sistema valida os campos informados. O sistema salva o novo bem no banco de dados. Exibe mensagem de sucesso e disponibiliza o bem no inventário.

3.  Gerar relatório

### Usuário escolhe o tipo de relatório (inventário, divergências, completo). O sistema busca todos os dados atualizados no banco. Compila informações: bens encontrados, ausentes, divergentes e históricos. Monta o relatório em formato estruturado (tabela/listagem). Gera visualização ou arquivo (ex.: PDF). Disponibiliza para download ou impressão.

### 10. Detalhamento de caso de uso

**Entrada:** O sistema recebe o código eletrônico (EPC) enviado pelo leitor RFID após o usuário aproximar a etiqueta.

**Processamento:** O sistema valida o código recebido, consulta no banco de dados qual bem está associado àquela etiqueta e identifica suas informações. Em seguida, atualiza o status desse bem dentro do inventário atual, marcando-o como encontrado e registrando data, hora e localização da leitura.


**Saída:** O bem aparece imediatamente na lista do inventário como localizado, com status atualizado e sem erros. Se houver divergência ou etiqueta desconhecida, o sistema informa ao usuário

### 11. Framework

Django --- mais completo para painel, autenticação e operações CRUD. O sistema precisa de painel web pronto, login e CRUD, e o Django já traz tudo isso sem complicação. Ele é mais rápido de desenvolver, fácil de aprender e ajuda muito quando o projeto tem prazo curto. Também permite integrar APIs depois usando o Django REST Framework. Sobre desempenho, o Django já entrega o suficiente para um sistema de inventário como o PATRI-TECH.

### 12. Riscos

Retrabalho, baixa performance, complexidade desnecessária.

------------------------------------------------------------------------

## PARTE 4 --- Síntese

### 13. Frase-síntese

Sistema rápido e confiável para inventariar bens públicos via RFID.

### 14. Mini-diagrama de casos de uso

    Servidor → Sistema → Registrar Leitura
    Administrador → Sistema → Cadastro
    Leitor RFID → Sistema → Identificação

### 15. Importância do alinhamento

É importante alinhar os requisitos e a arquitetura antes de começar a codar porque isso evita retrabalho. Quando você sabe exatamente o que o sistema precisa fazer e como ele será estruturado, você desenvolve mais rápido, com menos erros e sem precisar refazer partes do projeto depois. Isso deixa tudo mais organizado e garante que o código realmente atenda ao que o cliente pediu.