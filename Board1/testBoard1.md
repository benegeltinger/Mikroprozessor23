## Dokumentation Board 1

von: Luca Pinnekamp, Carolin Steger

#### CircutVerse
https://circuitverse.cs.hm.edu/users/234/projects/praktikum-4-b57bb048-e05d-476c-903f-f31e026de357 

https://circuitverse.cs.hm.edu/users/283/projects/praktikum-5-a3f33a6e-06d3-4b71-b812-1ffe298df51c 

Für den Instruktionsregistee haben wir das SRG4 benutzt. Bei dem Instruktionsdekoder haben wir die UND-Gatter A1 - A8 aus dem Schaltplan übernommen. Für die Sprungbefehle haben wir einen Demutiplexer mit volgender belegung genommen.

| 1   | 0   | A1  | A0  | jmp | brz | brc | brn |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | 0   | 0   | 0   | 1   | 0   | 0   | 0   |
| 1   | 0   | 0   | 1   | 0   | 1   | 0   | 0   |
| 1   | 0   | 1   | 0   | 0   | 0   | 1   | 0   |
| 1   | 0   | 1   | 1   | 0   | 0   | 0   | 1   |


