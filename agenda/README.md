# Mi Semana 📅

Agenda semanal rápida: escribes en una frase lo que tienes que hacer y la app entiende el día y la hora.

- **"mañana a las 10 dentista"** → mañana, 10:00, 🩺
- **"el viernes comprar pan"**, **"pasado mañana llamar a mamá a las 5"**, **"el 20/10 cumple de Ana"**, **"en 3 días…"**, **"la semana que viene…"**
- Desliza **→** para marcar hecha y **←** para pasarla a mañana (o pulsa *Mañana ⏭*)
- Las tareas sin hacer de días anteriores aparecen arriba en *Hoy*, con el botón **Todo a hoy**
- Vista de día y de semana, un color por día, modo oscuro automático y deshacer
- Todo se guarda en el propio móvil y funciona sin internet

## Android
Cada cambio en `agenda/` compila la APK con GitHub Actions y la publica en
[Releases](https://github.com/Eselrawi/ddd/releases/latest). Desde allí descargas `MiSemana.apk`.

### Actualizar sin desinstalar (recomendado)
Si no hay secretos, cada compilación se firma con una clave temporal y para
actualizar hay que desinstalar antes (se pierden las tareas). Para que las
actualizaciones se instalen encima, crea una clave una vez:

```bash
keytool -genkeypair -keystore misemana.jks -alias misemana -keyalg RSA -keysize 2048 -validity 10000
base64 -w0 misemana.jks   # copia el resultado
```

y añádela en *Settings → Secrets and variables → Actions* del repositorio:
`ANDROID_KEYSTORE_BASE64` (el base64) y `ANDROID_KEYSTORE_PASSWORD` (la contraseña;
usa la misma para el almacén y la clave). El alias debe ser `misemana`.

## iPhone
Sirve `agenda/www/` por HTTPS (por ejemplo con GitHub Pages) y ábrela en Safari →
Compartir → *Añadir a pantalla de inicio*. Para una app nativa de iOS:
`npx cap add ios` en un Mac con Xcode y una cuenta de Apple Developer.

## Desarrollo
```bash
cd agenda
npm install
npx cap add android && npx cap sync android
```
El código de la app está en `www/` (HTML, CSS y JS sin dependencias).
`make_icon.py` genera los iconos.
