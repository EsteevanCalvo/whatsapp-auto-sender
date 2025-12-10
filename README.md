# 📱 WhatsApp Auto-Sender para iPhone

> Automatización de mensajes de WhatsApp usando Excel desde OneDrive, diseñado para iPhone con a-Shell

[![Python](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-iOS-lightgrey.svg)](https://www.apple.com/ios/)
[![Status](https://img.shields.io/badge/status-production-success.svg)]()

## Resumen

WhatsApp Auto-Sender es un script de Python que automatiza el envío de mensajes personalizados de WhatsApp en iPhone, integrando datos de Excel almacenados en OneDrive. **Reduce el tiempo de envío en un 85%** comparado con el proceso manual.

Desarrollado como proyecto freelance real para resolver una necesidad de negocio concreta.

### ✨ Características

- ☁️ **Integración con OneDrive**: Descarga automática de archivos Excel desde Microsoft 365
- 📊 **Procesamiento de Excel**: Lee hipervínculos de WhatsApp directamente desde celdas
- 📱 **Nativo para iOS**: Abre WhatsApp con mensajes pre-escritos
- ✅ **Control del Usuario**: Verificación manual antes de enviar cada mensaje
- 🔄 **Siempre Actualizado**: Descarga la última versión del Excel cada vez
- 🛡️ **Seguro y Cumplidor**: Respeta términos de WhatsApp con envío manual

## 📈 Impacto Real

**Caso de Uso:** Cliente necesitaba enviar 50-100 mensajes diarios

| Métrica | Antes (Manual) | Después (Script) | Mejora |
|---------|----------------|------------------|--------|
| Tiempo por 100 mensajes | 2 horas | 20 minutos | **85%** |
| Errores en destinatarios | ~5% | 0% | **100%** |
| Tasa de actualización | Manual | Automática | ∞ |

**ROI:** Inversión recuperada en menos de 1 semana de uso.

## 🚀 Inicio Rápido

### Requisitos Previos

- iPhone con iOS 15+
- [a-Shell](https://apps.apple.com/app/a-shell/id1473805438) instalado
- WhatsApp instalado y configurado
- Cuenta de OneDrive/Microsoft 365 con archivo Excel

### Instalación

**1. Instala a-Shell** desde App Store (gratis)

**2. Instala librerías necesarias** en a-Shell:
```bash
pip install pandas openpyxl requests
```

**3. Descarga el script:**
```bash
# Opción A: Clonar repositorio (si tienes git en a-Shell)
git clone https://github.com/tu-usuario/whatsapp-auto-sender.git

# Opción B: Descargar archivo directamente
# Descarga whatsapp_sender.py y cópialo a a-Shell
```

**4. Configura el script:**
```python
# Edita estas variables en whatsapp_sender.py
ONEDRIVE_LINK = "tu_link_de_onedrive_aqui"
ARCHIVO_LOCAL = "datos.xlsx"
NOMBRE_HOJA_MENSAJES = "Mensajes de Whatsapp"
```

### Uso

**1. Prepara tu Excel** con hipervínculos de WhatsApp (ver [Formato de Excel](#-formato-de-excel))

**2. Sube a OneDrive** y obtén link compartido

**3. Ejecuta en a-Shell:**
```bash
python whatsapp_sender.py
```

**4. Sigue las instrucciones:**
- Script descarga Excel actualizado
- Muestra preview de mensajes
- Abre WhatsApp para cada uno
- Tú verificas y envías
- Presionas ENTER para siguiente

## 📊 Formato de Excel

Tu Excel debe contener hipervínculos de WhatsApp en formato:
```
https://wa.me/[TELÉFONO]?text=[MENSAJE]
```

### Estructura Recomendada

| Columna A | Columna B (Teléfono) | Columna C (Mensaje) | Columna D (Hipervínculo) |
|-----------|---------------------|---------------------|--------------------------|
| Juan Pérez | 573001234567 | Hola Juan,<br>Tu pedido está listo | [Enviar](https://wa.me/573001234567?text=...) |

### Ejemplo de Fórmula Excel

Para generar los hipervínculos automáticamente:

```excel
=SI(
  O(
    MINUSC($H2)="todos los días";
    MINUSC($H2)=MINUSC(TEXTO(HOY();"dddd"))
  );
  "https://wa.me/" & $B2 & "?text=" &
  SUSTITUIR(
    SUSTITUIR(
      SUSTITUIR($C2;" ";"%20");
      CARACTER(10);
      "%0A"
    );
    ","; "%2C"
  );
  "No enviar"
)
```

**Formato de teléfono:** Incluye código de país sin + (ej: 573001234567 para Colombia)

## 🏗️ Arquitectura

```
┌─────────────────┐
│   OneDrive      │
│  Excel con      │
│  hipervínculos  │
└────────┬────────┘
         │ 1. Descarga automática
         ▼
┌─────────────────┐
│  Script Python  │
│   (a-Shell)     │
│                 │
│  • Download     │
│  • Parse Excel  │
│  • Extract URLs │
│  • Convert      │
└────────┬────────┘
         │ 2. Abre URL
         ▼
┌─────────────────┐
│   WhatsApp      │
│   iOS App       │
│                 │
│  Mensaje        │
│  Pre-escrito    │
└─────────────────┘
         │ 3. Usuario envía manualmente
         ▼
    ✅ Enviado
```

## 🔧 Configuración Avanzada

### Variables Configurables

```python
# Link compartido de OneDrive
ONEDRIVE_LINK = ""

# Nombre del archivo temporal local
ARCHIVO_LOCAL = "datos.xlsx"

# Nombre de la hoja que contiene los mensajes
NOMBRE_HOJA_MENSAJES = "Mensajes de Whatsapp"
```

### Personalización

El script puede adaptarse fácilmente:
- **Formato de mensaje**: Modifica fórmulas de Excel
- **Formato de teléfono**: Ajusta función `convertir_url_whatsapp()`
- **Delay entre mensajes**: Cambia valores `time.sleep()`
- **Comportamiento de descarga**: Modifica `descargar_excel_onedrive()`

## 📖 Documentación

- [Manual de Usuario](docs/MANUAL_USUARIO.md) - Guía completa para usuarios finales
- [Configuración de Excel](docs/SETUP_EXCEL.md) - Cómo preparar tu archivo

## 🤝 Contribuir

¡Las contribuciones son bienvenidas! Por favor:

1. Fork el repositorio
2. Crea tu rama (`git checkout -b feature/CaracterísticaIncreíble`)
3. Commit tus cambios (`git commit -m 'Añade CaracterísticaIncreíble'`)
4. Push a la rama (`git push origin feature/CaracterísticaIncreíble`)
5. Abre un Pull Request

Ver [CONTRIBUTING.md](CONTRIBUTING.md) para más detalles.

## 🐛 Problemas Conocidos

- **Limitación iOS**: No se puede automatizar completamente el envío (requiere tap manual)
- **Límites WhatsApp**: Respetar límites (~50-100 mensajes/hora recomendado)
- **Formato Excel**: Solo funciona con hipervínculos, no texto plano según pruebas

## 🗺️ Roadmap

- [ ] Soporte para imágenes/multimedia
- [ ] Integración con Google Sheets
- [ ] Envío programado
- [ ] Reportes de entrega
- [ ] Dashboard web de monitoreo
- [ ] Soporte para WhatsApp Business API

## ⚠️ Disclaimer

Esta herramienta es para uso personal/empresarial legítimo con contactos que esperan comunicación.

**NO usar para:**
- Spam o mensajes no solicitados
- Marketing masivo a listas compradas
- Cualquier actividad que viole términos de WhatsApp

El usuario es responsable del contenido enviado y del cumplimiento de políticas de WhatsApp.

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver archivo [LICENSE](LICENSE) para detalles.

## 👨‍💻 Autor

**José Estevan Calvo Martinez**
- Estudiante de Ingeniería de Software - Uninpahu
- GitHub: [@tu-usuario](https://github.com/EsteevanCalvo)
- LinkedIn: [estevancalvo](https://linkedin.com/in/estevancalvo)
- Email: esteevancalvo2005@gmail.com

## Agradecimientos

- Desarrollado como proyecto freelance real
- Cliente que confió en un estudiante para resolver su problema
- Comunidad de a-Shell por soporte en iOS Python
- @Fundación Universitaria Uninpahu por la formación

## Estadísticas del Proyecto

- **Líneas de Código**: ~500
- **Tiempo de Desarrollo**: 30+ horas
- **Dependencias**: 3 (pandas, openpyxl, requests)
- **Versiones iOS Soportadas**: iOS 15+
- **Estado**: ✅ En producción

## Proyectos Relacionados

- [a-Shell](https://github.com/holzschu/a-shell) - Unix shell para iOS
- [openpyxl](https://openpyxl.readthedocs.io/) - Librería Python para Excel
- [pandas](https://pandas.pydata.org/) - Análisis de datos en Python

## 💬 Soporte

Si encuentras este proyecto útil:
- ⭐ Dale una estrella al repositorio
- 🐛 Reporta bugs
- 💡 Sugiere nuevas características
- 📢 Comparte con otros

Para dudas o soporte:
- Contacta por [email](mailto:esteevancalvo2005@gmail.com)
---

**Hecho con amor por un estudiante para ayudar a empresas**

*Última actualización: Octubre 2024*