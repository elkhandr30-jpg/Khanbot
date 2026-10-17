# Khan Bot

Servicio de accesibilidad para inDrive (conductor). Reglas:
- Cliente paga >= nuestro precio  -> acepta el precio del cliente.
- Cliente paga menos              -> escribe NUESTRO precio con el lapiz (calculado, o tarifa minima si el viaje no llega a la base).
- Omite si: recogida > maximo, recorrido > maximo, o viaje con paradas (si no las aceptas).
Nuestro precio = km del viaje x precio/km, redondeado, con piso en el precio minimo.

## Instalar
Android Studio: abrir la carpeta > Build > Build APK(s) (o Run con el telefono por USB).
Si la sincronizacion falla por Gradle, ya incluye gradle/wrapper/gradle-wrapper.properties (Gradle 8.7).
Sin PC: subir la carpeta a GitHub y bajar el APK desde Actions.

## Primer uso
1. Abrir Khan Bot > Abrir ajustes de accesibilidad > Khan Bot > activar.
   (Android 13+: Ajustes > Apps > Khan Bot > menu ... > Permitir ajustes restringidos.)
   Xiaomi: inicio automatico ON y bateria sin restricciones.
2. Aparece el boton flotante OFF/ON: toca = encender/apagar, arrastra = mover, mantener pulsado = menu.
3. Dejar "Modo prueba" ACTIVADO: solo avisa y registra. Revisar que lea bien km y precio.

## Calibrar el lapiz (importante)
Con una solicitud de inDrive abierta:
1. Mantener pulsado el boton flotante > "Probar lapiz (sin enviar)".
   Abre el lapiz, escribe el precio minimo y NO confirma. Si funciona, listo.
2. Si dice "No encontre el lapiz": menu > "Calibrar lapiz" y tocar el lapiz en pantalla (guarda la posicion).
3. Si no aparece el campo o no escribe: en la app, "Compartir diagnostico del lapiz" y "Compartir volcado completo"
   (menu > Volcar pantalla) y enviarlos para ajustar.
4. Cuando "Probar lapiz" funcione, apagar "Modo prueba" y encender el bot.

## Novedades v2.4
- El km del viaje (A->B) NO es texto en inDrive: esta en la burbuja del mapa. Khan Bot toma una captura, recorta la burbuja
  y la lee con OCR (ML Kit, sin internet). Burbuja azul = recogida, verde/lima = viaje. Necesita Android 11+.
  Tras instalar, desactiva y vuelve a activar el servicio de accesibilidad (permiso nuevo: captura de pantalla).
- Precio = km del viaje x precio por km (el minimo solo si el calculo queda bajo la base).
- En la lista de solicitudes elige solo las de recogida dentro de tu rango (la mas cercana primero) y las abre.
  Ignora las ya vistas por 3 min y se pausa 20 s tras enviar/aceptar una oferta.
- Si el OCR falla, "diagnostico_lapiz.txt" guarda una linea "OCR burbujas: ..." para ajustar.
