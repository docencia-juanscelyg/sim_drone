# sim_drone_ws

Workspace de ROS 2 para ejecutar y probar una simulación de dron (Sin autopiloto). El workspace reúne paquetes ROS; cada paquete aporta nodos, configuración y, cuando corresponde, archivos de lanzamiento. El flujo habitual es compilar el workspace, cargar su entorno y lanzar la simulación.

![Simulación de Dron en Gazebo](doc/img0.jpg)

## Requisitos

- Una instalación de ROS 2 compatible con los paquetes del proyecto.
- `colcon` y las dependencias declaradas por los paquetes.
- La herramienta de simulación que requiera el proyecto (por ejemplo, Gazebo), si aplica.

Abre una terminal en la raíz del workspace (`sim_drone_ws`) y carga ROS 2. Sustituye `jazzy` por la distribución instalada:

```bash
source /opt/ros/jazzy/setup.bash
```

## Compilar

Instala las dependencias disponibles en los manifiestos y compila:

```bash
cd {ros workspace}
rosdep install --from-paths src --ignore-src -r -y
colcon build
source install/setup.bash
```

Vuelve a ejecutar `source install/setup.bash` en cada terminal nueva donde quieras usar los paquetes del workspace.

## Ejecutar la simulación

Para lanzar la simulación del dron en Gazebo, ejecuta el siguiente comando:

```bash
ros2 launch sim_drone sim_gazebo.launch.py
```

Este launch file inicia:
- El servidor de Gazebo con el mundo personalizado (`drone_world.sdf`)
- La interfaz gráfica de Gazebo
- El robot state publisher para cargar la descripción del robot
- El bridge ROS-Gazebo para la comunicación entre ROS 2 y Gazebo
- El spawn del modelo del dron en la simulación

El mundo incluye el plugin de IMU y de barometer, y está configurado para proporcionar una plataforma de simulación realista para el dron.

