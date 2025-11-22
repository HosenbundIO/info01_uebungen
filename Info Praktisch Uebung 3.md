# Aufgabe 1
```python
def to_binary(n):
	# Wenn die Zahl n gleich 0 ist, gibt die Funktion sofort den String "0" zurück. Diese Condition ist auch notwendig da die Funktion nur für Zahlen funktionieren soll, die größer als 0 sind.
	if n == 0:
		return "0"
	
	# Initialisiere einen leeren String in dem alle späteren Values gesammelt werden.
	result = ""
	
	# Solange Zahl n > 0 wenn n gleich 0 gebe Wert (Result) zurück. Mach n % 2 um eine Binärzahl zu erhalten (0 oder 1), da eine Zahl eine gerade Zahl bsp: 6 % 2 immer den Rest 0 hat und eine ungerade Zahl immer (bsp: 7 % 2 = 3 R 1) Rest 1 hat. Der Rest wird vorne an den String gepackt und die Restliche Zahlenfolge dahinter. Im Anschluss wird die Zahl durch 2 mithilfe einer floordivision geteilt wodurch der Zahl zu einem Integer wird also die Kommastelle verschwindet (bsp: 255 // 2 = 127.5 = 127). Jetzt wiederholt sich das ganze bis die Zahl n gleich 0 ist und man eine Zeichenabfolge 0 und 1 hat.
	while n > 0:
		result = str(n % 2) + result
		n = n // 2
		
	return result
```

# Aufgabe 2

```python
"""
Ich lese einen Wert mit input() ein nur wenn ich explizit kein Wert in die Funktion gebe if value == None und in den Parametern der Funktion ist value standardmäßig auf None gestellt (def middle_square(value=None)).

Danach habe ich einen sogenannten Try und Except Block. In denen kann man Code ausführen der höchstwahrscheinlich Errors auslösen kann z.B. wenn du einen String ("abc") versuchst in eine Zahl zu wandeln wird ein ValueError "geworfen", den man dann im Except Block "fangen" kann und bestimmte Operationen durchführen kann oder wie ich hier einfach eine schönere Ausgabe gibt und aus der Funktion mit "return" springt.
Ein User Input ist zunächst immer ein String und damit zwinge ich den Nutzer einen String einzugeben der auch in einen Integer gewandelt werden kann also eine Zahl die aber auch Zweistellig ist, da ich sonst einen weiteren ValueError("invalid_range") werfe und im Except Block mit einem Print eine spezifische Fehlermeldung rausgebe und wieder aus der Funktion "returne".
Als nächstes habe ich eine While-Schleife weil in der Aufgabenbeschreibung explizit While-Schleife erwähnt wurde und nicht for wie es dafür in der Vorlage war und gehe einfach die Operationen wie Text beschrieben durch. Quadriere (funktion square()), Einerstelle entfernen und danach Tausenderstelle abschneiden.
"""
  

def middle_square(value=None):

	if value == None:
		value = input("Startwert: ")

		try:
			value = int(value)
			
			if not 10 <= value < 100:
				raise ValueError("invalid_range")

		except ValueError as e:
			if str(e) == "invalid_range":
				print(f"Ungültige Eingabe: {value} - Gültigen zweistelligen, nichtnegativen Wert eingeben")
			else:
				print(f"Ungültige Eingabe: {value} - Ist keine Zahl")
			return
		else:
			print(f"Eingabe korrekt - Startwert: {value}")

	counter = 0
	while counter < 101:
		print(f"Iteration {counter}: {value}")
		value = square(value)

		value = (value // 10) % 100

		counter += 1


	print("Ende der Folge.")


  

def square(x: int) -> int:
	_sum = 0
	num = 1
	for i in range(1, x + 1):
		_sum = _sum + num
		num = num + 2
	return _sum


  
  

# Beispielaufruf:

"""

for i in range(10, 100):

middle_square(i)

"""

  

middle_square(10)

  

# Beginnt mit einem Zyklus der Länge 1 = 10, 50

# Beginnt mit einem Zyklus der Länge 2 = 24, 57

# Folge enthält einen Zyklus der Länge 1, beginnt aber nicht mit einem Zyklus = 20, 51

# Folge enthält einen Zyklus der Länge 2, beginnt aber nicht mit einem Zyklus = 79

# Gibt es Folgen mit einem Zyklus der Länge größer 2? Nein
```

## Anmerkung zur Aufgabe 3
in der Aufgabe habe ich jeweils 2 Funktionen zur alternierenden Quersumme und divisible_by_29 geschrieben mit dem Hintergrund 2 verschiedene Lösungswege zu haben. Ein Lösungsweg (gekennzeichnet durch Endung int) löst die Aufgabe mit mathematischen Operatoren und Integer Werten während die Funktionen mit Endung str die Werte als Strings behandelt und durch sogenanntes "Slicing" einzelne Werte extrahiert. Somit sind hier 2 verschiedene Lösungswege gegeben. Es sei noch gesagt, dass es selten eine einzige Lösung gibt und gerade das Programmieren eine gewisse Individualität gibt und ihr somit Code euren eigenen Stempel verleihen könnt.
# Aufgabe 3
```python
# Die Funktion nimmt erstmal die anderen Funktionen mit der Zahl n (alternierende_quersumme, iterierte_quersumme und divisible_by_29_str) und bindet diese an eine Variable mit einem Check (bsp: == oder !=) wenn die "Checks" wahr sind wird der Wert True (1) zurückgegeben ansonsten False (0). Diese Checks nutze ich dann als Condition in den If-Statements (bsp: if is_divisible_by_9 == True ?) um ein Print Statement rauszugeben falls das stimmt.
def check_divisibility(n: int) -> None:
    is_divisible_by_11 = alternierende_quersumme(n) == 0
    is_divisible_by_9 = iterierte_quersumme(n) == 9
    is_divisible_by_29 = divisible_by_29_str(n) == 29

    if is_divisible_by_9:
        print(f"{n} ist durch 9 teilbar")
    else:
        print(f"{n} ist nicht durch 9 teilbar")

    if is_divisible_by_11:
        print(f"{n} ist durch 11 teilbar")
    else:
        print(f"{n} ist nicht durch 11 teilbar")
    
    if is_divisible_by_29:
        print(f"{n} ist durch 29 teilbar")
    else:
        print(f"{n} ist nicht durch 29 teilbar")
    
# Das wird jetzt etwas komplizierter, da ich hier die Funktion enumerate() benutze. Enumerate gibt zu jedem Wert der jetzt in dem String x vorkommt ein weiteren Wert (Counter/Iterator) in einem Objekt (könnt ihr erstmal ignorieren) zurück damit dieser Wert in dem String angesprochen werden kann wenn nötig. Die Funktion sum() summiert das ganze. Also negativ = die Summe aus Zahl z für jede Stelle (i) und Zahl (z) in String X wenn die Länge des Strings x - 1 (um von hinten zu beginnen) - i (um die Stellen rückwärts runter zu gehen) % 2 nicht gleich 0 ist - Also eine ungerade Stelle 

# Das gleiche passiert bei positiv nur, dass ich nach den geraden Stellen innerhalb der Zahlenfolge gucke
# Bsp: 58343 Zahl 5 ist an Stelle 0 --> (gerade/postive Zahl), Zahl 8 ist an Stelle 1 --> (ungerade/negative Zahle) 3 ist an Stelle 4 --> gerade. Als Informatiker müsst ihr immer von 0 anfangen zu zählen falls das verwirren sollte
def alternierende_quersumme(x: int) -> int:
    negativ = sum(int(z) for i, z in enumerate(str(x)) if (len(str(x)) - 1 - i) % 2 != 0)
    positiv = sum(int(z) for i, z in enumerate(str(x)) if (len(str(x)) - 1 - i) % 2 == 0)
    return abs(positiv - negativ)
    
# Hier benutze ich eine andere Lösung und zwar indem ich die Zahl von einem Integer (Zahl) in einen String (Zeichenabfolge) wandle. Stellt euch die Datentypen (String, Zahl, Bool, Float (Kommazahl), List etc.) und Variablen wie ein großes Regal (Arbeitsspeicher/RAM) vor. Wenn ihr eine Variable erstellt wird diese Variable in einem Fach des Regals abgelegt und die Reihe des Regals gibt an, welchen Datentypen diese Variable hat. Außerdem benutze ich eine Flipper (Integer) Variable und eine Summe welche die ganzen Werte am Ende summiert. Nun nutze ich eine for-loop um über alle Elemente im String x_str zu iterieren und einen direkten i wert zu haben um den Wert im String anzusprechen. Wir benutzen hier range(start, stop, steps) also wir starten bei länge von x_str (bsp. "856" = 3 - 1 = 2 wegen ab 0 anfagen zu zählen!) und stoppen bei -1 (Stelle 0 ist die letzte Zahl) und gehen -1 Schritte mit jeder iteration also rückwärts. Im Anschluss wandeln wir das Zeichen von x_str in einen Integer um mathematische Operationen durchführen zu können und multiplizieren diesen mit der Flipper Variable (bsp. für Zahl 594 Iteration 0 int(x_str[0]) -> 5 * 1 (Flipper) = 5). Danach wird die Flipper Variable mal -1 genommen um in der nächsten Iteration eine negative Zahl zu erhalten (bsp: für Zahl 594 Iteration 1 int(x_str[1]) -> 9 * -1 (flipper) = -9. Diese Zahlen werden alle in der Variable Summe summiert/gesammelt und am Ende rausgegeben mit dem return keywort. 

def alternierende_quersumme_str(x: int) -> int:
    x_str = str(x)
    flipper = 1
    summe = 0
    for i in range(len(x_str) - 1, -1, -1):
        summe += int(x_str[i]) * flipper
        flipper *= -1
    return summe
    
    
    
# Das war legit 1 zu 1 aus der Aufgabe rausgeschrieben nur in Code. Oben steht bei mir immer divisible_by_29_int(x: int) -> bool: oder sowas änhliches. Das beudetet im Endeffekt nur, dass von x erwartet wird, dass es ein Integer in dem Fall ist und die ganze Funktion ein Bool also Wahr oder Falsch zurückgibt. Muss man in Python nicht unbedingt machen wie in den meisten anderen Programmiersprachen aber hilft einige Werte besser nachvollziehen zu können, da die IDE (VSCode, PyCharm etc.) dann Hinweise gibt.  Aber hier benutze ich den % 29 Operator was die Funktion etwas Sinnbefreit macht, da wir diesen ja nicht direkt nutzen sollen. Deswegen habe ich nochmal unten mit String Operationen gearbeitet.

def divisible_by_29_int(x: int) -> bool:
    while x > 29:
        last_digit = (x % 10) * 3
        rest = x // 10
        x = last_digit + rest
    return bool(x % 29)
    
# Hier wieder dasselbe mit String Slicing. Solange x > 29 wir d x in ein String gewandelt (x_str = str(x)) und wenn die länge von x = 1 dann wird aus der Schleife "gebrochen" und x zurückgegeben. Bei "last" hole ich die letzte Ziffer aus dem String (siehe Beispiel) und den "rest" durch String slicing. Diese Werte werden direkt wieder in Integer gewandelt und mit den Operatoren wie in der Aufgabe genannt verrechnet.

# Beispiel:
# str1 = "beispiel"
# str2 = "1234"
# Operationen am String = string[start, stop, step]
# print(str1[0]) #Output: b --> erste Stelle im String = index 0
# print(str2[0]) #Output: 1
# print(str1[-1]) #Output: l --> letzte Stelle im String = index -1
# print(str1[:-1]) #Output: 123 --> Stoppt vor -1 also letzte Stelle

def divisible_by_29_str(x: int) -> int:
    while x > 29:

        x_str = str(x)
        if len(x_str) == 1:
            break

        last = int(x_str[-1])
        rest = int(x_str[:-1])

        summe = rest + 3 * last
        x = summe
    return x

# iterierte quersumme aus woche 2. Hier ist die for loop ebenfalls in einem One-Liner (quersumme = sum(int(z) for z in str(x))) ist dasselbe wie:
    #    for z in str(x):
     #       quersumme += int(z)
	
 def iterierte_quersumme(x: int) -> int:
    while len(str(x)) > 1:
        quersumme = sum(int(z) for z in str(x))
        x = quersumme
    return x

# Hier eine einfache loop die bis 10000 geht und i in die einzelnen Funktionen steckt um zu testen ob dieser Wert teilbar ist. Wenn ja wird der Wert rausgegeben mit einem Print Statement
def loop_through_10000():
    for i in range(10000):
        if alternierende_quersumme(i) == 0 and iterierte_quersumme(i) == 9 and divisible_by_29_str(i) == 29:
            print(i)

check_divisibility(594)
loop_through_10000()
```