
# 🚀 Tutoriales 04, 06 y 07: Despliegue de Microservicio Node.js en AWS con Docker, ECR, ECS Fargate y ALB

**Estudiante:** Marbin Yesid Rivera Ciro  
**Curso:** Tópicos Especiales en Ingeniería de Software  
**Universidad:** Universidad EAFIT  
**Repositorio:** https://github.com/myripyesid/randomquotes

---

## 📌 Descripción del Proyecto

Este proyecto corresponde a la implementación y despliegue del microservicio **`randomquotes`** desarrollado en Node.js y Express. La solución fue empaquetada en un contenedor **Docker** y desplegada en la infraestructura de **Amazon Web Services (AWS)** utilizando una arquitectura serverless basada en **AWS Fargate** con balanceo de carga automático y despliegue continuo (CI/CD).

---

## 🛠️ Arquitectura y Tecnologías Utilizadas

* **Microservicio:** Node.js 24 + Express framework.
* **Contenerización:** Docker (`Dockerfile` optimizado).
* **Registro de Imágenes:** Amazon Elastic Container Registry (ECR).
* **Orquestación de Contenedores:** Amazon Elastic Container Service (ECS) en modo AWS Fargate (4 réplicas simultáneas).
* **Balanceo de Carga:** Application Load Balancer (ALB) con Target Group en puerto HTTP 80.
* **Seguridad:** AWS Security Groups con aislamiento de tráfico (ALB -> ECS Tasks).
* **Automatización CI/CD:** GitHub Actions.

---

## 🌐 Enlace del Microservicio en Vivo

* **URL del Balanceador de Carga (ALB):**  
  `http://randomquotes-alb-422030289.us-east-1.elb.amazonaws.com/

---

## 📸 Evidencias de Ejecución y Pruebas

### 1. Imagen publicada en Amazon ECR
*Evidencia de la imagen Docker cargada exitosamente en el repositorio privado de Amazon ECR con la etiqueta `latest`.*

![Amazon ECR](screenshots/ecr-image.png)

---

### 2. Clúster de ECS y Réplicas en Ejecución
*Evidencia de las 4 tareas (réplicas de contenedores) ejecutándose en estado `RUNNING` dentro de AWS Fargate.*

![ECS Cluster](<img width="1600" height="652" alt="image" src="https://github.com/user-attachments/assets/e0303947-8491-40a7-bee2-0bd77ee9eca5" />
)

---

### 3. Prueba de Balanceo de Carga (Application Load Balancer)
*Al realizar peticiones a la URL DNS del ALB, se observa cómo el balanceador distribuye el tráfico asignando la solicitud a diferentes `Container Id` (hostnames).*

![ALB Test 1](<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/ec068002-9780-45d0-b048-6e54c2a23ae9" />
)  
![ALB Test 2](<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/d87b34b6-0f4e-41e4-92e2-a175b215ed01" />
)  

---

### 4. Prueba de Autorrecuperación (*Auto-healing*)
*Demostración de resiliencia del clúster: al detener manualmente una tarea en ECS, el servicio detecta el fallo y despliega automáticamente una tarea de reemplazo para mantener el `Desired Count = 4`.*

![Auto Healing Test](screenshots/auto-healing.png)

---

### 5. Flujo de Despliegue Automático (GitHub Actions)
*Evidencia de la ejecución exitosa del flujo CI/CD al realizar un `push` a la rama principal (`main`).*

![GitHub Actions Workflow](<img width="597" height="547" alt="image" src="https://github.com/user-attachments/assets/7b6fc12e-2acf-415d-9651-e3b69c6c0df7" />
)

---

## ⚙️ Instrucciones para Ejecutar Localmente

```bash
# 1. Clonar el repositorio
git clone [https://github.com/myripyesid/randomquotes.git](https://github.com/myripyesid/randomquotes.git)
cd randomquotes

# 2. Construir la imagen Docker
docker build -t randomquotes .

# 3. Ejecutar el contenedor localmente en el puerto 8080
docker run --rm -p 8080:80 randomquotes
```

Acceder desde el navegador a: `http://localhost:8080`

---

## 📝 Conclusiones

1. **Escalabilidad y Alta Disponibilidad:** El uso de AWS Fargate junto a un Application Load Balancer permite distribuir el tráfico eficientemente entre múltiples contenedores sin necesidad de gestionar servidores virtuales underlying.
2. **Resiliencia Operativa:** La arquitectura demostró la capacidad de autorrecuperación (*auto-healing*), garantizando la disponibilidad del servicio incluso ante fallos imprevistos en contenedores individuales.
3. **Automatización:** La integración de GitHub Actions simplificó el ciclo de vida del desarrollo de software, permitiendo compilaciones y despliegues automáticos a Amazon ECR y ECS en cada commit.
```
