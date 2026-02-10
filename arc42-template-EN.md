fecha	título  
Febrero de 2026  

![arc42](./Docs/images/arc42-logo.png) Plantilla  

Acerca de arc42  

arc42, la plantilla para la documentación de software y arquitectura de sistemas.  

Versión de plantilla 9.0-EN (basada en la versión AsciiDoc), febrero de 2026  

Creado, mantenido y © por el Dr. Peter Hruschka, el Dr. Gernot Starke y colaboradores.  
Véase https://arc42.org .  

---

## Introducción y objetivos {#section-introduction-and-goals}

### Descripción general de requisitos {#_requirements_overview}

El Sistema ERP tiene como objetivo integrar y automatizar los principales procesos de negocio de la empresa.  
Esta documentación se centra en el **Módulo de Compras**, encargado de la gestión de productos, proveedores y órdenes de compra.

Requisitos de negocio más importantes del Módulo de Compras:
- Registrar y mantener productos
- Gestionar proveedores
- Crear y consultar órdenes de compra
- Mantener historial de compras
- Integrarse con el sistema contable
- Controlar accesos según roles de usuario

### Objetivos de calidad {#_quality_goals}

- **Usabilidad**: interfaz intuitiva para usuarios administrativos  
- **Seguridad**: autenticación y autorización por roles  
- **Mantenibilidad**: arquitectura modular y documentada  
- **Escalabilidad**: posibilidad de crecimiento futuro  

### Partes interesadas {#_stakeholders}

| Rol/Nombre | Contacto | Expectativas |
|-----------|----------|--------------|
| Administrador de Compras | — | Gestionar productos, proveedores y órdenes |
| Gerencia | — | Consultar reportes y estado del negocio |
| Equipo de TI | — | Facilidad de mantenimiento y despliegue |

---

## Restricciones de arquitectura {#section-architecture-constraints}

- Backend desarrollado en **Java con Spring Boot**
- Base de datos **PostgreSQL**
- Frontend como **SPA en React**
- Comunicación mediante **API REST**
- Uso de **GitHub** para control de versiones y documentación
- Posibilidad de despliegue mediante **contenedores Docker**

---

## Contexto y alcance {#section-context-and-scope}

### Contexto empresarial {#_business_context}

![Diagrama de Contexto](./Docs/images/c1_context.png)

El Sistema ERP interactúa con usuarios internos (Administradores y Gerencia) y con sistemas externos como el sistema contable y los proveedores.

Opcionalmente:  
El ERP envía información contable al sistema externo y órdenes de compra a los proveedores.

### Contexto técnico {#_technical_context}

El sistema utiliza una arquitectura cliente-servidor basada en servicios REST.  
El frontend se comunica con el backend mediante HTTP/JSON y este persiste la información en una base de datos relacional.

---

## Estrategia de solución {#section-solution-strategy}

Se adopta una arquitectura en capas con separación clara entre presentación, lógica de negocio y persistencia, permitiendo mantenibilidad y escalabilidad.

---

## Vista de bloque de construcción {#section-building-block-view}

### Sistema general de caja blanca {#_whitebox_overall_system}

![Diagrama de Contenedores](./Docs/images/c2_containers.png)

#### Motivación

La división en contenedores permite desacoplar responsabilidades y facilitar el mantenimiento.

#### Bloques de construcción contenidos

- Frontend Web
- Backend API
- Base de Datos

#### Interfaces importantes

- API REST entre Frontend y Backend
- Integración con sistema contable externo

### Frontend Web {#_name_black_box_1}

Propósito / Responsabilidad:  
Proporcionar la interfaz gráfica para la gestión del módulo de compras.

Interfaz(es):  
Consume la API REST del backend.

### Backend API {#_name_black_box_2}

Propósito / Responsabilidad:  
Implementar la lógica de negocio del ERP y gestionar la persistencia.

Interfaz(es):  
Expone servicios REST y se comunica con sistemas externos.

---

## Vista de tiempo de ejecución {#section-runtime-view}

### Escenario de ejecución: Registrar un Producto {#_escenario_de_ejecución_1}

![Diagrama de Secuencia](./Docs/images/sequence_register_product.png)

Descripción del escenario:

1. El Administrador de Compras accede al formulario de registro.
2. Ingresa los datos del producto.
3. El Frontend envía la solicitud al Backend.
4. El Backend valida la información.
5. El producto se guarda en la base de datos.
6. El sistema confirma el registro al usuario.

---

## Vista de implementación {#section-deployment-view}

### Infraestructura Nivel 1 {#_infrastructure_level_1}

El sistema se despliega en un servidor utilizando contenedores Docker:

- Contenedor Frontend
- Contenedor Backend
- Contenedor Base de Datos

Motivación:  
Facilitar despliegue, escalabilidad y mantenimiento.

---

## Conceptos transversales {#section-concepts}

### Seguridad {#_concepto_1}

Autenticación y autorización basada en roles.

### Persistencia {#_concepto_2}

Uso de base de datos relacional PostgreSQL.

---

## Decisiones de arquitectura {#section-design-decisions}

- Uso de Spring Boot para acelerar el desarrollo
- Separación frontend/backend
- Uso de REST como mecanismo de comunicación

---

## Requisitos de calidad {#section-quality-scenarios}

### Descripción general de los requisitos de calidad {#_quality_requirements_overview}

El sistema debe ser usable, seguro y fácil de mantener.

### Escenarios de calidad {#_quality_scenarios}

- Un usuario autorizado puede registrar productos sin errores
- El sistema responde en tiempos aceptables bajo carga normal

---

## Riesgos y deudas técnicas {#section-technical-risks}

- Dependencia de sistemas externos
- Falta inicial de pruebas automatizadas

---

## Glosario {#section-glossary}

| Término | Definición |
|--------|------------|
| Producto | Bien adquirido a proveedores |
| Proveedor | Entidad externa que suministra productos |
| Orden de Compra | Documento que formaliza la adquisición |
| ERP | Sistema de Planificación de Recursos Empresariales |
