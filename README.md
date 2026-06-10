# 🕯️ Velitas

App web mobile-first para grupos de padres de jardín que juntan dinero mensualmente para los cumpleaños de los chicos.

## ¿Qué hace?

- Muestra el estado de pagos del mes por familia
- Calcula automáticamente cuánto debe pagar cada familia según cuántos niños cumplen ese mes
- Las familias cuyos hijos cumplen ese mes quedan exentas del pago (o pagan solo por los cumples ajenos)
- Permite registrar pagos con comprobante adjunto
- Envía notificaciones por mail al inicio de mes y recordatorios a los que no pagaron
- Panel de administración protegido por PIN
- Instalable como app en el celular (PWA)

## Funcionalidades

- ✅ Registro de pagos por familia con comprobante opcional y límite de monto
- 🎂 Gestión de familias, hijos y cumpleaños (día y mes)
- 💰 Monto configurable por niño por mes
- 👑 Familia recaudadora del mes con alias bancario copiable
- 💸 Box de transferencias para el admin con seguimiento por checkbox
- 📧 Notificaciones automáticas y manuales por mail (EmailJS)
- 📋 Historial del último envío con detalle por familia (✓/✗)
- ⚠️ Indicador de pagos atrasados del mes anterior
- 🔒 Panel admin con PIN
- 🌙 Modo oscuro automático según preferencia del sistema
- 📱 Diseño mobile-first, instalable como PWA

## 📖 Instrucciones de uso

### Para las familias

1. Abrí la URL de la app en el celular (o instalala desde Safari/Chrome)
2. Seleccioná el mes en el selector de arriba
3. Buscá tu familia en la lista — ordenada alfabéticamente
4. Tocá **💳 Pagar** cuando hayas hecho la transferencia
5. Ingresá el monto, adjuntá el comprobante si tenés y confirmá

> El alias bancario al que hay que transferir aparece en el banner azul arriba de todo

**Estados posibles:**
- 🔴 **Pendiente** — no pagó nada
- 🟠 **Parcial** — pagó una parte
- 🟣 **Declarado** — pagó sin comprobante
- 🟢 **Verificado** — pagó con comprobante
- 🎂 **No paga** — su hijo cumple este mes

---

### Para el administrador

#### Configuración inicial (una sola vez)

1. Abrí el **⚙️ Admin** (botón arriba a la derecha) e ingresá el PIN (por defecto: `1234`)
2. Expandí **Familias del grupo** → **+ Agregar familia** y cargá:
   - Nombre de la familia
   - Email (para notificaciones)
   - Alias bancario
   - Hijos con día y mes de cumpleaños
3. Tocá el ícono **👑** al lado de la familia que recauda ese mes

#### Cada mes

1. En **Monto por niño por mes** → elegí el mes y configurá el monto → Guardar
2. Mandá el mail de inicio: **✉️ Notificaciones** → **📨 Enviar mails de inicio de mes**
3. Seguí los pagos en **Pagos registrados**
4. En el box **💸 Transferencias a realizar** ves a quién transferir, cuánto y el alias — tildá el checkbox cuando la hagas
5. Si quedan morosos: **✉️ Notificaciones** → **⏰ Enviar recordatorios**

## Stack

- HTML / CSS / JavaScript vanilla — un solo archivo `index.html`
- [Firebase Firestore](https://firebase.google.com/) — base de datos en tiempo real
- [EmailJS](https://www.emailjs.com/) — envío de mails sin backend
- Hosteado en [GitHub Pages](https://pages.github.com/)

## Archivos del proyecto

```
index.html      → App completa
manifest.json   → Configuración PWA
sw.js           → Service worker
icon-192.png    → Ícono 192px
icon-512.png    → Ícono 512px
```

## Configuración

### Firebase
1. Crear un proyecto en [firebase.google.com](https://firebase.google.com/)
2. Activar Firestore Database en modo de prueba
3. Registrar una app web y reemplazar `firebaseConfig` en `index.html`
4. En Firestore → Reglas, publicar:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /app/data {
      allow read, write: if true;
    }
  }
}
```

### EmailJS
1. Crear cuenta en [emailjs.com](https://www.emailjs.com/)
2. Conectar un servicio de email (Gmail u Outlook)
3. Crear dos templates:
   - **Inicio de mes**: variables `family_name`, `month_name`, `birthday_count`, `birthday_kids`, `amount`, `exempt_message`
   - **Recordatorio**: variables `family_name`, `birthday_kids`, `amount`
4. Reemplazar `EJS_PUBLIC`, `EJS_SERVICE`, `EJS_TMPL_MONTHLY` y `EJS_TMPL_REMINDER` en `index.html`

## Deploy

1. Subir todos los archivos al repositorio
2. Ir a **Settings → Pages → Branch: main → Save**
3. La app queda en `https://tuusuario.github.io/nombre-repo`

### Instalar como PWA
- **iPhone**: Safari → Compartir → Agregar a pantalla de inicio
- **Android**: aparece un banner automático al abrir la URL
