# Velitas

App web para grupos de padres de jardín que juntan dinero mensualmente para los cumpleaños de los chicos.

## ¿Qué hace?

- Muestra el estado de pagos del mes por familia
- Calcula automáticamente cuánto debe pagar cada familia según cuántos niños cumplen ese mes
- Las familias cuyos hijos cumplen ese mes quedan exentas del pago (o pagan solo por los cumples ajenos)
- Permite registrar pagos con comprobante adjunto
- Envía notificaciones por mail al inicio de mes y recordatorios a los que no pagaron
- Panel de administración protegido por PIN

## Funcionalidades

- ✅ Registro de pagos por familia con comprobante opcional
- 🎂 Gestión de familias y cumpleaños de los hijos
- 💰 Monto configurable por niño por mes
- 📧 Notificaciones automáticas y manuales por mail (EmailJS)
- ⚠️ Indicador de pagos atrasados del mes anterior
- 🔒 Panel admin con PIN
- 🌙 Modo oscuro automático según preferencia del sistema
- 📱 Diseño mobile-first

## Stack

- HTML / CSS / JavaScript vanilla
- [Firebase Firestore](https://firebase.google.com/) — base de datos en tiempo real
- [EmailJS](https://www.emailjs.com/) — envío de mails sin backend
- Hospedado en [GitHub Pages](https://pages.github.com/)

## Configuración

### Firebase
1. Crear un proyecto en [firebase.google.com](https://firebase.google.com/)
2. Activar Firestore Database en modo de prueba
3. Reemplazar `firebaseConfig` en `index.html` con las credenciales del proyecto

### EmailJS
1. Crear cuenta en [emailjs.com](https://www.emailjs.com/)
2. Conectar un servicio de email (Gmail u Outlook)
3. Crear dos templates:
   - **Inicio de mes**: variables `family_name`, `month_name`, `birthday_count`, `birthday_kids`, `amount`, `exempt_message`
   - **Recordatorio**: variables `family_name`, `birthday_kid`, `amount`
4. Reemplazar `EJS_PUBLIC`, `EJS_SERVICE`, `EJS_TMPL_MONTHLY` y `EJS_TMPL_REMINDER` en `index.html`

## Deploy

El proyecto es un único archivo `index.html`. Para publicarlo en GitHub Pages:

1. Subir `index.html` al repositorio
2. Ir a **Settings → Pages → Branch: main → Save**
3. La app queda disponible en `https://tuusuario.github.io/nombre-repo`
