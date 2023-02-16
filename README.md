# Base Ubuntu

Este role funciona únicamente para sistemas **Ubuntu** y es el encargado de:

- Configurar los repositorios de Docker, Hashicorp y Ansible.
- Instalar y actualizar todos los paquetes base y todos los paquetes extra necesarios dependiento de cada host.
- Es el encargado de configurar el hostname de cada servidor y actualizar el fichero de /etc/hosts.
- Es el encargado de generar una llave ssh para el usuario **ubuntu**

### Repositorios a configurar:

Este role por defecto no configura ningún repositorio adicional a los del sistema. Sin embargo, podemos indicarle al role que configure algunos repositorios adicionales configurando un diccionario en host_vars o en group_vars, por ejemplo:

```YAML
list_repositories:
  docker_exist: True
  hashicorp_exist: True
  ansible_exist: True
```

Por defecto, estos valores están en _False_

### Paquetes a instalar:

Este role instala paquetes básicos que podréis encontrar en defaults/main.yml

Además permite instalar paquetes extra que son necesarios dependiendo del host. Para indicarle qué paquetes extra instalar debemos configurar la siguiente lista en host_vars o en group_vars. Ejemplo:

```YAML
list_packages_install_extra:
  - docker-ce
  - docker-ce-cli
  - containerd.io
```

### Indicar el hostname:

Este role requiere que se le indique el hostname del servidor que se está configurando. Esto se realiza declarando una variable en el fichero de host_vars correspondiente. Ejemplo:

```YAML
hostname: bender
```

### Actualización de /etc/hosts:

Para añadir hosts al DNS interno del servidor se ha de declarar la lista de la siguiente forma:

```YAML
hosts_list:
  - "10.1.1.1 example"
```

### Denegar acceso SSH con usuario y contraseña:
Se realiza por defecto en la task 004-ssh.yml
