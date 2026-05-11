# chroma-modulation
ChromaMod es un proyecto experimental que busca crear un sistema de modulación de datos de alta resiliencia utilizando flujos de video con códigos QR multiplexados por color (ChromaQR) como capa de transporte física sobre radioenlaces de larga distancia (PTP).

# El PlanteamientoLa mayoría de las antenas Punto a Punto (PTP) modernas (Ubiquiti, Mimosa, Cambium) están optimizadas para el tráfico de video mediante protocolos de priorización de hardware. Sin embargo, en condiciones de interferencia extrema o clima adverso, el ancho de banda colapsa.

ChromaMod propone una técnica de "Túnel Visual":

Encapsulamiento: Los datos crudos se empaquetan en tramas con cabeceras de sincronía y CRC.Modulación Visual: Estas tramas se convierten en códigos QR de colores (aprovechando los canales R, G y B para triplicar la densidad).

Transporte: El código QR se transmite como un flujo de video H.264 constante a través del radioenlace.

Resiliencia: Aprovechamos la corrección de errores nativa de los QR (Reed-Solomon) sumada a la priorización de video de las antenas para lograr un enlace de datos que no se cae incluso cuando la señal es pésima.

🛠 Utilidad y Casos de UsoTelemetría Crítica: Transmisión de datos de sensores en entornos con altísima interferencia de radio (RF Noise).Stealth Networking (Air-Gap): Túneles de datos ocultos dentro de flujos de video estándar que evaden inspección de paquetes convencional.
Enlaces de Emergencia: Comunicación básica en condiciones climáticas donde la modulación 256-QAM tradicional falla, pero el video (más robusto) aún logra pasar fragmentos.

Modulación DIY: Una plataforma para experimentar con modulación definida por software sin necesidad de hardware de radio costoso (SDR), usando solo cámaras y pantallas.💡 ¿Por qué es una buena idea? (The "Moonshot")Si este proyecto logra una latencia baja (usando FPGAs o procesamiento optimizado en C++), estaríamos creando un Módem Óptico-Digital que corre sobre infraestructura de video. Es una capa de redundancia que hoy no existe: si puedes ver la imagen (aunque sea con ruido), puedes recuperar los datos.

🔧 Arquitectura Técnica PropuestaEncoder: Captura de datos -> Generación de ChromaQR (Python/OpenCV/ChromaQR) -> Stream H.264 (FFmpeg).Protocolo de Trama: [SYNC_BYTE][SEQ_ID][PAYLOAD_LEN][DATA][CRC16].

Hardware: Implementación inicial en Raspberry Pi con miras a una arquitectura final en FPGA para latencia de microsegundos.

Transporte: UDP/RTP Multicast sobre enlaces PTP inalámbricos.

🤝 Colaboración¡Buscamos mentes inquietas! Si te apasiona:📡 Telecomunicaciones y radioenlaces.🐍 Python y procesamiento de imágenes (OpenCV).🧬 Algoritmos de corrección de errores (ECC).🏎️ Optimización de flujos de video (FFmpeg/GStreamer).¡Únete al repositorio y ayúdanos a modular el futuro!
