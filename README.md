# Actividad de seguimiento - Simulación 1

|Integrante|correo|usuario github|
|---|---|---|
|Valentina Muñoz Rincón|valentina.munozr1@udea.edu.co|ValenMR|
|Juan Felipe Escobar Rendón|juan.escobar15@udea.edu.co|juanfes517|

## Instrucciones

Antes de empezar a realizar esta actividad haga un **fork** de este repositorio y sobre este trabaje en la solución de las preguntas planteadas en la actividad de simulación. Las respuestas deben ser respondidas en español o si lo prefiere en ingles en el lugar señalado para ello (La palabra **answer** muestra donde).

**Importante**:
* Como la actividad es en las parejas del laboratorio, solo uno de los integrantes tiene que hacer el fork; y sobre repositorio bifurcado que se genera, la modificación se realiza en equipo.
* Como la entrega se debe hacer modificando el archivo READNE, se recomienda que consulte mas sobre el lenguaje **Markdown**. En el repo adjuntan dos cheatsheet ([cheat sheet 1](Markdown_Cheat_Sheet.pdf), [cheatsheet 2](markdown-cheatsheet.pdf)) para consulta rapida.
* Entre mas creativo mejor.

## Homework (Simulation)

This program, [`process-run.py`](process-run.py), allows you to see how process states change as programs run and either use the CPU (e.g., perform an add instruction) or do I/O (e.g., send a request to a disk and wait for it to complete). See the [README](https://github.com/remzi-arpacidusseau/ostep-homework/blob/master/cpu-intro/README.md) for details.

### Questions

1. Run `process-run.py` with the following flags: `-l 5:100,5:100`. What should the CPU utilization be (e.g., the percent of time the CPU is in use?) Why do you know this? Use the `-c` and `-p` flags to see if you were right.
   
   <details>
   <summary>
      <h4>Ey! Look at the answer😱</h4>
   </summary>
   
      ![Image 1](command_line_1.png)

   📌 En mi caso, como se observa en la imagen el comando simula 2 procesos como se pide en el enunciado. Cada uno con 5 instrucciones de CPU y cada instrucción toma el 100%.  

   📊 El uso de CPU se refiere al porcentaje de tiempo que la CPU estuvo ocupada ejecutando las instrucciones. Por lo tanto:
   * **Tiempo total de simulación**: 10 unidades de tiempo
   * **CPU ocupada**: 10 unidades (el 100%)
   * **No hubo I/O**: lo que traduce al 0% de uso de entradas/salidas  
   
   ✅ Debido a que no hubo entradas/salidas, la CPU estuvo ejecutando procesos sin parar durante todo el tiempo. Por eso ambos procesos dan el 100%. 
   </details>
   <br>

2. Now run with these flags: `./process-run.py -l 4:100,1:0`. These flags specify one process with 4 instructions (all to use the CPU), and one that simply issues an I/O and waits for it to be done. How long does it take to complete both processes? Use `-c` and `-p` to find out if you were right. 
   
   <details>
   <summary>
      <h4>Ey! Look at the answer😜</h4>
   </summary>
      
    ![Image 1](command_line_2.png)
      
   📌 Para esta línea de comando, se observa que el PID 0 tiene 4 instrucciones de CPU y el PID 1 tiene 1 instrucción de I/O 
   📊 Ambos procesos tardan en completarse **11 unidades de tiempo**, pues el PID 0 termina en 4 unidades mientras que el PID 1 inicia su I/O en el tiempo 5 y termina en el tiempo 11.

   🤔 **¿Cómo?** Pues el Proceso 0 se ejecuta primero y termina rápidamente, luego el proceso 1 entra en estado de bloqueo porque está esperando la respuesta de la I/O, finalmente en el tiempo 11 se completa el I/O
   y el proceso termina.
   </details>
   <br>

3. Switch the order of the processes: `-l 1:0,4:100`. What happens now? Does switching the order matter? Why? (As always, use `-c` and `-p` to see if you were right)
   
   <details>
   <summary>
      <h4>Ey! Look at the answer😜</h4>
   </summary>
      
      ![Image 1](command_line_3.png)

   ⏱ Según el resultado, al invertir el orden de los procesos, sí hubo un impacto en el rendimiento total ya que se cambió la ejecución de la CPU e I/O.

   ![Image 1](table_comparative_1.png)

   📌 Sucede porque se logra un mejor paralelismo, es decir, el proceso que hace I/O se ejecuta primero, y mientras está bloqueado, el otro proceso puede usar la
   CPU.
   📊A pesar de que los valores absolutos son iguales, los porcentajes aumentaron esto pasa por el solapamiento que se presentó, lo que se traduce como trabajo en
   paralelo.
   
   </details>
   <br>

5. We'll now explore some of the other flags. One important flag is `-S`, which determines how the system reacts when a process issues an I/O. With the flag set to SWITCH ON END, the system will NOT switch to another process while one is doing I/O, instead waiting until the process is completely finished. What happens when you run the following two processes (`-l 1:0,4:100 -c -S SWITCH ON END`), one doing I/O and the other doing CPU work?
   
   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

6. Now, run the same processes, but with the switching behavior set to switch to another process whenever one is WAITING for I/O (`-l 1:0,4:100 -c -S SWITCH ON IO`). What happens now? Use `-c` and `-p` to confirm that you are right.
   
   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

7. One other important behavior is what to do when an I/O completes. With `-I IO RUN LATER`, when an I/O completes, the process that issued it is not necessarily run right away; rather, whatever was running at the time keeps running. What happens when you run this combination of processes? (`./process-run.py -l 3:0,5:100,5:100,5:100 -S SWITCH ON IO -c -p -I IO RUN LATER`) Are system resources being effectively utilized?
   
   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>

8. Now run the same processes, but with `-I IO RUN IMMEDIATE` set, which immediately runs the process that issued the I/O. How does this behavior differ? Why might running a process that just completed an I/O again be a good idea?
   
   <details>
   <summary>Answer</summary>
   Coloque aqui su respuerta
   </details>
   <br>


### Criterios de evaluación
- [x] Despligue de los resultados y analisis claro de los resultados respecto a lo visto en la teoria.
- [x] Creatividad y orden.
