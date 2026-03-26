# 📋 Metodología del Proyecto

## Visión General

Este documento describe la metodología de trabajo, procesos y mejores prácticas para el desarrollo exitoso del robot humanoide.

---

## 🎯 Filosofía del Proyecto

### Principios Fundamentales

1. **Iteración continua**: Construir → Probar → Aprender → Mejorar
2. **Documentación activa**: Documentar mientras se desarrolla, no después
3. **Modularidad**: Componentes independientes y reutilizables
4. **Pruebas constantes**: Validar temprano y frecuentemente
5. **Seguridad primero**: Nunca comprometer la seguridad por rapidez

---

## 🔄 Ciclo de Desarrollo

### Modelo Iterativo

```
┌─────────────────────────────────────────┐
│                                         │
│    1. Planificar                        │
│    ↓                                    │
│    2. Diseñar                           │
│    ↓                                    │
│    3. Implementar                       │
│    ↓                                    │
│    4. Probar                            │
│    ↓                                    │
│    5. Documentar ──→ Lecciones          │
│    ↓                Aprendidas          │
│    Revisar y Ajustar                    │
│                                         │
└─────────────────────────────────────────┘
```

### Sprints Semanales

**Estructura de una semana tipo**:

1. **Lunes**: Planificación y revisión
   - Revisar sprint anterior
   - Definir objetivos de la semana
   - Identificar recursos necesarios

2. **Martes-Jueves**: Ejecución
   - Desarrollo activo
   - Construcción
   - Pruebas incrementales

3. **Viernes**: Integración y cierre
   - Integrar componentes
   - Pruebas de sistema
   - Documentación de la semana
   - Retrospectiva

---

## 📝 Gestión de Tareas

### Sistema de Priorización

**MoSCoW**:
- **M**ust have (Debe tener): Requisitos críticos
- **S**hould have (Debería tener): Importantes pero no críticos
- **C**ould have (Podría tener): Deseables
- **W**on't have (No tendrá): Fuera de alcance


### Uso de GitHub/Git

**Estructura de branches**:
```
main
├── develop
│   ├── feature/inverse-kinematics
│   ├── feature/sensor-integration
│   └── bugfix/motor-calibration
└── hotfix/emergency-stop
```

**Commits semánticos**:
```bash
git commit -m "feat: Add inverse kinematics solver"
git commit -m "fix: Correct servo angle calculation"
git commit -m "docs: Update control module README"
git commit -m "test: Add unit tests for Joint class"
git commit -m "refactor: Optimize PID controller"
```

**Prefijos**:
- `feat`: Nueva funcionalidad
- `fix`: Corrección de bug
- `docs`: Documentación
- `test`: Pruebas
- `refactor`: Refactorización
- `style`: Formato (no afecta código)
- `chore`: Mantenimiento

---

## 🧪 Estrategia de Pruebas

### Niveles de Prueba

**1. Pruebas Unitarias**
- Funciones y clases individuales
- Framework: `unittest`, `pytest`

```python
# test_joint.py
import unittest
from robot.joint import Joint

class TestJoint(unittest.TestCase):
    def setUp(self):
        self.joint = Joint(name="elbow", min_angle=-90, max_angle=90)
    
    def test_init(self):
        self.assertEqual(self.joint.name, "elbow")
        self.assertEqual(self.joint.current_angle, 0)
    
    def test_move_within_limits(self):
        result = self.joint.move_to(45)
        self.assertTrue(result)
        self.assertEqual(self.joint.current_angle, 45)
    
    def test_move_exceeds_limit(self):
        result = self.joint.move_to(100)
        self.assertFalse(result)
        self.assertEqual(self.joint.current_angle, 0)  # No cambió

if __name__ == '__main__':
    unittest.main()
```

**2. Pruebas de Integración**
- Múltiples componentes trabajando juntos
- Ejemplo: Sensor → Procesamiento → Actuador

**3. Pruebas de Sistema**
- Robot completo
- Escenarios realistas

**4. Pruebas de Aceptación**
- Cumple requisitos del usuario
- Casos de uso completos

### Cobertura de Código

**Objetivo**: ≥80% de cobertura

```bash
# Ejecutar con cobertura
pytest --cov=robot --cov-report=html tests/

# Ver reporte
open htmlcov/index.html
```

### Pruebas de Hardware

**Checklist pre-prueba**:
- [ ] Batería cargada y conectada
- [ ] Todos los cables verificados
- [ ] E-stop accesible y funcional
- [ ] Área de trabajo despejada
- [ ] Logs activados

**Progresión**:
1. **Banco de pruebas**: Componentes fijos
2. **Movimientos limitados**: Articulación por articulación
3. **Secuencias simples**: Movimientos coordinados
4. **Autonomía parcial**: Con supervisión
5. **Autonomía completa**: Sin intervención

---

## 📚 Documentación

### Tipos de Documentación

**1. README por Carpeta**
- Propósito del módulo
- Cómo usar
- Ejemplos
- Dependencias

**2. Docstrings en Código**
```python
def calculate_inverse_kinematics(target_position, robot_model):
    """
    Calcula ángulos articulares para alcanzar posición objetivo.
    
    Utiliza método numérico basado en Jacobiano con damped least squares
    para evitar singularidades.
    
    Args:
        target_position (np.ndarray): Posición 3D objetivo [x, y, z] en metros
        robot_model (RobotModel): Modelo cinemático del robot
        
    Returns:
        np.ndarray: Ángulos articulares en radianes, shape (n_joints,)
        
    Raises:
        IKConvergenceError: Si no converge en max_iterations
        ValueError: Si target_position fuera de workspace
        
    Example:
        >>> robot = RobotModel()
        >>> target = np.array([0.3, 0.2, 0.5])
        >>> angles = calculate_inverse_kinematics(target, robot)
        >>> print(angles)
        array([0.52, -0.78, 1.23, 0.45, -0.32, 0.67])
        
    Note:
        Implementación basada en:
        Buss, S. R. (2004). "Introduction to inverse kinematics with jacobian 
        transpose, pseudoinverse and damped least squares methods."
    """
    # Implementación...
```

**3. Wiki del Proyecto**
- Guías de configuración
- Troubleshooting
- FAQs
- Tutoriales

**4. Diagramas**
- Arquitectura de software
- Diagramas de flujo
- Esquemas eléctricos
- Diagramas UML

**Herramientas**:
- Mermaid: Diagramas en markdown
- draw.io: Diagramas generales
- Fritzing: Esquemas electrónicos
- PlantUML: UML automatizado

---

## 🔍 Code Review

### Proceso

1. **Crear Pull Request**
   - Descripción clara de cambios
   - Referenciar issue relacionado
   - Screenshots/videos si aplica

2. **Auto-revisión**
   - Revisar propios cambios
   - Ejecutar tests localmente
   - Verificar estilo de código

3. **Revisión de Pares** (si hay equipo)
   - Al menos 1 aprobación
   - Comentarios constructivos

4. **Merge**
   - Squash commits si hay muchos pequeños
   - Mensaje descriptivo

### Checklist de Code Review

**Funcionalidad**:
- [ ] ¿Hace lo que se supone?
- [ ] ¿Maneja casos edge?
- [ ] ¿Maneja errores apropiadamente?

**Código**:
- [ ] ¿Es legible?
- [ ] ¿Sigue convenciones (PEP 8 para Python)?
- [ ] ¿Está documentado?
- [ ] ¿DRY (Don't Repeat Yourself)?

**Pruebas**:
- [ ] ¿Hay tests?
- [ ] ¿Tests pasan?
- [ ] ¿Cobertura adecuada?

**Seguridad**:
- [ ] ¿Validación de inputs?
- [ ] ¿Sin credenciales hardcodeadas?
- [ ] ¿Manejo seguro de datos?

---

## 🐛 Debugging y Troubleshooting

### Estrategia de Debugging

**1. Reproducir**
- Aislar el problema
- Crear caso de prueba mínimo

**2. Investigar**
- Revisar logs
- Usar debugger (pdb, gdb)
- Añadir prints estratégicos

**3. Formular hipótesis**
- ¿Qué podría estar causando esto?

**4. Probar**
- Verificar hipótesis
- Iterar

**5. Documentar**
- Registrar solución
- Actualizar docs/troubleshooting

### Herramientas de Debugging

**Python**:
```python
import pdb

def problematic_function(x):
    pdb.set_trace()  # Breakpoint
    result = some_calculation(x)
    return result
```

**ROS**:
```bash
# Logs
rqt_console

# Visualización
rqt_graph  # Grafo de nodos
rqt_plot   # Plotting de topics

# Debugging
rosrun --prefix 'gdb -ex run --args' package_name node_name
```

---

## 📊 Métricas y KPIs

### Métricas de Desarrollo

**Velocity** (Velocidad):
- Tareas completadas por sprint
- Story points (si se usan)

**Burndown Chart**:
```
Tareas
  │
10│●
  │ ●
 8│   ●●
  │     ●●
 6│       ●
  │         ●●
 4│           ●
  │             ●
 2│               ●
  │                 ●
 0└───────────────────────
   L M M J V L M M J V
      Sprint Days
```

### Métricas de Calidad

- **Test coverage**: % código cubierto
- **Bugs encontrados vs. resueltos**
- **Tiempo medio de resolución de bugs**
- **Deuda técnica**: TODOs, FIXMEs

### Métricas del Robot

- **Uptime**: Tiempo operativo sin fallos
- **MTBF** (Mean Time Between Failures)
- **Tasa de éxito de tareas**
- **Eficiencia energética**: Tareas por Wh

---

## 🔐 Seguridad en Desarrollo

### Prácticas Seguras

**1. No commits de secretos**
```bash
# .gitignore
*.key
*.pem
secrets.yaml
config_private.py
```

**2. Usar variables de entorno**
```python
import os

API_KEY = os.environ.get('ROBOT_API_KEY')
if not API_KEY:
    raise ValueError("API_KEY no configurada")
```

**3. Dependencias actualizadas**
```bash
# Verificar vulnerabilidades
pip install safety
safety check

# Actualizar dependencias
pip list --outdated
```

---

## 🤝 Colaboración (si hay equipo)

### Comunicación

**Daily Standup** (5-10 min):
1. ¿Qué hice ayer?
2. ¿Qué haré hoy?
3. ¿Hay bloqueos?

**Reunión Semanal** (30-60 min):
- Revisión de sprint
- Planificación siguiente
- Discusión técnica

**Canales**:
- Slack/Discord: Chat rápido
- GitHub Issues: Tareas y bugs
- Email: Comunicaciones formales
- Video: Reuniones síncronas

### Resolución de Conflictos

**Técnica**:
1. Escuchar todas las perspectivas
2. Identificar el objetivo común
3. Evaluar opciones objetivamente
4. Decidir (por consenso o líder)
5. Documentar decisión (ADR)

---

## 🎓 Aprendizaje Continuo

### Tiempo para Aprender

**Regla 80/20**:
- 80% implementación
- 20% aprendizaje/investigación

### Recursos de Aprendizaje

**Al encontrar problema**:
1. Documentación oficial
2. Stack Overflow
3. Papers académicos (si es avanzado)
4. Tutoriales/blogs
5. Preguntar en comunidades

### Registro de Aprendizajes

**TIL (Today I Learned)**:
```markdown
## 2026-02-27

### Problema
Servomotores vibrando en posición estacionaria.

### Aprendido
- Zona muerta (deadband) en PID ayuda a estabilizar
- Valor típico: ±1-2° para servos
- Implementación:
  ```python
  if abs(error) < DEADBAND:
      output = 0
  ```

### Referencias
- https://example.com/pid-tuning-guide
```

---

## 🔄 Mejora Continua

### Retrospectivas

**Formato Start-Stop-Continue**:

**Start** (Empezar a hacer):
- Más pruebas de integración temprana
- Daily logs de progreso

**Stop** (Dejar de hacer):
- Procrastinar documentación
- Saltarse validación de seguridad

**Continue** (Continuar haciendo):
- Code reviews exhaustivos
- Refactoring regular

### Kaizen (Mejora Incremental)

- Pequeñas mejoras constantes
- Eliminar desperdicio
- Automatizar tareas repetitivas

**Ejemplo**:
```bash
# Script para automatizar setup diario
#!/bin/bash
# daily_setup.sh

echo "Iniciando entorno de desarrollo..."

# Activar entorno virtual
source venv/bin/activate

# Actualizar repositorio
git pull origin develop

# Verificar dependencias
pip install -r requirements.txt

# Ejecutar tests rápidos
pytest tests/unit/ -v

echo "✓ Entorno listo!"
```

---

## 📅 Cadencia de Actividades

### Diario
- Commit de cambios
- Logging de progreso
- Breve revisión de objetivos

### Semanal
- Retrospectiva de sprint
- Planificación siguiente sprint
- Actualización de documentación

### Mensual
- Revisión de objetivos de fase
- Ajuste de cronograma si necesario
- Evaluación de métricas

### Por Fase
- Revisión completa de fase
- Documentación exhaustiva
- Demo de funcionalidades
- Go/No-Go para siguiente fase

---

## 🎯 Definición de "Hecho" (Done)

Una tarea se considera completada cuando:

- [ ] **Código escrito** y funciona
- [ ] **Tests** implementados y pasando
- [ ] **Documentado** (código y README)
- [ ] **Code review** aprobado (si aplica)
- [ ] **Integrado** con sistema principal
- [ ] **Probado** en hardware (si aplica)
- [ ] **Sin regressions** (tests anteriores siguen pasando)

---

## 🛠️ Automatización

### CI/CD (Continuous Integration/Deployment)

**GitHub Actions ejemplo**:
```yaml
# .github/workflows/test.yml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: 3.9
    
    - name: Install dependencies
      run: |
        pip install -r requirements.txt
    
    - name: Run tests
      run: |
        pytest tests/ --cov=robot
    
    - name: Upload coverage
      uses: codecov/codecov-action@v2
```

### Pre-commit Hooks

```bash
# .git/hooks/pre-commit
#!/bin/bash

echo "Ejecutando tests antes de commit..."
pytest tests/unit/ -q

if [ $? -ne 0 ]; then
    echo "❌ Tests fallaron. Commit cancelado."
    exit 1
fi

echo "✓ Tests OK. Procediendo con commit."
```

---

## 📖 Plantillas

### Plantilla de README

```markdown
# Nombre del Módulo

## Propósito
Breve descripción (1-2 líneas)

## Contenido
```
carpeta/
├── file1.py
└── file2.py
```

## Instalación
```bash
pip install requirements
```

## Uso
```python
from module import function
result = function(param)
```

## API
### function(param)
Descripción de la función

**Params**:
- `param` (type): Descripción

**Returns**:
- type: Descripción

## Ejemplos
...

## Tests
```bash
pytest tests/test_module.py
```

## Referencias
- Link 1
- Link 2
```

---

## 🏆 Cultura de Excelencia

### Principios

1. **Calidad sobre cantidad**: Mejor poco bien hecho
2. **Responsabilidad**: Ownership de tu código
3. **Curiosidad**: Siempre pregunta "¿por qué?"
4. **Humildad**: Acepta feedback, aprende continuamente
5. **Colaboración**: Comparte conocimiento

### Anti-patrones a Evitar

❌ **Código espagueti**: Sin estructura clara
❌ **Comentarios innecesarios**: Código debe ser autoexplicativo
❌ **Optimización prematura**: Primero funciona, luego optimiza
❌ **Not Invented Here**: Usa librerías existentes cuando tiene sentido
❌ **Ignorar warnings**: Atiéndelos temprano

---

**Última actualización**: Febrero 2026

**Nota**: Esta metodología es adaptable. Ajustar según necesidades del proyecto y lecciones aprendidas.
