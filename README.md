# Projeto Power BI — Star Schema para Análise de Professores

## Objetivo

Este projeto é uma implementação-base do desafio de modelagem dimensional proposto no curso.
O desafio pede a criação de um **Star Schema**, tendo **Professor** como objeto de análise,
com uma tabela fato relacionada a professores, cursos e departamentos, além de uma dimensão
de datas criada para suprir a ausência de datas no modelo relacional.

> **Fonte do desafio:** o documento fornecido no curso. O documento informa o objetivo e o
> contexto da modelagem, mas a imagem do diagrama relacional não está disponível no conteúdo
> textual extraído. Por isso, os nomes e relacionamentos deste projeto são uma **proposta-base
> didática**, que deve ser ajustada caso o diagrama original do professor tenha entidades ou
> atributos diferentes.

## Estrutura

```text
projeto_powerbi_star_schema/
├── data/
│   ├── dim_data.csv
│   ├── dim_departamento.csv
│   ├── dim_disciplina.csv
│   ├── dim_curso.csv
│   ├── dim_professor.csv
│   └── fato_oferta_professor.csv
├── dax/
│   └── medidas.dax
├── docs/
│   └── modelo.md
├── sql/
│   └── star_schema.sql
└── README.md
```

## Modelo dimensional

**Fato:** `fato_oferta_professor`

**Dimensões:**
- `dim_professor`
- `dim_curso`
- `dim_disciplina`
- `dim_departamento`
- `dim_data`

### Granularidade da fato

Cada linha representa uma **oferta de disciplina ministrada por um professor em uma determinada data**, associada a um curso e departamento.

## Relacionamentos no Power BI

Configure os relacionamentos como:

- `dim_professor[ProfessorKey]` 1 → * `fato_oferta_professor[ProfessorKey]`
- `dim_curso[CursoKey]` 1 → * `fato_oferta_professor[CursoKey]`
- `dim_disciplina[DisciplinaKey]` 1 → * `fato_oferta_professor[DisciplinaKey]`
- `dim_departamento[DepartamentoKey]` 1 → * `fato_oferta_professor[DepartamentoKey]`
- `dim_data[DataKey]` 1 → * `fato_oferta_professor[DataKey]`

Direção de filtro: **Single**, das dimensões para a fato.

## Como montar no Power BI

1. Abra o Power BI Desktop.
2. Vá em **Obter Dados > Texto/CSV**.
3. Importe os seis arquivos da pasta `data`.
4. Entre em **Exibição de Modelo**.
5. Crie os cinco relacionamentos descritos acima.
6. Marque `dim_data` como tabela de datas, usando a coluna `Data`.
7. Crie as medidas do arquivo `dax/medidas.dax`.
8. Monte uma página de dashboard com:
   - quantidade de professores;
   - quantidade de cursos;
   - quantidade de disciplinas;
   - carga horária total;
   - ofertas por departamento;
   - carga horária por professor;
   - ofertas ao longo do tempo.

## Observação acadêmica

Os dados deste repositório são **fictícios e demonstrativos**. Eles existem para permitir que
o modelo seja carregado e testado no Power BI. Substitua-os pelos dados disponibilizados no
curso, caso existam.

## Entrega

Para publicar:

```bash
git init
git add .
git commit -m "Projeto Power BI - Star Schema"
git branch -M main
git remote add origin SEU_REPOSITORIO
git push -u origin main
```
