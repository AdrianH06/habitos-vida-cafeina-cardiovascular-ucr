# **Asociación entre hábitos de vida, características antropométricas y variables cardiovasculares en adultos jóvenes consumidores de cafeína de la Universidad de Costa Rica**

------------------------------------------------------------------------

## Resumen

Este proyecto estudia si el consumo semanal de cafeína y otros hábitos de vida como las horas de sueño, la actividad física, el consumo de nicotina, así como la edad, el género y demás características antropométricas, se asocian con la presión arterial y la frecuencia cardiaca en adultos jóvenes mediante regresión lineal múltiple.

------------------------------------------------------------------------

## Estructura del repositorio

```         
│
├── README.md
├── LICENSE                    Licencia del código
├── LICENSE-datos              Licencia de los datos y textos
├── Análisis/                  Documentos Quarto con todo el análisis
│   ├── 01_Análisis_Descriptivo.qmd
│   ├── 02_Análisis_pas_imc.qmd
│   ├── 03_Análisis_pad_imc.qmd
│   ├── 04_Análisis_fc_imc.qmd
│   ├── 05_Análisis_pas_peso.qmd
│   ├── 06_Análisis_pad_peso.qmd
│   └── 07_Análisis_fc_peso.qmd
├── Datos/
│   └── Datos_Limpios.rds           Datos en formato RDS
├── Documentos/  
│   ├── Dicionario_Variables.md         Descripción de todas las variables
│   └── Preguntas_Cuestionario.md       Preguntas del cuestionario y su relación con las variables
├── Resultados/                Informes renderizados en PDF
│   ├── 01_Análisis_Descriptivo.pdf
│   ├── 02_Análisis_pas_imc.pdf
│   ├── 03_Análisis_pad_imc.pdf
│   ├── 04_Análisis_fc_imc.pdf
│   ├── 05_Análisis_pas_peso.pdf
│   ├── 06_Análisis_pad_peso.pdf
│   └── 07_Análisis_fc_peso.pdf
├── renv.lock                  Versiones exactas de los paquetes de R
└── habitos-vida-cafeina-cardiovascular-ucr.Rproj
```

------------------------------------------------------------------------

## Datos

| Aspecto | Detalle |
|----|----|
| Participantes | 110 (una fila por participante) |
| Variables | 16 columnas |
| Valores faltantes | Ninguno |
| Población | Estudiantes de distintas facultades de la Universidad de Costa Rica, seleccionados al azar |
| Descripción de las variables | [`Documentos/Dicionario_Variables.md`](Documentos/Dicionario_Variables.md) |
| Preguntas del cuestionario | [`Documentos/Preguntas_Cuestionario.md`](Documentos/Preguntas_Cuestionario.md) |

------------------------------------------------------------------------

## Análisis

Cada documento Quarto en la capeta [`Análisis/`](Análisis/) contiene el análisis completo de un resultado:

| Documento                     | Respuesta | Medida corporal      |
|-------------------------------|-----------|----------------------|
| `01_Análisis_Descriptivo.qmd` | Todas     | Análisis descriptivo |
| `02_Análisis_pas_imc.qmd`     | PAS       | IMC                  |
| `03_Análisis_pad_imc.qmd`     | PAD       | IMC                  |
| `04_Análisis_fc_imc.qmd`      | FC        | IMC                  |
| `05_Análisis_pas_peso.qmd`    | PAS       | Peso y altura        |
| `06_Análisis_pad_peso.qmd`    | PAD       | Peso y altura        |
| `07_Análisis_fc_peso.qmd`     | FC        | Peso y altura        |

------------------------------------------------------------------------

## Cómo reproducir los resultados

### Requisitos

- R 4.6.2
- RStudio
- Quarto 1.11.9

### Pasos

1.  Clonar el repositorio:

    ```         
    git clone https://github.com/AdrianH06/habitos-vida-cafeina-cardiovascular-ucr.git
    ```

2.  Abrir el archivo `habitos-vida-cafeina-cardiovascular-ucr.Rproj`

3.  Restaurar los paquetes con las versiones registradas:

    ``` r
    renv::restore()
    ```

4.  Abrir cualquier documento de la carpeta `Análisis/` y correr el código

Las rutas se construyen con `here::here()`, así que no hace falta ajustarlas.

------------------------------------------------------------------------

## Resultados

Los renders completos están en la carpeta [`Resultados/`](Resultados/).

Resumen de los modelos finales:

| Modelo | Variables finales | R² | R² ajustado |
|----|----|----|----|
| PAS (IMC) | Genero e IMC | 0.4572 | 0.4471 |
| PAD (IMC) | Edad e IMC. | 0.1174 | 0.1009 |
| FC (IMC) | Genero, IMC, Actividad Física e Interacción entre Género e IMC | 0.1151 | 0.08144 |
| PAS (peso) | Genero y Peso | 0.495 | 0.4855 |
| PAD (peso) | Edad y Peso | 0.1575 | 0.1418 |
| FC (peso) | Actividad Física | 0.07067 | 0.06206 |

------------------------------------------------------------------------

## Licencia

- **Código:** licencia MIT. Ver [`LICENSE`](LICENSE).
- **Datos y textos:** licencia [Creative Commons Atribución 4.0 Internacional (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.es). Ver [`LICENSE-datos`](LICENSE-datos).

------------------------------------------------------------------------

## Cómo citar

Si usas los datos, el código o los documentos de este repositorio, cítalo así:

Hidalgo Alfaro, J. A.
y Arroyo Segura, A. I.
(2026).
*Asociación entre hábitos de vida, características antropométricas y variables cardiovasculares en adultos jóvenes consumidores de cafeína*.
GitHub.
<https://github.com/AdrianH06/habitos-vida-cafeina-cardiovascular-ucr>

------------------------------------------------------------------------

## Autoría

- José Adrián Hidalgo Alfaro
- Allison Isabel Arroyo Segura
