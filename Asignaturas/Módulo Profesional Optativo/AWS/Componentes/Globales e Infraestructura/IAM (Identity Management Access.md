**Definición:** Servicio que permite administrar el acceso a los recursos de AWS de forma segura.

- **Autenticación (Authentication):** ¿Quién eres? (Login).
    
- **Autorización (Authorization):** ¿Qué tienes permiso para hacer? (Permissions).
    

> **Ejemplo Real:** Imagina un edificio de oficinas de alta seguridad.
> 
> - La tarjeta de identificación es tu **Usuario IAM**.
>     
> - El departamento al que perteneces es tu **Grupo IAM**.
>     
> - Las reglas de "Solo personal autorizado en Sala de Servidores" es la **Política**.
>     
> - La tarjeta de visita temporal que le das a un consultor externo es un **Rol**.
>     

---

## 1. Componentes Esenciales

### 👤 Usuario de IAM (User)

- **¿Qué es?**: Una identidad dentro de tu cuenta de AWS que tiene permisos específicos.
    
- **Uso:** Representa a una **persona** (tú, un administrador) o una **aplicación** que necesita interactuar con AWS.
    
- **Credenciales:** Tiene credenciales permanentes (Usuario/Contraseña para consola, o Access Keys para código).
    

### 👥 Grupo de IAM (Group)

- **¿Qué es?**: Una colección de usuarios de IAM.
    
- **Uso:** Sirve para gestionar permisos a gran escala. En lugar de dar permisos a 100 personas una por una, se los das al grupo.
    
- **Regla:** Un usuario puede pertenecer a **varios grupos** a la vez.
    
    - _Ejemplo:_ "Li Juan" está en el grupo `Developers` (para programar) y en el grupo `Testers` (para probar). Hereda los permisos de ambos.
        

### 📜 Política de IAM (Policy)

- **¿Qué es?**: Un documento que define explícitamente los permisos (qué se puede hacer y sobre qué recurso).
    
- **Formato:** Se escriben siempre en **JSON**.
    
- **Asignación:** Se pueden "pegar" a Usuarios, Grupos o Roles.
    

### 🎭 Rol de IAM (Role)

- **¿Qué es?**: Un conjunto de permisos que **no** tiene credenciales permanentes (sin contraseña).
    
- **Uso:** Es como un "disfraz" o sombrero de permisos que alguien se pone temporalmente.
    
- **¿Quién lo usa?**:
    
    - Un servicio de AWS (ej. una máquina EC2 que necesita subir fotos a S3).
        
    - Un usuario de otra cuenta de AWS.
        

---

## 2. Ejemplo Práctico: Política JSON

Como desarrollador, te encontrarás con esto a menudo. Así se ve una política que permite **solo leer** archivos en S3:

JSON

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",        // 1. ¿Permitir o Denegar?
      "Action": "s3:ListBucket", // 2. ¿Qué acción? (Listar archivos)
      "Resource": "arn:aws:s3:::mi-bucket-de-fotos" // 3. ¿Sobre qué recurso?
    }
  ]
}
```

## 3. Best Practices (Para tu examen)

1. **Least Privilege (Privilegio Mínimo):** Dale a Li Juan solo los permisos exactos que necesita para su trabajo, ni uno más.
    
2. **Nunca uses el usuario `root`:** Crea un usuario IAM Admin para el día a día. El root guárdalo bajo llave.
    
3. **Usa Grupos:** Evita asignar políticas a usuarios individuales; asígnalas a grupos.
    