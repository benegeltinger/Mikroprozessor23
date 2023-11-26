## Dokumentation des Digiboard 5 (Daten-RAM und Instruktionsspeicher):
von: Jan Skarbecki, Benedikt Geltinger

## Multiplexer für die zu schreibende Adresse:

Der erste Multiplexer (MUX3) entscheidet ob die zu schreibende Adresse vom Adressbus kommt oder ob sie manuell codiert wurde.
Auf unserem Digiboard ist der oberste Eingang (/ProgrammingEnabled) das Steuersignal für den Multiplexer. 
Das manuelle Codieren erfolgt über die unteren vier Eingänge. Dabei ist der unterte Eingang das 1. Bit.

Der Output, der die zu schreibende Adresse aus dem Multiplexer enthält, geht sowohl an den Daten-RAM als auch an den Instruktions-RAM.

## Multiplexer für die zu schreibenden Daten:

Der zweite Multiplexer (MUX4) entscheidet ob die zu schreibenden Daten aus dem Akkumulator oder aus dem linken Hexadezimal-Codierschalter kommen.
Für den zweiten Multiplexer dient ebenfalls der oberste Eingangn (/ProgrammingEnabled) als das Steuersignal.

Der Output aus dem Multiplexer (MUX4) geht in den ersten 3-State-Bus Driver. 

## Schreiben in den Datenspeicher und den Instruktionsspeicher
Um in die beiden Speicherelemente speichern zu können kommt zum einen aus dem Steuerwerk ein Write-Signal sowie ein manuelles Programming-Write-Signal aus dem zweiten Eingang des Digiboards 5.
Diese beiden Signale kommen auf unserem Digiboard in ein "UND"-Gatter.
Der Output des "UND"-Gatters A01 fließt zum einen negiert in die beiden 3-State-Driver, außerdem fließt das nicht-negierte Signal in den WE-EIngang der beiden RAM-Bausteine.
## Zwei 3-State-Bus Driver 

Der Eingang für den ersten 3-State-Bus Driver stammt aus dem Mutliplexer (MUX4).

Der Eingang für den zweiten 3-State-Bus Driver stammt aus dem rechten Hexadezimal-Codierschalter.
Über den rechten Hexadezimal-Codierschalter können die Befehle für das Instruktionsregister programmiert werden.

Außerdem fließen in die beiden 3-State-Driver das negierte Signal aus dem Logikgatter A01.


## Daten-RAM
Die Speicheradresse wird über die Eingänge A0 bis A3 in den Datenspeicher geladen. In den negierten WE-Eingang fließt das Signal aus dem Logikbaustein A01. 
Das negierte A0 Signal fließt in den negierten OE-Eingang. In den negierten CS-Eingang fließt ein konstantes Low-Signal.
In den Datenspeicher fließen über die D3 bis D0 die tatsächlichen Daten aus dem ersten 3-State-Driver.
Außerdem können über die die Ausgänge D1 bis D3 die Daten die in den jeweiligen Adressen gespeichert sind, ausgelesen werden.



## Instruktions-RAM
Der Instruktor-RAM besitzt ebenfalls die Eingänge A0 bis A3 über die, die Speicheradresse in den Instruktsionsspeicher laden. Außerdem fließt in den negierten WE Eingang das
Signal des Eingangs /ProgrammingWriteNow. In den negierten OE Eingang fließt das negierte Eingangssignal /ProgrammingWriteNow.
In den negierten CS Ausgang fließt ein konstantes Low-Signal.
In den Instruktionsspeicher fließen über die D3 bis D0 Eingänge ebenfalls die Ausgänge aus dem zweiten 3-State-Driver.
Wie bei dem Daten-RAM können über die Ausgänge D1 bis D3 die Instruktionen in den jeweiligen Adressen gespeichert sind, abgelesen werden.



