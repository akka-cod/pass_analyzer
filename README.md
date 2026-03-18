# 🛡️ Pass Analyzer

Analizador de robustez de contraseñas. Herramienta web de un solo archivo HTML que evalúa la fortaleza de contraseñas y passphrases de forma local y privada.

### Enlace a la web y software actualizado: https://akka-cod.github.io/pass_analyzer/

## Qué hace

- **Análisis por patrones**: descompone la contraseña en tokens reconocibles (palabras de diccionario, secuencias, patrones de teclado, fechas, leet speak) y estima las combinaciones reales que necesitaría un atacante, en lugar de asumir fuerza bruta pura.
- **Verificación de filtraciones**: consulta la API de [Have I Been Pwned](https://haveibeenpwned.com/) mediante el protocolo de k-anonymity. Solo se envían 5 de los 40 caracteres del hash SHA-1. La contraseña nunca sale del navegador.
- **Tiempo de descifrado**: estimación en 4 escenarios reales (ataque online, bcrypt offline, GPU con hash rápido, clúster de GPUs) basados en benchmarks de Hashcat.
- **Puntuación, composición, patrones detectados y recomendaciones** personalizadas según las debilidades encontradas.

## Privacidad

Todo el análisis se ejecuta localmente en el navegador mediante JavaScript. No hay backend, no se almacenan datos, no se registran contraseñas. La única conexión de red es la verificación HIBP con k-anonymity.

## Uso

Abrir `index.html` en cualquier navegador. Funciona completamente offline (excepto la verificación de filtraciones, que requiere conexión).

## Referencias

Los criterios de evaluación siguen las directrices de [NIST SP 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html), [OWASP](https://owasp.org/) y la metodología de descomposición por patrones de [zxcvbn](https://github.com/dropbox/zxcvbn).

## Autoría

Herramienta desarrollada por el equipo de Desarrollo Tecnológico de **Greenpeace España**, con la asistencia de **Claude** (Anthropic).

---

* · Equipo IT · *
