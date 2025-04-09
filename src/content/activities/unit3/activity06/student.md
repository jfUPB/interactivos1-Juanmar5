["A"] → Agrega al tiempo [X]

["Botón A"] → Agrega al tiempo [X]

["B"] → En Configuración Disminuye Tiempo [X]

["Botón B"] → En Configuración Disminuye Tiempo [X]

["T"] → En Configuración Resetea Bomba [X]

["Tocar pin"] → En Cuenta Regresiva Resetea Bomba [X]

["Agitar"] → En Configuración Inicia Bomba [X]

["S"] → En Configuración Inicia Bomba [X]

["A", "Botón A", "B", "S"] → En Configuración Aumenta tiempo, aumenta tiempo, disminuye tiempo, inicia cuenta regresiva. [X]

["B", "Botón B", "B", "Agitar"] → En Configuración Disminuye tiempo tres veces y comienza la cuenta regresiva. [X]

["A", "B", "A", "S"] → En Cuenta Regresiva Secuencia correcta para desactivar la bomba. [X]

["Botón A", "Botón B", "Botón A", "Agitar"] → En Cuenta Regresiva Secuencia correcta para desactivar la bomba. [X]

["A", "Botón B", "Botón A", "S"] → En Cuenta Regresiva Secuencia correcta para desactivar la bomba. [] Se debe a un input delay de las señales de p, no parece haber un arreglo más que adaptarse a ese retraso

["Agitar", "T"] → En Configuración Inicia cuenta regresiva y la resetea con T. [X]

["S", "Tocar pin"] → En Configuración Inicia cuenta regresiva y la resetea con T. [X]

["S", "B", "B", "B"] → En Cuenta Regresiva Inicia cuenta regresiva y presiona B varias veces sin desactivar la bomba. [X]

["S", "S", "S", "S"] → En Cuenta Regresiva Inicia cuenta regresiva y sigue enviando S sin hacer nada útil. [X]
