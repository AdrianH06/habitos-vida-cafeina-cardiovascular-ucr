# Diccionario de variables

**Proyecto:** Asociación entre hábitos de vida, características antropométricas y variables cardiovasculares en adultos jóvenes consumidores de cafeína de la Universidad de Costa Rica

## Descripción general de la base

**Archivos de datos:** `Datos_Limpios.rds`

El archivo `Datos_Limpios.rds cuenta con 110 filas (una por cada participante) y 16 columnas, que corresponen a variables que se detallan en la siguiente tabla:`

| Número | Variable | Tipo | Descripción |
|----|----|----|----|
| 1 | ID_participante | Identificador (numérico) | Identificador secuencial de cada participante. |
| 2 | Hora | Numérica continua | Hora del día de la medición, en formato decimal de 24 horas (por ejemplo, 16.5 = 4:30 p. m.). |
| 3 | Edad_anios | Numérica discreta | Edad del participante en años cumplidos. |
| 4 | Genero | Categórica nominal (factor) | Género del participante, con 2 niveles: Masculino y Femenino. |
| 5 | Altura_cm | Numérica continua | Estatura del participante en centímetros. |
| 6 | Peso_kg | Numérica continua | Peso corporal en kilogramos. |
| 7 | IMC | Numérica continua | Índice de masa corporal (kg/m²), calculado a partir del peso y la altura. |
| 8 | Diagnostico_previo_hipertension | Categórica binaria (texto) | Si el participante tiene diagnóstico previo de hipertensión (Sí/No). Los 110 participantes respondieron "No", por lo que no se usa en los modelos. |
| 9 | Cafeina_total_mg_semana | Numérica continua | Cafeína total consumida por semana (mg): suma de café, té negro, té verde, cola, bebidas energéticas, suplemento pre-entreno, chocolate y medicamentos con cafeína, calculada a partir de la frecuencia semanal de cada fuente y su contenido de cafeína. |
| 10 | Tiempo_desde_ultima_ingesta_horas | Numérica continua | Horas transcurridas desde la última vez que el participante consumió cafeína. |
| 11 | Consumo_nicotina_frecuencia | Categórica nominal (factor) | Consumo de nicotina recodificado a 3 niveles: No consume nicotina, Nicotina sin combustion y Nicotina con combustion. Originalmente tenía 7 categorías de tipo y frecuencia; tras la recodificación solo distingue el tipo de consumo, no la frecuencia. |
| 12 | Horas_sueno | Numérica continua | Horas de sueño reportadas por el participante. |
| 13 | Godin_Shephard_score | Numérica discreta | Puntaje de actividad física de la escala de Godin-Shephard, calculado a partir de las veces por semana de actividad moderada y vigorosa. A mayor puntaje, mayor actividad física. |
| 14 | PAS_mmHg | Numérica discreta | Presión arterial sistólica (mmHg), medida con esfigmomanómetro digital. |
| 15 | PAD_mmHg | Numérica discreta | Presión arterial diastólica (mmHg), medida con esfigmomanómetro digital. |
| 16 | FC_lpm | Numérica discreta | Frecuencia cardíaca (latidos por minuto), medida con esfigmomanómetro digital. |

### Columnas añadidas a la base durante el análisis

| Número | Variable | Tipo | Descripción |
|----|----|----|----|
| 17 | Tiempo_grupo | Categórica ordinal (factor) | Tiempo desde la última ingesta de cafeína en 3 grupos: "7 h o menos", "7 a 24 h" y "Más de 24 h". Solo se usa en el análisis exploratorio. |
| 18 | t_pas | Numérica continua | Residual estudentizado de cada observación según mod_PAS. Se agrega a Datos para identificar valores extremos en la respuesta, comparándolo con el valor crítico de Bonferroni. |
| 19 | t_pad | Numérica continua | Residual estudentizado de cada observación según mod_PAD. Se agrega a Datos para identificar valores extremos en la respuesta, comparándolo con el valor crítico de Bonferroni. |
| 20 | t_fc | Numérica continua | Residual estudentizado de cada observación según mod_FC. Se agrega a Datos para identificar valores extremos en la respuesta, comparándolo con el valor crítico de Bonferroni. |

## Diccionario de objetos de R

En los nombres de los objetos, `X` representa la variable de respuesta (`PAS`, `PAD` o `FC`); en los objetos auxiliares va en minúscula (`p_pas`, `t_pad`, `dfb_fc`).

| Objeto | Tipo | Qué es |
|----|----|----|
| Datos | data.frame | Base limpia con los factores ya recodificados y las columnas creadas en cada archivo. |
| RUTA | texto | Ruta de `Datos_Limpios.rds`, construida con `here()`. |
| mod_X | lm | Modelo completo inicial: todos los predictores más las interacciones previstas. Usa IMC en los archivos 02 a 04, y altura y peso en los 05 a 07. |
| mod_X_no_in | lm | El mismo modelo sin interacciones; se usa para multicolinealidad (VIF) y linealidad. |
| mod_X_final | lm | Resultado de `step(mod_X, direction = "backward", test = "F")`; guía para escoger el modelo final. |
| mod_X2 | lm | Modelo final elegido tras revisar la salida de `step()`. |
| mod_FC2_no_in | lm | Solo en el 04: `mod_FC2` sin la interacción, para VIF y linealidad. |
| bc_mod_PAD, bc_mod_PAD2 | boxcox | Solo en PAD (03 y 06): perfil de Box-Cox del modelo completo y del modelo final. |
| lambda_optimo_PAD, lambda_optimo_PAD2 | numérico | Solo en PAD: lambda que maximiza la verosimilitud en Box-Cox. |
| mod_PAD_trans, mod_PAD2_trans | lm | Solo en PAD: los modelos anteriores con `log(PAD_mmHg)` como respuesta. |
| n | numérico | Número de observaciones (`nrow(Datos)`). |
| p_x | numérico | Número de parámetros de `mod_X`; entra en los límites de DFFITS y de la distancia de Cook. |
| t_x | numérico | Residuales estudentizados de `mod_X` (también guardados como columna en `Datos`). |
| tc_x | numérico | Valor crítico de Bonferroni para los residuales estudentizados. |
| dfb_x | matriz | DFBETAS de `mod_X`, una columna por coeficiente. |
| predic_num, matriz_cor | texto, matriz | Solo en el 01: nombres de los predictores numéricos y su matriz de correlación de Spearman. |
