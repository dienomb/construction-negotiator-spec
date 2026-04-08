# 🏗️ Construction Negotiator

**Asistente de compras para construcción impulsado por IA.**

Un comprador de obra gestiona decenas de conversaciones con proveedores a la vez — comparar ofertas, hacer seguimiento, negociar condiciones — todo repartido entre correos, hojas de cálculo y memoria. Construction Negotiator centraliza ese proceso y negocia de forma autónoma, respetando tus reglas y tu estilo.

---

## 🎯 Qué hace

- **Lanza conversaciones con proveedores** desde un único brief de proyecto
- **Recoge y compara ofertas** aunque lleguen en formatos distintos
- **Negocia de forma autónoma** — contraofertas, cesiones, intercambios de variables — siempre dentro de tus límites
- **Compara proveedores** con scoring transparente por precio, plazo, fiabilidad y condiciones
- **Registra los acuerdos** para que cada negociación alimente la siguiente

---

## 📐 Cómo funciona

El sistema aplica **Negociación por Principios de Harvard** (Fisher & Ury):

| Principio | Aplicación |
|-----------|-----------|
| Separar personas del problema | Los mensajes se centran en datos y necesidades del proyecto, no en presión personal |
| Centrarse en intereses | Identifica lo que el proveedor valora (trabajo estable, pronto pago, volumen) y construye ofertas alrededor de eso |
| Inventar opciones de beneficio mutuo | Propone paquetes de intercambio en lugar de regatear sobre una sola variable |
| Insistir en criterios objetivos | Ancla posiciones en precios de mercado, históricos y datos reales |

---

## 🔄 Flujo de trabajo

```
Proyecto → Proveedores → RFQ → Ofertas → Negociación → Comparación → Acuerdo
```

1. **Configura el proyecto** — qué comprar, cuánto, para cuándo, con qué prioridades
2. **Selecciona proveedores** — con historial, scoring y recomendaciones
3. **Envía peticiones de oferta** — personalizadas por proveedor y relación
4. **Recoge ofertas** — el sistema interpreta formatos distintos y normaliza
5. **Negocia** — contraofertas automáticas, intercambio de variables, respeto de líneas rojas
6. **Compara y decide** — scoring multi-variable, vista lado a lado
7. **Registra el acuerdo** — historial completo para futuras compras

---

## 📄 Especificación

| Documento | Contenido |
|-----------|-----------|
| [Capacidades](docs/01_capabilities.md) | Funcionalidades y áreas de valor |
| [Lógica de negociación](docs/02_negotiation_logic.md) | Principios, BATNA, estrategias de concesión, árbol de decisión |
| [Flujos de trabajo](docs/04_workflows.md) | Detalle de cada etapa del proceso |
| [Integraciones](docs/06_integrations.md) | Gmail, Outlook, Excel y futuras conexiones |

---

## 📋 Cuestionario para socios

El cuestionario captura el conocimiento del experto sobre cómo funciona la compra y la negociación en construcción. Sus respuestas configuran el comportamiento de la plataforma.

🔗 **[Abrir cuestionario](https://dienomb.github.io/construction-negotiator-spec/client/cuestionario_socio.html)**

- ✅ 4 temas — se puede completar en varias sesiones
- 🎙️ Entrada por voz (dictado en español)
- 💾 Guardado automático — continúa donde lo dejaste
- 📤 Las respuestas se envían directamente al repositorio

---

## 🏢 Panorama competitivo

### Negociación y compras con IA

| Producto | Enfoque |
|----------|---------|
| [Pactum](https://pactum.com/) | Agentes de IA autónomos para negociación de proveedores y optimización de costes |
| [ProcurePro](https://procurepro.co/) | Gestión de licitaciones y comparación de ofertas para contratistas principales |
| [Nyfty.ai](https://www.nyfty.ai/) | Automatización de adquisiciones, órdenes de compra y gestión de materiales |
| [ConstructionBids.ai](https://constructionbids.ai/) | Descubrimiento y calificación de licitaciones públicas con IA |

### Plataformas de gestión de obra con módulo de compras

| Producto | Enfoque |
|----------|---------|
| [Procore](https://www.procore.com/) | Gestión integral de construcción con planificación de adquisiciones |
| [Kojo](https://www.usekojo.com/) | Gestión de materiales y proveedores para contratistas MEP |
| [Buildxact](https://www.buildxact.com/) | Estimación y compras digitales para constructores |
| [Briq](https://briq.com/) | Automatización financiera con workflows de gasto y facturas |
| [ConstructConnect](https://www.constructconnect.com/) | Gestión de licitaciones y descubrimiento de proyectos |

### ¿En qué se diferencia Construction Negotiator?

La mayoría de estas herramientas gestionan el **proceso** (enviar RFQs, recoger ofertas, comparar). Construction Negotiator también **negocia** — genera contraofertas, gestiona concesiones y cierra acuerdos de forma autónoma siguiendo las reglas del comprador.

---

## 🛠️ Estado del proyecto

Este repositorio contiene la **especificación de producto** — no hay código de aplicación. Los documentos definen qué debe hacer la plataforma, cómo debe negociar y qué integraciones necesita.

---

*Construction Negotiator — Documento interno — Confidencial*
