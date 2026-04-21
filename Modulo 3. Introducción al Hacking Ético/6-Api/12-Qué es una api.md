![[Pasted image 20260414124927.png]]





![[Pasted image 20260414125048.png]]

![[Pasted image 20260414125146.png]]

![[Pasted image 20260414125215.png]]

























```plaintext
from flask import Flask, jsonify, request

# Crear una instancia de la aplicación Flask
app = Flask(__name__)

# Datos de ejemplo (simulando una base de datos)
users = [
    {"id": 1, "name": "Alice", "age": 25},
    {"id": 2, "name": "Bob", "age": 30}
]

# Endpoint para obtener todos los usuarios (GET /users)
@app.route('/users', methods=['GET'])
def get_users():
    return jsonify(users)

# Endpoint para obtener un usuario específico por ID (GET /users/<int:user_id>)
@app.route('/users/<int:user_id>', methods=['GET'])
def get_user(user_id):
    user = next((user for user in users if user["id"] == user_id), None)
    if user:
        return jsonify(user)
    else:
        return jsonify({"error": "User not found"}), 404

# Endpoint para agregar un nuevo usuario (POST /users)
@app.route('/users', methods=['POST'])
def add_user():
    new_user = request.get_json()
    new_user["id"] = len(users) + 1
    users.append(new_user)
    return jsonify(new_user), 201

# Endpoint para actualizar un usuario existente (PUT /users/<int:user_id>)
@app.route('/users/<int:user_id>', methods=['PUT'])
def update_user(user_id):
    user = next((user for user in users if user["id"] == user_id), None)
    if user:
        updated_data = request.get_json()
        user.update(updated_data)
        return jsonify(user)
    else:
        return jsonify({"error": "User not found"}), 404

# Endpoint para eliminar un usuario (DELETE /users/<int:user_id>)
@app.route('/users/<int:user_id>', methods=['DELETE'])
def delete_user(user_id):
    global users
    user = next((user for user in users if user["id"] == user_id), None)
    if user:
        users = [user for user in users if user["id"] != user_id]
        return jsonify({"message": "User deleted"})
    else:
        return jsonify({"error": "User not found"}), 404

# Ejecutar la aplicación
if __name__ == '__main__':
    # Escuchar en todas las interfaces de red (0.0.0.0) y en el puerto 5000
    app.run(host='0.0.0.0', port=5000, debug=True)
```