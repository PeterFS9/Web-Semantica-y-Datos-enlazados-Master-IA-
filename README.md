# Curso20252026
================

Este es el repositorio que utilizaremos para nuestro trabajo colaborativo, y para llevar a cabo las entregas de la asignatura. Recuerda que tienes instrucciones mas detalladas sobre el trabajo [aquí](https://docs.google.com/document/d/e/2PACX-1vQrfa6nrN-4nbLWARcyWrY5AxN9lbwRMbT9OuwGHTSXwfQUN5ak7a945mgsuqt7QSPZ5fvYUbh_oZQk/pub)

A nivel técnico, este es el proceso normal que el alumno tendrá que seguir:

* Realizar un Fork al repositorio principal en tu propia cuenta (esto generará un nuevo repositorio en tu cuenta de GitHub). Este paso se realiza solo una vez en el curso. En este repositorio deberás crear un directorio con tu nombre, donde estarán los documentos y datos de tu trabajo.

* Si ya has realizado el fork sobre este repositorio, deberás sincronizar tu repositorio con la versión actual. Para ello debes [configurar un remote para el fork](https://help.github.com/articles/configuring-a-remote-for-a-fork) y [sincronizar tu fork](https://help.github.com/articles/syncing-a-fork). Básicamente debe:
 * Establece el remote: 
 
        git remote add upstream https://github.com/AEPIA-WebSemanticaDatosEnlazados/Curso20212022

 * Recuperar cualquier cambio hecho en él: 
 
        git fetch upstream
 
 * Realizar un checkout de la rama principal en local del fork: 
 
        git checkout master
 
 * Hacer un merge de los cambios desde el remote en su rama principal: 
 
        git merge upstream/master

* Realizar cambios en el repositorio.
* Hacer commit de los cambios en el repositorio local
* Hacer push de los cambios al repositorio online de cada alumno.
* Hacer un pull request, de tal forma que los cambios puedan ser aceptados e incorporados en el repositorio general

Cada alumno creará un directorio dentro del proyecto, usando su nombre y apellidos, e incluirá en dicho directorio todos los documentos relativos a su trabajo. De cara a evitar problemas de gestión, ningún alumno deberá modificar el contenido del trabajo de otro alumno. Las contribuciones mediante comentarios o issues en github y/o en el foto de la asignatura son bienvenidas.
