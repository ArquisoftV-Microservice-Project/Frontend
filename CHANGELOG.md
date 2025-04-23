# 📄 CHANGELOG

## [1.0.1] - 2025-04-23

### 🎉 Added
- Feature de release por commit arreglada
---

## [1.0.0] - 2025-04-23

### 🎉 Added
- Estructura base del frontend con Vue.js para una aplicación distribuida tipo TODO.
- Dockerfile para construir la imagen de producción.
- GitHub Actions workflow (`build.yml`) para CI/CD:
  - Autenticación con Google Cloud mediante Service Account.
  - Instalación de SDK de GCP y configuración de Artifact Registry.
  - Build de imagen Docker con etiquetas automáticas (`latest` y por timestamp).
  - Push a GCP Artifact Registry.
  - Actualización del deployment `frontend` en GKE si existe.
- Configuración de variables y secretos necesarios para el despliegue automatizado.

### 🛠️ Infraestructura
- Integración completa con GKE usando `kubectl` y autenticación automática.
- Rama `main` protegida para evitar commits directos y forzar PRs.

---

