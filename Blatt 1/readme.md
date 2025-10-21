# Aufgabe 1.1:
Der reguläre Ausdruck beschreibt eine Sprache, die entweden aus einem einzelnen "a" oder einem Wort, welches mit einem "a" beginnt, gefolgt von belibig vielen oder keinen "a" oder "b" und wieder mit einem "a" beendet wird.

# Aufgabe 1.2:
## Regex:
(a-z + A-Z) (a-z + A-Z + 0-9 + _ )* (a-z + A-Z + 0-9)

Der erste Teil stellt sicher, dass als erstes ein großer oder kleiner Buchstabe im Wort auftaucht (der Bezeichner), der zweite stellt den Mittelteil eines Wortes dar, er kann aus allen Groß- und Kleinbuchstaben sowie Zahlen und unterstrichen bestehen. In der Mitte des Wortes können kein oder beliebig viele Zeichen aus dieser Gruppe stehen. Der letzte Abschnitt stellt sicher, dass am Ende kein Unterstrich steht, und dass das Wort mindestens 2 Zeichen lang ist.

### Beispiele:
#### VTest_123:
V: (a-z + A-Z)
Test_12: (a-z + A-Z + 0-9 + _ )*
3: (a-z + A-Z + 0-9)


#### b_test_test:
b: (a-z + A-Z)
_test_tes: (a-z + A-Z + 0-9 + _ )*
t: (a-z + A-Z + 0-9)


## DFA:
(Automat siehe 02_DFA.png)

### Beispiele:
Format: (Zustand 1) -- (Symbol) --> (Zustand 2)

#### VTest_123:
A --V--> B
B --T--> B
B --e--> B
B --s--> B
B --t--> B
B --_--> C
C --1--> B
B --2--> B
C --3--> B

#### b_test_test:
A --b--> B
B --_ --> C
C --t--> B
B --e--> B
B --s--> B
B --t--> B
B --_--> C
C --t--> B
B --e--> B
B --s--> B
B --t--> B


## Grammatik:
Klammern zur lesbarkeit hinzugefügt.

({NTA, NTB}, {a-z, A-Z, 0-9}, P, NTA)

P:
(NTA) -> a-z(NTB) | A-Z(NTB)
(NTB) -> a-z(NTB) | A-Z(NTB) | 0-9(NTB) | _(NTB) | a-z | A-Z | 0-9

### Beispiele:
#### VTest:
(Siehe 02_VTest.png)

#### b_test_test:
(Siehe 02_b_test_test)


# Aufgabe 1.3:

## Python:
### Regex:
(((0-9)+ (. + (e(0-9)+)) (0-9)* ) + ((0-9)* . (0-9)+) + ((0-9)+ . (0-9)* )) +
+(((0-9)+ (. + (e(0-9)+)) (0-9)* ) + ((0-9)* . (0-9)+) + ((0-9)+ . (0-9)* )) +
-(((0-9)+ (. + (e(0-9)+)) (0-9)* ) + ((0-9)* . (0-9)+) + ((0-9)+ . (0-9)* ))

Quelle: https://python-lernen.online/hintergrund-informationen/gleitkommazahlen/

### Automat Python:
(Siehe 03_DFA_Python.png)

### Grammatik Python:
Leerzeichen zur lesbarkeit hinzugefügt.

({S, q0, q1, q2, q3, q4, q5, q7, q8, q9, q10, q11, q12}, {0-9}, P, S)

P:
S    -> 0-9 q0 | + q1 | - q3 | . q2
q0   -> . q9 | e q10 | 0-9 q0
q1   -> 0-9 q0
q9   -> 0-9 q11 | 0-9
q10  -> 0-9 q4 | 0-9
q11  -> e q12 | 0-9 q11 | 0-9
q12  -> 0-9 q4 | 0-9
q4   -> 0-9 q4 | 0-9
q3   -> 0-9 q0
q2   -> 0-9 q5 | 0-9
q5   -> 0-9 q5 | 0-9 | e q7
q7   -> 0-9 q8 | 0-9
q8   -> 0-9 q8 | 0-9


## JAVA:
Praktisch gleich zu Python, der einzige Unterschied ist, dass am Ende der Zeile ein "f" für Float bzw. ein "d" für Double

### Regex:
(((0-9)+ (. + (e(0-9)+)) (0-9)* ) + ((0-9)* . (0-9)+) + ((0-9)+ . (0-9)* ))(f+d) +
+(((0-9)+ (. + (e(0-9)+)) (0-9)* ) + ((0-9)* . (0-9)+) + ((0-9)+ . (0-9)* ))(f+d) +
-(((0-9)+ (. + (e(0-9)+)) (0-9)* ) + ((0-9)* . (0-9)+) + ((0-9)+ . (0-9)* ))(f+d)

### Automat:
(Siehe 03_DFA_JAVA.png)


### Grammatik:
Leerzeichen zur lesbarkeit hinzugefügt.

({q0, q1, q2, q3, q4, q5, q7, q8, q9, q10, q11, q12}, {f, d}, P, S)

P:
S     -> 0-9 q0 | + q1 | - q3 | . q2
q0    -> . q9 | e q10 | 0-9 q0
q1    -> 0-9 q0
q9    -> 0-9 q11
q10   -> 0-9 q4
q11   -> e q12 | 0-9 q11 | d q6 | d | f q6 | f 
q12   -> 0-9 q4
q4    -> 0-9 q4 | d q6 | d | f q6 | f 
q3    -> 0-9 q0
q2    -> 0-9 q5
q5    -> 0-9 q5 | e q7 | d q13 | d | f q13 | f 
q7    -> 0-9 q8
q8    -> 0-9 q8 | d q13 | d | f q13 | f



# Aufgabe 1.4:
Der regex ist nicht geeignet, da Großbuchstaben, Zahlen und bestimmte Sonderzeichen wie Bindestriche nicht betrachtet werden (Daher ist auch der Ausdruck a+b+c+d...+z nicht besser). Der Teil nach dem @ ist außerdem nicht geeignet, da nur nach einem einzelnen Zeichen gesucht wird. Die Toplevel-Domain am Ende der Addresse kann zusätzlich ungültig sein, da hier nur nach Zeichen gesucht wird, und nicht nach gültigen TLDs.

Ein besserer Ausdruck ist:
(a-z + A-Z + 0-9)+ @ (a-z + A-Z + 0-9)+ . (.com + .de + ... usw.)
(TLDs nicht vollständig angegeben)

# Aufgabe 1.5:
(Automat siehe 05_DFA.png)


# Aufgabe 1.6:
Die Grammatik beschreibt eine Sprache, die mit einem "a" beginnt, gefolgt von beliebig vielen oder keinen "b" oder "c", wenn ein "d" vorkommt, folgt darauf ein c geht die Sequenz aus "b", "c" oder "d" wieder von vorne los, folgt auf "d" kein "c", wird das Wort mit einem "a" oder "b" beendet.


## Regex:
a(b + c)* d (c (b + c)* d)* (a + b)


## Automat:
(Automat siehe 06_DFA.png)

In diesem Automaten ist der Zustand TRAP dafür da alle ungültigen Eingaben abzufangen und in einem Zustand zu "fangen" der kein Endszustand ist, um so die Vorgaben eines DFA zu erfüllen und alle falschen Eingaben zu ignorieren.
