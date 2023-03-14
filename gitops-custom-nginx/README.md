# GitOps wordpress demo

Este repositorio, nos mostrará como podremos crear un despliegue basado en
GitOps usando el [chart público de nginx de bitnami](https://github.com/bitnami/charts/tree/main/bitnami/nginx).

El chart no sería el adecuado para la imagen que usaremos, pero en este
escenario donde queremos mostrar únicamente como utilizar una imagen privada que
require un [imagePullSecret](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/),
nos concentraremos en ello, y usaremos el chart público con una imágen
diferente, creada por nosotros desde [este mismo repositorio](../docker).

A diferencia del chart del wordpress en este mismo repositorio, aquí no
crearemos ningún chart de requerimientos, únicamente esta carpeta contendrá el
chart que depednerá del de nginx. La imagen será nuestra imagen privada, y por
supuesto, usaremos un secreto que el propio flujo de git, nos dejará listo en un
paso previo para ser usado desde este repositorio.

## Requisitos

A diferencia de los otros ejemplos, en este caso usaremos un chart sin datos
sensibles. Por tanto, aquí no nos preocuparemos por cifrar datos.

## Modificar `values.yaml`

Simplemente, es necesario modificar el archivo `values.yaml` que puede copiarse
y parametrizar sus valores a partir de `values.tpl.yaml`. La idea es simplemente
completar los campos que dicen CHANGEME.

Una vez finalizados todos los cambios, subirlos a git y hacer push:

```
git add .
git commit -m "Add custom values.yaml"
git push origin main
```

El nginx personalizado, podrá accederse con el ingress aquí configurado que
tendrá la url http://nginx-custom.private-registry.gitops.localhost.

Una vez editados los valores y subidos a git, podrá continuar con el [ejemplo de
GitOps que utiliza una registry privada](https://github.com/Mikroways/argo-gitops-demo-example/tree/main/projects?#un-ambiente-con-un-repositorio-externo-de-gitops-que-utiliza-registry-privada).

## Qué ignora este repositorio

El repositorio actual, ignora:

* El archivo `Chart.lock` para permitir a Argo CD detectar cambios cuando el
  chart del que depende nuestro chart saca un nuevo **patch number**. Esto es
  posible porque el `Chart.yaml` define como dependencia un **asterisco** en la
  versión del **patch number**. Si se versionara el `Chart.lock` esto no sería
  posible, porque Argo CD respetaría lo que el **indique el lock*.
* El directorio `charts/` que contiene las dependencias si corremos `helm
  dependency update`

## Cómo crear este directorio

El directorio actual fue creado usando, desde la carpeta inmediatamente
exterior, el siguiente comando:

```
helm create gitops-custom-nginx
cd gitops-custom-nginx
rm -fr {charts,templates,values.yaml} 
```

Luego, hemos editado `Chart.yaml` agregando como dependencia el chart de quién
dependen.
