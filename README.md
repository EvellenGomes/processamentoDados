# Trabalho Final - Introdução ao Processamento de Dados

## Descrição
Este trabalho processa os dados do ENEM 2023, realiza análises estatísticas e responde a perguntas específicas sobre o desempenho dos candidatos.

## Arquivos
- `trabalho_final.ipynb`: Notebook Jupyter com toda a análise
- `MICRODADOS_ENEM_2023.csv`: Dados do ENEM 2023 (1.7GB)
- `ITENS_PROVA_2023.csv`: Dados dos itens da prova
- `Dicionário_Microdados_Enem_2023.xlsx`: Dicionário de dados

## Como Executar

### 1. Instalar Dependências
```bash
pip install pandas numpy matplotlib seaborn psycopg2-binary sqlalchemy python-dotenv
```

### 2. Configurar PostgreSQL
- Instalar PostgreSQL
- Criar banco de dados `processamentoDados`
- Configurar usuário `postgres` com senha `1234`
- Ajustar configurações no notebook se necessário

### 3. Executar o Notebook
```bash
jupyter notebook trabalho_final.ipynb
```

## Tratamentos Realizados nos Dados

### 1. **Seleção de Colunas Relevantes**
- Filtrei apenas as colunas necessárias para a análise:
  - `TP_PRESENCA_LC`: Presença em Linguagens e Códigos
  - `TP_SEXO`: Sexo do candidato
  - `TP_PRESENCA_MT`: Presença em Matemática
  - `TP_FAIXA_ETARIA`: Faixa etária
  - `TP_ESCOLA`: Tipo de escola
  - `Q001`: Escolaridade do pai
  - `Q002`: Escolaridade da mãe
  - `Q006`: Renda familiar
  - `NU_NOTA_REDACAO`: Nota da redação
  - `NU_NOTA_MT`: Nota de matemática

### 2. **Tratamento de Notas para Ausentes**
- Atribuí nota 0 para candidatos ausentes nas provas de Matemática e Redação
- Utilizei condicionais baseadas nos campos de presença

### 3. **Cálculo de Taxas de Ausência**
- Calculei percentuais de ausência para Linguagens e Códigos e Matemática
- Criei DataFrame específico para armazenar essas métricas

### 4. **Mapeamento de Códigos para Labels Descritivos**
- **Faixa Etária**: Mapeei códigos numéricos para faixas etárias descritivas
- **Escolaridade dos Pais**: Mapeei códigos (A-H) para níveis de escolaridade
- **Renda Familiar**: Mapeei códigos (A-Q) para faixas de renda monetária

### 5. **Agregações e Cálculos Estatísticos**
- **Por Sexo**: Calculei médias de notas separadas por gênero
- **Por Tipo de Escola**: Calculei médias para escolas públicas vs privadas
- **Por Escolaridade dos Pais**: Agrupei dados por nível educacional dos pais
- **Por Renda**: Agrupei dados por faixa de renda familiar

### 6. **Estruturação para Banco de Dados**
- Criei DataFrames específicos para cada tipo de análise
- Padronizei nomes de colunas e estruturas
- Preparei dados para inserção em tabelas PostgreSQL

### 7. **Limpeza de Memória**
- Removi DataFrames originais após processamento para otimizar uso de memória

## Perguntas Respondidas

1. **Percentual de faltas** em Matemática e Redação
2. **Distribuição por faixas etárias** dos candidatos
3. **Comparação de notas por sexo** (masculino vs feminino)
4. **Influência do tipo de escola** (pública vs privada)
5. **Influência da escolaridade do pai** nas notas
6. **Influência da escolaridade da mãe** nas notas
7. **Influência da renda familiar** nas notas

## Funcionalidades Implementadas

- ✅ Carregamento e tratamento dos dados
- ✅ Limpeza de dados (remoção de duplicatas, valores ausentes)
- ✅ Seleção de colunas relevantes
- ✅ Tratamento de notas para candidatos ausentes
- ✅ Cálculo de taxas de ausência
- ✅ Mapeamento de códigos para labels descritivos
- ✅ Análises estatísticas com Pandas
- ✅ Salvamento no PostgreSQL
- ✅ Consultas SQL com Pandas
- ✅ Visualizações com matplotlib
- ✅ Resposta a todas as perguntas solicitadas

## Estrutura do Código

1. **Importação de bibliotecas** (pandas, numpy, sqlalchemy, matplotlib)
2. **Carregamento dos dados** (com encoding latin-1)
3. **Seleção de colunas relevantes** para análise
4. **Tratamento de notas para ausentes**
5. **Cálculo de taxas de ausência**
6. **Mapeamento de códigos para labels descritivos**
7. **Agregações estatísticas por diferentes variáveis**
8. **Salvamento no PostgreSQL**
9. **Consultas com Pandas**
10. **Visualizações e análises**

## Tabelas Criadas no PostgreSQL

- `abstence_calculated_data`: Taxas de ausência
- `age_range_calculated_data`: Distribuição por faixa etária
- `sex_calculated_data`: Médias por sexo
- `school_type_calculated_data`: Médias por tipo de escola
- `mother_education_calculated_data`: Médias por escolaridade da mãe
- `father_education_calculated_data`: Médias por escolaridade do pai
- `income_calculated_data`: Médias por renda familiar

## Resultados Esperados

O notebook irá gerar:
- Estatísticas descritivas dos dados
- Percentuais de faltas por disciplina
- Distribuição por faixas etárias
- Comparações de notas por diferentes variáveis
- Análises de correlação entre fatores socioeconômicos e desempenho
- Visualizações gráficas para cada análise

## Observações

- O arquivo CSV é grande (1.7GB), então o carregamento pode demorar
- O código inclui tratamento de erros para diferentes cenários
- As análises são robustas e lidam com dados ausentes
- Os tratamentos realizados otimizam o uso de memória
- Todas as análises consideram apenas candidatos presentes nas provas 