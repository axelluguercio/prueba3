Para el ci/cd utilize la herramienta Github actions de Github que permite
Realizar pipelines desde 0 o utilizando actions ya previamente creadas por otros
usuarios.

En este caso buildie un imagen con un nginx de alpine y le pase el index.html. 
El yaml cicd presente en el workflow runear 2 jobs uno es el build y pusheo de la 
nueva imagen buildeade de nginx con el index.html y la sube a mi repositorio de docker
utilizando env secret de github action DOCKER_USERNAME y DOCKER_PASSWORD. 
EL repositorio se va llamar como el repositorio de github y la imagen va ser
tageada con el github.sha.

El ultimo job es el deploy-to-cluster que es un action pre armada en el repositorio
de steebchen que utilize en este caso se le pasa el KUBE_CONFIG_DATA como env que
no es nada menos que el output del kubeconfig que tengamos en el cluster, seguido
le va a pasar como argumento el deployment/app que en este caso seria el deployment
de nginx actualmente corriendo y el repositorio.

En este caso como yo utilize minikube y el job de deploy no puede acceder a mi cluster
local no puso completarse, pero en un ambiente de cloud donde el kubeconfig esta
bien configurado para poder acceder desde afuera a la api de kubernetes se 
completaria (siempre y cuando este el deploy de app corriendo).
