Vamos a crear un formulario de login:
```python
from flask import Flask, render_template, request, redirect, url_for, session, flash
from flask_sqlalchemy import SQLAlchemy
from datetime import datetime
import os

app = Flask(__name__)
app.secret_key = 'tu_clave_secreta_aqui'  # Cambia esto por una clave secreta fuerte

# Configuración de la base de datos
basedir = os.path.abspath(os.path.dirname(__file__))
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + os.path.join(basedir, 'database.db')
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)

# Modelos de la base de datos
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(80), unique=True, nullable=False)
    password = db.Column(db.String(120), nullable=False)
    
    def __repr__(self):
        return f'<User {self.username}>'

class LoginRecord(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    user_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
    login_time = db.Column(db.DateTime, nullable=False, default=datetime.utcnow)
    ip_address = db.Column(db.String(50))

# Crear las tablas (ejecutar solo una vez)
with app.app_context():
    db.create_all()

@app.route('/')
def home():
    if 'username' in session:
        return redirect(url_for('welcome'))
    return redirect(url_for('login'))

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        username = request.form['username']
        password = request.form['password']
        
        user = User.query.filter_by(username=username, password=password).first()
        
        if user:
            session['username'] = username
            session['user_id'] = user.id
            
            # Registrar el acceso
            new_record = LoginRecord(
                user_id=user.id,
                ip_address=request.remote_addr
            )
            db.session.add(new_record)
            db.session.commit()
            
            return redirect(url_for('welcome'))
        else:
            flash('Usuario o contraseña incorrectos', 'error')
    
    return render_template('login.html')

@app.route('/welcome')
def welcome():
    if 'username' in session:
        # Obtener historial de accesos
        access_history = LoginRecord.query.filter_by(user_id=session['user_id']).order_by(LoginRecord.login_time.desc()).all()
        return render_template('welcome.html', username=session['username'], history=access_history)
    return redirect(url_for('login'))

@app.route('/logout')
def logout():
    session.pop('username', None)
    session.pop('user_id', None)
    return redirect(url_for('login'))

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000, debug=True)
``` 
Los estilos CSS en static/style.css:
```bash
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f9;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.login-container, .welcome-container {
    background: white;
    padding: 2rem;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    width: 100%;
    max-width: 400px;
}

h1 {
    text-align: center;
    color: #333;
}

.form-group {
    margin-bottom: 1rem;
}

label {
    display: block;
    margin-bottom: 0.5rem;
    color: #555;
}

input {
    width: 100%;
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    box-sizing: border-box;
}

.btn {
    width: 100%;
    padding: 0.75rem;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1rem;
}

.btn:hover {
    background-color: #0056b3;
}

.alert {
    padding: 0.75rem;
    margin-bottom: 1rem;
    border-radius: 4px;
}

.alert-error {
    background-color: #f8d7da;
    color: #721c24;
    border: 1px solid #f5c6cb;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin: 1rem 0;
}

th, td {
    padding: 0.5rem;
    text-align: left;
    border-bottom: 1px solid #ddd;
}

th {
    background-color: #f4f4f4;
}
```
El templates/login.html:
```html
<!-- templates/login.html -->
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Iniciar sesión</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <div class="login-container">
        <h2>Iniciar sesión</h2>

        {% with messages = get_flashed_messages(with_categories=true) %}
          {% if messages %}
            {% for category, message in messages %}
              <div class="flash-message">{{ message }}</div>
            {% endfor %}
          {% endif %}
        {% endwith %}

        <form method="POST" action="{{ url_for('login') }}">
            <input type="text" name="username" placeholder="Usuario" required>
            <input type="password" name="password" placeholder="Contraseña" required>
            <input type="submit" value="Entrar">
        </form>
    </div>
</body>
</html>
```
Y el templates/welcome.html:
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bienvenido</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
</head>
<body>
    <div class="welcome-container">
        <h1>Bienvenido, {{ username }}!</h1>
        <p>Has iniciado sesión correctamente.</p>
        
        <h2>Historial de accesos:</h2>
        <table>
            <thead>
                <tr>
                    <th>Fecha y Hora</th>
                    <th>Dirección IP</th>
                </tr>
            </thead>
            <tbody>
                {% for record in history %}
                <tr>
                    <td>{{ record.login_time.strftime('%Y-%m-%d %H:%M:%S') }}</td>
                    <td>{{ record.ip_address }}</td>
                </tr>
                {% endfor %}
            </tbody>
        </table>
        
        <a href="{{ url_for('logout') }}" class="btn">Cerrar Sesión</a>
    </div>
</body>
</html>
```
De tal forma que tendremos el siguiente panel de login:
![[Pasted image 20250730093236.png]]
De tal forma que desde un cliente iniciaremos sesión y con wireshark al filtrar por paquetes del protocolo HTTP veremos las credenciales en texto plano:
![[Pasted image 20250730093327.png]]

## FILTROS ÚTILES
Para HTTP:
```bash
tcp.port == 80
```
Y por HTTPS:
```bash
tcp.port == 443
```
![[Pasted image 20250731130426.png]]
**Filtrar por un dominio**
```bash
dns.qry.name == "dockerlabs.es"
```
![[Pasted image 20250731130552.png]]
Vamos a analizar estos paquetes explicando que está ocurriendo:
![[Pasted image 20250731130620.png]]
### 📦 1. `Standard query 0xe38f A dockerlabs.es`

- **Tipo**: Consulta DNS.
    
- **Query ID**: `0xe38f`.
    
- **Tipo de registro**: `A` (IPv4).
    
- **Dominio solicitado**: `dockerlabs.es`.
    
- 🧠 El cliente está preguntando: “¿Cuál es la dirección IPv4 del dominio `dockerlabs.es`?”
    

---

### 📦 2. `Standard query 0x7d8d AAAA dockerlabs.es`

- **Tipo**: Consulta DNS.
    
- **Query ID**: `0x7d8d`.
    
- **Tipo de registro**: `AAAA` (IPv6).
    
- **Dominio solicitado**: `dockerlabs.es`.
    
- 🧠 El cliente también quiere saber: “¿Cuál es la dirección IPv6 del dominio `dockerlabs.es`?”
    

---

### 📦 3. `Standard query response 0xe38f A dockerlabs.es A 54.36.101.154`

- **Tipo**: Respuesta DNS.
    
- **Query ID**: `0xe38f` (coincide con la primera consulta).
    
- **Respuesta**: El servidor responde que la dirección IPv4 de `dockerlabs.es` es `54.36.101.154`.
    
- 🧠 Esta IP es la que se usará para establecer conexión TCP/HTTPS después.
    

---

### 📦 4. `Standard query response 0x7d8d AAAA dockerlabs.es`

- **Tipo**: Respuesta DNS.
    
- **Query ID**: `0x7d8d` (coincide con la consulta de tipo AAAA).
    
- **Respuesta**: El servidor responde **vacío o sin dirección IPv6**, probablemente porque `dockerlabs.es` no tiene configurado un registro AAAA.
    
- 🧠 El cliente no podrá usar IPv6 y usará la IP IPv4 (`54.36.101.154`) para comunicarse.

**Ver el Proceso de Comunicación TCP HTTPS**
Hemos aplciado el siguiente filtro:
```bash
ip.addr == 54.36.101.154 && tcp.port == 443
```
![[Pasted image 20250731130959.png]]
Y vemos que ocurre el proceso de three way handshake, ocurriendo los siguientes pasos:

🧱 1. Paquete 1: `SYN` - Tu equipo (cliente) inicia la conexión al servidor (`dockerlabs.es`) en el puerto 443 (HTTPS).
    
- `SYN` indica el comienzo de una nueva conexión TCP.
    
- Incluye opciones como:
    
    - **MSS (Maximum Segment Size)** = 1460
        
    - **SACK_PERM** (Selective ACK permitido)
        
    - **Window Scaling** y **Timestamps**

🧱 2. Paquete 2: `SYN, ACK`

- El servidor responde con `SYN, ACK`, confirmando que acepta la conexión.
    
- Indica que está preparado para establecer una conexión segura.
    
- Contiene su propia **MSS**, **ventana de recepción**, **timestamps**, etc.

🧱 3. Paquete 3: `ACK`

- Tu máquina responde con un `ACK`, completando el **3-way handshake** TCP.
    
- A partir de aquí, puede comenzar el **handshake TLS** (no aparece aún en la captura, pero sería el siguiente paso).

Esta secuencia indica que:

- La resolución DNS fue exitosa (ya tenías la IP).
    
- El servidor está **escuchando en el puerto 443**.
    
- La conexión TCP ha sido establecida con éxito.

Justo después de esta secuencia, comienza el handsharke TLS 1.3 necesario para establecer una conexión segura con https://dockerlabs.es:

📦 1. `Client Hello` (Paquete 1)

- Tu cliente (navegador o herramienta) inicia el handshake TLS.
    
- Especifica:
    
    - Versión TLS deseada (`TLS 1.3`)
        
    - Cifrados soportados (cipher suites)
        
    - Extensiones como:
        
        - **SNI (Server Name Indication)** → `dockerlabs.es`  
            Esto permite al servidor saber qué certificado usar si aloja varios dominios.
            
        - Soporte para ALPN, grupos de curvas elípticas, etc.
            

🧠 Este paquete es clave para identificar el **dominio al que accede el usuario, incluso aunque el tráfico sea cifrado**.


![[Pasted image 20250731131150.png]]

📦 2. `ACK` (TCP puro)

El servidor confirma recepción del `Client Hello`.

📦 3. `Server Hello` + `Change Cipher Spec` + `Application Data`

El servidor responde aceptando la conexión segura:

- Elige una de las **cipher suites** propuestas por el cliente.
    
- Manda su certificado (en TLS 1.3 va dentro del `EncryptedExtensions`).
    
- Cambia al modo **cifrado** (`Change Cipher Spec`).
    
- Envia datos cifrados (pueden ser handshake final o early data).


📦 4. `ACK` (respuesta TCP del cliente)

El cliente confirma la recepción del paquete anterior.

📦 5. `Change Cipher Spec` + `Application Data`

- El cliente también indica que ya ha establecido el canal cifrado.
    
- Envía **datos cifrados**, probablemente la **solicitud HTTPS (GET /)**.

✅ Conclusión:

- Se ha completado el **handshake TLS 1.3** entre tu equipo y `dockerlabs.es`.
    
- A partir de aquí, **todo el tráfico está cifrado** y se ve como `Application Data`.
    
- Aunque Wireshark no puede descifrarlo (sin claves), sí puedes ver que:
    
    - El dominio accedido fue `dockerlabs.es` (gracias al SNI).
        
    - El cifrado TLS fue exitoso.


## GUARDAR ARCHIVO PCAP

Ejecutamos el siguiente comando para guardar el tráfico de red en un archivo .pcap:
```bash
sudo tcpdump -i eth0 -w captura.pcap
```
![[Pasted image 20250731131603.png]]
Generamos cualquier tipo de tráfico:
![[Pasted image 20250731131635.png]]
Y lo tenemos por aquí en el .pcap:
![[Pasted image 20250731131651.png]]
Lo abrimos con wireshark:
![[Pasted image 20250731131855.png]]
