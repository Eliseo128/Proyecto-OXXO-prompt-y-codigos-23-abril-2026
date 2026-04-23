¡Excelente elección! Como desarrollador de software y guía técnico, he diseñado este plan de trabajo estructurado bajo una arquitectura limpia y una metodología de "Agentes de Desarrollo" para que los estudiantes no solo programen, sino que entiendan el flujo profesional.

---

## 🛠️ Fase 1: Entorno y Configuración (Antigravity Flow)

Para este proyecto, utilizaremos la metodología **Antigravity**, que se centra en elevar el desarrollo por encima de las complicaciones innecesarias, priorizando la estructura y la reactividad.

### 1. Estructura de Directorios
Desde tu terminal:
```bash
mkdir xflutternava1777
cd xflutternava1777
flutter create crudoxxo
cd crudoxxo
```

### 2. Configuración de Firebase (Consola)
1. Ve a [Firebase Console](https://console.firebase.google.com/).
2. Crea un proyecto llamado `crudoxxo`.
3. En el menú lateral, ve a **Firestore Database** y haz clic en **Crear base de datos**.
4. Crea la colección **"empleados"** y agrega un documento de prueba con:
   * `nombre`: String
   * `edad`: Number
   * `puesto`: String

### 3. Dependencias (Archivo `pubspec.yaml`)
Modifica tu archivo `pubspec.yaml` agregando estas librerías bajo `dependencies`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^3.0.0      # Núcleo de Firebase
  cloud_firestore: ^5.0.0    # Base de datos Firestore
  google_fonts: ^6.0.0       # Estética visual
```
*Ejecuta `flutter pub get` en la terminal para instalar.*

---

## 🤖 Fase 2: Metodología de Agentes y Roles

Para que la práctica sea guiada, dividiremos el desarrollo en **Agentes Lógicos**:

| Agente | Rol | Skill (Habilidad) |
| :--- | :--- | :--- |
| **Architect** | Definir Modelos | Transformar JSON de Firebase a objetos Dart. |
| **Data Master** | CRUD Services | Conexión directa con Firestore (Add, Get, Update, Delete). |
| **UI Designer** | Vista y Estética | Crear interfaces con colores atractivos y feedback visual. |

---

## 📂 Estructura del Proyecto (Clean Folder Structure)

```text
crudoxxo/
├── lib/
│   ├── agents/
│   │   ├── data_master.dart   (Lógica Firebase)
│   │   └── architect.dart      (Modelo de datos)
│   ├── ui/
│   │   ├── colors.dart         (Paleta de colores)
│   │   └── home_screen.dart    (Interfaz CRUD)
│   └── main.dart               (Punto de entrada)
```

---

## 💻 Código Funcional (Implementación)

### 1. El Arquitecto (Modelo de Datos)
`lib/agents/architect.dart`
```dart
class Empleado {
  String id;
  String nombre;
  int edad;
  String puesto;

  Empleado({required this.id, required this.nombre, required this.edad, required this.puesto});

  // Convertir de Firestore a Objeto
  factory Empleado.fromFirestore(Map<String, dynamic> data, String id) {
    return Empleado(
      id: id,
      nombre: data['nombre'] ?? '',
      edad: data['edad'] ?? 0,
      puesto: data['puesto'] ?? '',
    );
  }

  // Convertir de Objeto a Firestore
  Map<String, dynamic> toMap() {
    return {
      'nombre': nombre,
      'edad': edad,
      'puesto': puesto,
    };
  }
}
```

### 2. El Data Master (Servicios CRUD)
`lib/agents/data_master.dart`
```dart
import 'cloud_firestore/cloud_firestore.dart';
import 'architect.dart';

class DataMaster {
  final CollectionReference coleccion = FirebaseFirestore.instance.collection('empleados');

  // CREATE
  Future<void> agregarEmpleado(Empleado emp) => coleccion.add(emp.toMap());

  // READ (Stream para tiempo real)
  Stream<List<Empleado>> consultarEmpleados() {
    return coleccion.snapshots().map((snapshot) =>
        snapshot.docs.map((doc) => Empleado.fromFirestore(doc.data() as Map<String, dynamic>, doc.id)).toList());
  }

  // UPDATE
  Future<void> actualizarEmpleado(Empleado emp) => coleccion.doc(emp.id).update(emp.toMap());

  // DELETE
  Future<void> eliminarEmpleado(String id) => coleccion.doc(id).delete();
}
```

### 3. UI Designer (Interfaz con Colores Atractivos)
`lib/ui/home_screen.dart`
```dart
import 'package:flutter/material.dart';
import '../agents/data_master.dart';
import '../agents/architect.dart';

class HomeScreen extends StatelessWidget {
  final DataMaster _master = DataMaster();
  final TextEditingController _nameCtrl = TextEditingController();
  final TextEditingController _ageCtrl = TextEditingController();
  final TextEditingController _jobCtrl = TextEditingController();

  void _mostrarForm(BuildContext context, {Empleado? empleado}) {
    if (empleado != null) {
      _nameCtrl.text = empleado.nombre;
      _ageCtrl.text = empleado.edad.toString();
      _jobCtrl.text = empleado.puesto;
    }

    showModalBottomSheet(
      backgroundColor: Colors.grey[900],
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(20)),
      context: context,
      builder: (ctx) => Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          children: [
            TextField(controller: _nameCtrl, style: TextStyle(color: Colors.white), decoration: InputDecoration(labelText: 'Nombre', labelStyle: TextStyle(color: Colors.orangeAccent))),
            TextField(controller: _ageCtrl, keyboardType: TextInputType.number, style: TextStyle(color: Colors.white), decoration: InputDecoration(labelText: 'Edad', labelStyle: TextStyle(color: Colors.orangeAccent))),
            TextField(controller: _jobCtrl, style: TextStyle(color: Colors.white), decoration: InputDecoration(labelText: 'Puesto', labelStyle: TextStyle(color: Colors.orangeAccent))),
            SizedBox(height: 20),
            ElevatedButton(
              style: ElevatedButton.styleFrom(backgroundColor: Colors.orangeAccent),
              onPressed: () {
                final emp = Empleado(
                  id: empleado?.id ?? '',
                  nombre: _nameCtrl.text,
                  edad: int.parse(_ageCtrl.text),
                  puesto: _jobCtrl.text,
                );
                empleado == null ? _master.agregarEmpleado(emp) : _master.actualizarEmpleado(emp);
                Navigator.pop(ctx);
                _nameCtrl.clear(); _ageCtrl.clear(); _jobCtrl.clear();
              },
              child: Text(empleado == null ? 'Guardar' : 'Actualizar', style: TextStyle(color: Colors.black)),
            )
          ],
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Color(0xFF121212), // Dark Theme
      appBar: AppBar(title: Text('OXXO CRUD - Empleados'), backgroundColor: Colors.redAccent),
      body: StreamBuilder<List<Empleado>>(
        stream: _master.consultarEmpleados(),
        builder: (context, snapshot) {
          if (!snapshot.hasData) return Center(child: CircularProgressIndicator());
          return ListView.builder(
            itemCount: snapshot.data!.length,
            itemBuilder: (context, i) {
              final e = snapshot.data![i];
              return Card(
                color: Color(0xFF1E1E1E),
                margin: EdgeInsets.symmetric(horizontal: 15, vertical: 8),
                child: ListTile(
                  title: Text(e.nombre, style: TextStyle(color: Colors.orangeAccent, fontWeight: FontWeight.bold)),
                  subtitle: Text("${e.puesto} - ${e.edad} años", style: TextStyle(color: Colors.white70)),
                  trailing: Row(
                    mainAxisSize: MainAxisSize.min,
                    children: [
                      IconButton(icon: Icon(Icons.edit, color: Colors.blueAccent), onPressed: () => _mostrarForm(context, empleado: e)),
                      IconButton(icon: Icon(Icons.delete, color: Colors.redAccent), onPressed: () => _master.eliminarEmpleado(e.id)),
                    ],
                  ),
                ),
              );
            },
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        backgroundColor: Colors.redAccent,
        onPressed: () => _mostrarForm(context),
        child: Icon(Icons.add, color: Colors.white),
      ),
    );
  }
}
```

### 4. Punto de Entrada Principal
`lib/main.dart`
```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'ui/home_screen.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(); // Inicialización vital
  runApp(MaterialApp(
    debugShowCheckedModeBanner: false,
    theme: ThemeData(brightness: Brightness.dark, primaryColor: Colors.redAccent),
    home: HomeScreen(),
  ));
}
```

---

## 🚀 Flujo de Trabajo (Resumen para el Estudiante)

1.  **Entrada:** El estudiante inicia la app (Agente UI).
2.  **Solicitud:** Al dar clic en "+", el **Architect** prepara el molde de datos.
3.  **Procesamiento:** El **Data Master** recibe la información y la envía a la nube (Firestore).
4.  **Feedback:** Gracias a `StreamBuilder`, la UI se actualiza automáticamente sin refrescar, dando una sensación de fluidez (Antigravity).

¿Te gustaría que ajustemos algún color específico para que combine más con la marca OXXO o prefieres profundizar en la seguridad de Firestore?
