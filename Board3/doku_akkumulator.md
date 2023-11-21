# Mikroprozessor Board 3 Akkumulator

von: **Julian Weichselbaumer und Lorenz Scheler**

## Akkumulator

### Multiplexer
![](MultiplexerWahrheitstabelle.jpeg)

Die Wahrheitstabelle ist die für den Multiplexer der auf dem Board gegeben ist.
Hierbei gehen wir davon aus, dass A0 immer null ist. Somit ist nur A1 relevant und wir können uns aussuchen ob wir das Signal von Channel null oder eins nehmen. Ist die Steuerleitung also 1, werden die Daten vom Datenregister übernommen. Ist die Steuerleitung 0, dann wird die Ausgabe der ALU genutzt. 


Wir nutzen unseren gegebenen Multiplexer für den Eingang des 1. Outputs der ALU und von d0, danach bauen wir uns selbst 3 weitere Multiplexer. Eine Besonderheit bei dem gegebenen Multiplexer ist, dass wir nicht einfach a0 nicht berücksichtigen können, weil die Eingangsleitungen zum Steuern des Multiplexers vertauscht sind im Vergleich zur Dokumentation des Boards. Deshalb tauschen wir unsere Eingänge von a0 und a1. Somit ist a1 dann nicht belegt und a0 hat immer die Steuerleitung für die Multiplexer. Hier nimmt der erste selbst gebaute den zweiten Ausgang der ALU und d1. Der zweite selbstgebaute nimmt den dritten Output der ALU und d2. Der letzte selbstgebaute Multiplexer nimmt den vierten Output der ALU und d3. Um Übersicht zu bewahren nehmen wir gelbe Kabel für die Werte vom Datenregister und rote Kabel für die Outputs der ALU


### Schieberegister

Für den Eingang des Schieberegisters nehmen wir die jeweiligen Ausgänge der Multiplexer. Dafür benutzen wir die Eingänge 3,4D mit blauen Kabeln. Eingang 1,4D und 2,4D benötigen wir nicht, da wir vorerst nicht mit serieller Verschiebung arbeiten wollen. 

Die Ausgänge unseres Schieberegisters werden zu den Eingängen P0-P3 der ALU (schwarze Kabel) und sind gleichzeitig auch der Ausgang Richtung Datenbus(mit braunen Kabeln dargestellt).

## ALU 

Die ALU nutzt die Augänge des Schieberegisters als P0-P3, weiterhin werden die Eingänge Q0-Q3 mit den Ausgängen des Datenregisters verbunden.




### Carry Bit
Das Carry Bit der letzten Operation wird in einem JK FlipFlop gespeichert. Dafür muss der $\overline C \overline O$ der ALU in den Input K des JK Flipflops geleitet werden und die Negation von $\overline C \overline O$ in den J Input


### Zero Bit
Alle Eingangsleitungen q0-q3 werden durch ein NOR Gatter geleitet. In einem JK Flipflop werden diese zusammen mit der Clock zum Zero Bit. Dieses ist nur existent, wenn alle Eingangsleitungen 0 sind.

### Negativ Bit

Das Negativ Bit ergibt sich aus q3. Dieses wird mit sich selbst, einer Negation von sich und der Clock in einem JK Flipflop zusammen geführt, welcher das Negativ Bit dann speichert. Dieses Negativ Bit ergibt sich nur wenn, bei der Subtraktion eine größere Zahl von einer kleineren abgezogen wird

## Testen

### Zero Bit Test
Das Zero Bit ist an, wenn alles null ist. Wenn man das Board anschaltet ist, müsste das Zero Bit also ein sein. Dies ist bei uns der Fall.
Weiterhin müsste es leuchten, wenn man z.B. 4-4 rechnet.

### load
Das Load Signal lädt Werte des 



Das Signal haben wir dann in beide Steuerleitungen des Schieberegisters gelegt. Dies benötigen wir, da im Schieberegister bei a0=1 und a1=1 geladen wird. Nun können wir für jeden einzelnen Eingang d0-d3 testen, ob er geladen wird. Dafür brauchen wir die einzelnen d Eingänge, das enable Signal, das load Signal, die Steuerleitungen für den Multiplexer und einen Eingang einer negierten Clock, da der Akkumulator negativ Taktflanken gesteuert ist. Nun testen wir für alle Varianten ab, ob die richtigen Eingänge durchgeladen werden. Hierbei werden load, enable und die Steuerleitungen der Multiplexer angeschaltet und außerdem die jeweilige Kombination der d-Eingänge. Um zu schauen ob es geladen wird, muss nun die Clock betätigt werden. Es muss hierbei darauf geachtet werden, dass die Werte erst durchgeladen werden, wenn die Clock von positiv auf negativ umschaltet. 


### normale Addition 

Bei der normalen Addition, sollen zwei Werte addiert werden, ohne das ein Übertrag entsteht. Beispiel hierfür ist z.B. 1+1 oder 4+3.

Hierfür wird zuerst der erste Wert geladen. Im Anschluss wird ein neuer Wert geschaltet. Die Additon funktioniert dann automatisch ohne das Einschalten einer Clock, weil die ALU immer rechnet. Wenn man das Signal dann wieder lädt muss der Wert der zwei addierten Ziffern ausgegeben werden. 

Beim Beispiel von 4 + 3 kommt der Wert 7 --> funktioniert

### Addition mit Übertrag

Bei der Addition mit Übertrag entsteht ein Wert der zu groß für die Darstellung in 4 Bit ist, z.B: 15 + 1 

Hier sollten dann alle Lampen q ausgehen  

### Subtraktion




