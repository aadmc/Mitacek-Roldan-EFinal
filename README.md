# Mitacek-Roldan-EFinal
Entrega Final Laboratorio de Implementación I MCD - Austral 2026
Corrida 9613 frente al workflow baseline 739

Diferencias con el baseline

| Celda | Baseline 739 | 9613 | Justificación |
|------------------|------------------|------------------|------------------|
| Parámetros | Semilla 102191, experimento 9500 | Semilla 349603, experimento 9613 | Otra semilla primigenia y carpeta propia |
| 85: iteraciones de la BO | 30 | 50 | Más iteraciones para un espacio de 8 hiperparámetros |
| 85: parámetros fijos | Sin `boosting`; fija `min_data_in_leaf= 0`, `lambda_l1= 0`, `lambda_l2= 0` y `min_sum_hessian_in_leaf= 0.001` | `boosting= "gbdt"` explícito; esos cuatro se sacan porque los define la BO | Deja claro el método y evita valores fijos que la BO pisa |
| 86: espacio de la BO | 5 hiperparámetros con rangos genéricos (ver tabla siguiente) | 8 hiperparámetros con rangos acotados | Es el espacio de la 9504, ajustado a dónde caían los óptimos en las BO anteriores |
| 100: modelo final | Transforma 5 hiperparámetros | Transforma los 8, y divide `min_data_in_leaf` por `training_pct` | La BO entrena con el 20% de los CONTINUA y el modelo final con el 100% |
| Envío a Kaggle | Mensaje con envíos y semilla | Agrega `exp=` y `boosting=` | Para identificar cada envío en el leaderboard |

Espacio de búsqueda de la BO:

| Hiperparámetro | Baseline 739 | 9613 |
|------------------------|------------------------|------------------------|
| num_iterations | 4 a 1.024 | 512 a 4.096 |
| learning_rate | 0,0078 a 0,93 | 0,0025 a 0,025 |
| num_leaves | 4 a 2.048 | 64 a 1.024 |
| feature_fraction | 0,05 a 0,90 | 0,05 a 0,50 |
| min_sum_hessian_in_leaf | 0,001 a 1.024 | 0,001 a 1.024 |
| lambda_l1 | fijo en 0 | 0 a 10 |
| lambda_l2 | fijo en 0 | 0 a 150 |
| min_data_in_leaf | fijo en 0 | 16 a 1.024 en la BO (80 a 5.120 en el modelo final) |
