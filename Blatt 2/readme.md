# Aufgabe 1:
(Siehe 01_PDA.png)

# Aufgabe 2:
Der Automat ist nichtdeterministisch, da es im Zustand q3 zwei möglichkeiten für (A, d) gibt.

(Siehe 02_PDA.png)

M = {  
{q0, q1, q2, q3, q4},  
{a, b, c, d},  
{|, A, B},  
(Übergänge in der Aufgabe gegeben),  
q0,  
|,  
{q4}  
}  

Er akzeptiert eine Sprache die mit mindestens einem "a" beginnt, gefolgt von n "b" und n "c" (n > 0), beendet von gleich vielen oder mehr "d" als "a" am Anfang stehen.


# Aufgabe 3:
Die Grammatik generiert eine Sprache die eine If-Verzweigung darstellt. Auf ein If folgt eine condition und ein weiteres Statement (weiteres If oder ein Else), auf ein Else folgt ein statement.  
Da mehrere If Statements ohne Else aufeinanderfolgen können, können aus einer Eingabe mehrere Ableitungsbäume entstehen (Else wird unterschiedlichen If Statements zugeordnet).

# Aufgabe 4:
G = (  
{q2_ε_END, q3_ε_END, q4_ε_END, q1_A_q2, q5_B_q6, q6_B, q2_A_q2, q0},  
{a, c, b},  
P,  
q0)

P = {  
q0       -> a  q1_A_q2  q2_ε_END | c  q3_ε_END | a  q4_ε_END | b  q5_B_q6  
q6_B     -> c  
q5_B_q6  -> b  q5_B_q6 q6_B | c  
q3_ε_END -> c  q3_ε_END | ε  
q1_A_q2  -> b | a  q1_A_q2  q2_A_q2  
q2_A_q2  -> b  
q2_ε_END -> c  q3_ε_END | ε  
q4_ε_END -> b  q5_B_q6 | a  q4_ε_END | ε  
}  

Format der Übergänge: (Startzustand) _ (Kellerzeichen) _ (Endzustand)

(Siehe 04_PDA.png)

Wenn man den Verbindungen im Automaten folgt, sieht man, dass zum Beispiel das Wort "abc" den oberen oder den unteren Weg nehmen kann, und daher zwei verschiedene Ableitungsbäume entstehen können.
Daher ist die Grammatik mehrdeutig.