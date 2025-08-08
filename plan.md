# Plan de Desarrollo – LeadBoard

## Visión General
Construir **LeadBoard**, una plataforma modular que combina una *Landing inteligente*, un *Sistema de reservas/turnos online* y un *Panel administrativo* para múltiples rubros (peluquerías, talleres, consultorios, gimnasios).

---

## Fases del Proyecto

### 1. Configuración Inicial (Semana 1)
- [ ] Crear repositorio Git.
- [ ] Clonar y configurar entorno de desarrollo.
- [ ] Configurar `.env` basado en `.env.example` con credenciales reales.
- [ ] Levantar entorno local con Docker (`npm run dev:docker`).
- [ ] Aplicar migraciones iniciales (`npx prisma migrate dev`).
- [ ] Ejecutar seeds (`npx prisma db seed`).

---

### 2. Desarrollo de la Landing Inteligente (Semanas 2–3)
- [ ] Implementar diseño responsive con Tailwind CSS 4.
- [ ] Añadir metadatos SEO y Open Graph en `+layout.ts`.
- [ ] Crear formulario de contacto accesible (labels, aria, focus).
- [ ] Validación en cliente y servidor (Zod).
- [ ] Guardar leads en la base de datos con Prisma.
- [ ] Enviar notificación por email (Nodemailer) al admin al recibir un lead.
- [ ] Implementar rate limiting en el formulario.

---

### 3. Sistema de Reservas/Turnos (Semanas 4–5)
- [ ] Modelo `Service`, `Booking`, `Availability`, `Blackout` en Prisma.
- [ ] CRUD inicial de servicios y disponibilidad desde seeds.
- [ ] Generación de slots según reglas de disponibilidad, buffer y feriados.
- [ ] Endpoint `/book/slots` para obtener disponibilidad.
- [ ] Formulario `/book` con selección de servicio, día y hora.
- [ ] Validación transaccional para evitar doble reserva.
- [ ] Confirmación visual y envío de email con archivo `.ics`.
- [ ] Reprogramación y cancelación con enlace seguro y ventana mínima.

---

### 4. Panel Administrativo (/admin) (Semanas 6–7)
- [ ] Proteger con Basic Auth (`ADMIN_USER`/`ADMIN_PASS`).
- [ ] Tab “Leads”: listar, buscar, filtrar, exportar CSV.
- [ ] Tab “Reservas”: listar, filtrar por estado y rango de fechas.
- [ ] CRUD de reservas (crear, editar, cancelar, reprogramar).
- [ ] Gestión de disponibilidad y bloqueos (blackouts).
- [ ] Exportaciones CSV para leads y reservas.

---

### 5. Seguridad y Calidad (Semana 8)
- [ ] Validación de datos con Zod en todas las acciones y endpoints.
- [ ] Protección CSRF de SvelteKit para formularios.
- [ ] Sanitización de strings para CSV y emails.
- [ ] ESLint + Prettier configurados y ejecutados.
- [ ] Tests unitarios con Vitest (`booking.ts`, `rate-limit.ts`).
- [ ] Tests E2E con Playwright para flujo de reserva completo.

---

### 6. Integración y Optimización (Semana 9)
- [ ] Integrar y probar flujo completo: lead → email → reserva → admin.
- [ ] Revisar performance con Lighthouse.
- [ ] Ajustar SEO y accesibilidad según auditoría.
- [ ] Optimizar consultas Prisma y reducir N+1.
- [ ] Revisar Timezone (`TZ` en `.env`) y consistencia horaria.

---

### 7. Deploy y Producción (Semana 10)
- [ ] Configurar base de datos gestionada (Railway, Supabase, Neon, etc.).
- [ ] Configurar SMTP de producción.
- [ ] Deploy en Vercel/Fly.io/Railway.
- [ ] Ejecutar migraciones en producción (`prisma migrate deploy`).
- [ ] Verificar `/health` en hosting.
- [ ] Pruebas finales en entorno productivo.

---

## Estructura de Carpetas
```
/leadboard
  /prisma
    schema.prisma
    seed.ts
  /src
    /lib
      /components
      /server
      /utils
    /routes
      /admin
      /book
      health
  /static
  docker-compose.yml
  Dockerfile
```

---

## Próximos Pasos
1. Configurar entorno local con Docker y Prisma.
2. Implementar Landing con formulario y almacenamiento de leads.
3. Crear sistema de reservas básico y testear generación de slots.
4. Desarrollar panel administrativo y exportaciones.
5. Asegurar seguridad, calidad y pruebas.
6. Preparar deploy y lanzar.
