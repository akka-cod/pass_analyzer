# 🛡️ Pass Analyzer

Analizador de robustez de contraseñas. Herramienta web de un solo archivo HTML que evalúa la fortaleza de contraseñas y passphrases de forma local y privada.

Enlace a la web y software actualizado: https://akka-cod.github.io/pass_analyzer/

## Qué hace

- **Análisis por patrones**: descompone la contraseña en tokens reconocibles (palabras de diccionario, secuencias, patrones de teclado, fechas, leet speak) y estima las combinaciones reales que necesitaría un atacante, en lugar de asumir fuerza bruta pura.
- **Verificación de filtraciones**: consulta la API de [Have I Been Pwned](https://haveibeenpwned.com/) mediante el protocolo de k-anonymity. Solo se envían 5 de los 40 caracteres del hash SHA-1. La contraseña nunca sale del navegador.
- **Tiempo de descifrado**: estimación en 4 escenarios reales (ataque online, bcrypt offline, GPU con hash rápido, clúster de GPUs) basados en benchmarks de Hashcat.
- **Puntuación, composición, patrones detectados y recomendaciones** personalizadas según las debilidades encontradas.

## Privacidad

Todo el análisis se ejecuta localmente en el navegador mediante JavaScript. No hay backend, no se almacenan datos, no se registran contraseñas. La única conexión de red es la verificación HIBP con k-anonymity. No se cargan fuentes ni recursos de terceros (zero tracking).

## Uso

Abrir `index.html` en cualquier navegador. Funciona completamente offline (excepto la verificación de filtraciones, que requiere conexión).

## Nota para despliegues fuera de GitHub Pages

La herramienta incluye la directiva `frame-ancestors 'none'` en la Content Security Policy para prevenir ataques de clickjacking (que la página sea embebida en un iframe malicioso). Sin embargo, según la especificación W3C, esta directiva **es ignorada cuando se declara mediante meta tag HTML** — solo tiene efecto como header HTTP del servidor.

En GitHub Pages esto no es un problema porque el servicio envía automáticamente el header `X-Frame-Options: DENY`, que proporciona la misma protección.

**Si despliegas esta herramienta en un servidor propio**, debes configurar los headers HTTP del servidor para garantizar la protección. Ejemplo para los servidores más comunes:

**Nginx:**
```
add_header X-Frame-Options "DENY" always;
add_header Content-Security-Policy "frame-ancestors 'none'" always;
```

**Apache (.htaccess):**
```
Header always set X-Frame-Options "DENY"
Header always set Content-Security-Policy "frame-ancestors 'none'"
```

**Google Cloud Storage / Firebase Hosting** (en `firebase.json`):
```json
"headers": [{
  "source": "**",
  "headers": [
    { "key": "X-Frame-Options", "value": "DENY" },
    { "key": "Content-Security-Policy", "value": "frame-ancestors 'none'" }
  ]
}]
```

## Referencias

Los criterios de evaluación siguen las directrices de [NIST SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html), [OWASP](https://owasp.org/) y la metodología de descomposición por patrones de [zxcvbn](https://github.com/dropbox/zxcvbn).

## Autoría

Herramienta desarrollada por el equipo de Desarrollo Tecnológico de **Greenpeace España**, con la asistencia de **Claude** (Anthropic).

---

*· Equipo IT ·*
