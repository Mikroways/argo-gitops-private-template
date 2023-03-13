# Wordpress desplegado con GitOps

Este repositorio, mantiene varios ejemplos de GitOps que son referenciados desde
el [flujo propuesto por Mikroways](https://github.com/Mikroways/argo-gitops-demo-example/).

Este repositorio en un ejemplo real, no debe ser un único repositorio con varios
directorios, sino que cada directorio debería existir en un repositorio
independiente. Obviamente que esto dependenrá de cada usuario del flujo, pero
mantener repositorios independientes ofrece mayor desacoplamiento y los permisos
sobre cada uno se vuelve más granular. Así como el esquema de trabajo del equipo
que mantenga ese despliegue GitOps.

## Ejemplos en este repositorio

Debido a que el flujo presenta varios ejemplos, con este repositorio
completaremos los ejemplos que requieren trabajar con:

* Un repositorio de GitOps: desplegará un wordpess
* Un repositorio de GitOps con una registry privada
* Un repositorio de GitOps utilizando un repositorio de chart privado.

## Uso del repositorio

Este repositorio, no deberá usarse directamente, sino que la idea, es crear un
nuevo repositorio **personal y privado** desde el botón [template](https://github.com/Mikroways/argo-gitops-private-template/generate).

Una vez creado el repositorio privado seguir la documentación de cada
directorio y del flujo para así completar la experiencia.
