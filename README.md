# Una máquina virtual para Ruby on Rails Core Development

## Introducción

Este proyecto automatiza el setup de un entorno de desarrollo para trabajar con Ruby on Riails. Utilice esta máquina virtual para trabajar en sus proyectos con todo listo para ejecutar y testear.

## Requerimientos y herramientas necesarias para poder instalar el ambiente de desarrollo

Herramientas que se recomienda instalar para poder trabajar con Ruby on Rails.

* [GitBash](http://git-scm.com/downloads)
* [Sublime Text 2](http://www.sublimetext.com/2)
* [VirtualBox](https://www.virtualbox.org) o [VMWare Fusion](http://www.vmware.com/products/fusion) o [Parallels Desktop](http://www.parallels.com/products/desktop/)(es necesaria la versión de Vagrant 1.5+, ver [vagrant-parallels](http://parallels.github.io/vagrant-parallels/docs/installation/index.html))

* [Vagrant 1.1+](http://vagrantup.com) (No para Ruby Gem)

## Como crear la máquina Virtual

Crear la máquina virtual es fácil

    host $ git clone https://github.com/rails/rails-dev-box.git
    host $ cd rails-dev-box
    host $ vagrant up

Eso es todo.

Si Ud. quiere usar VMWare Fusion en lugar de VirtualBox, escriba `vagrant up --provider=vmware_fusion` en lugar de `vagrant up` para crear la VM por primera vez. Luego de esto, Vagrant recordará su elección de proveedor, y ud. no necesitará incluir el  
provider` nuevamente

Si ud. desea isar Parallels Desktop en lugar de VirtualBox, Ud. necesitará Vagrant 1.5 o superior, y escribir `vagrant up --provider=parallels` en lugar de `vagrant up` cuando crea la VM por primera vez. Luego de esto Vagrant recordará su selección

Luego para acceder a la virtual machine usaremos Putty o similar mediante los siguientes comandos:

    host $ vagrant ssh
    Welcome to Ubuntu 12.04 LTS (GNU/Linux 3.2.0-23-generic-pae i686)
    ...
    vagrant@rails-dev-box:~$

El puerto 3000 es el designado para que escuche la VM, por lo que todas las aplicaciones que corran sobre la virtual machine pueden acceder vía localhost:3000 en la computadora que oficia de host.


## Que tenemos en esta distro

* Git

* RVM

* Ruby 2.0.0 (binary RVM install)

* Bundler

* SQLite3, MySQL, and Postgres

* System dependencies for nokogiri, sqlite3, mysql, mysql2, and pg

* Databases and users needed to run the Active Record test suite

* Node.js for the asset pipeline

* Memcached

## WorkFlow de trabajo recomendado

Se recomienda

* Editar en sus máquinas locales

* Probar en la VM

Solo se debe clonar el repositorio en la computadora y luego ejecutar los siguientes comandos:

    host $ ls
    README.md   Vagrantfile puppet
    host $ git clone git@github.com:<your username>/rails.git

Vagrant montará el directorio como /vagrant dentro de la VM


    vagrant@rails-dev-box:~$ ls /vagrant
    puppet  rails  README.md  Vagrantfile

Luego instalaremos las dependencias de GEM:

    vagrant@rails-dev-box:~$ cd /vagrant/rails
    vagrant@rails-dev-box:/vagrant/rails$ bundle

Estamos listos para editar en nuestras máquinas locales y testear en nuestra VM

Este workflow es conveniente porque en las computadoreas locales normalmente tendremos el editor de nuestra preferencia, nuestro GIT configurado y las keys SSH instaladas localmente.

## Como manejar nuestra VM

Cuándo terminemos nos desloguearemos y suspenderemos la VMachine

    host $ vagrant suspend

luego la reiniciamos nuevamente

    host $ vagrant resume

La ejecutamos

    host $ vagrant halt

Para darla de baja y volver a iniciarla

    host $ vagrant up

Se puede ver el status de la VM en cuanlquier momento invocando el siguiente comando

    host $ vagrant status

Finalmente para completar si queremos destruir todo el contenido

    host $ vagrant destroy # Cuidado este comando nos borrará todo lo realizado hasta el momento

Por favor, ver en [Vagrant documentation](http://docs.vagrantup.com/v2/) para más información sobre Vagrant.

## Testeo rápido de rails

Se aconseja usar el mecanismo por defecto para el uso compartido, luego todo se resuelve dentro de las veriones de Vagrant. Pero hay un par de alternativas más performantes.

### RSYNC

Vagrant 1.5 implementa un [mecanismos para compartir basado en rsync](https://www.vagrantup.com/blog/feature-preview-vagrant-1-5-rsync.html) que incorpora la posibilidad de leer y escribir los archivos porque dichos archivos se encuentran guardados en el cliente.

  Simplemente tipear el comando.

    config.vm.synced_folder '.', '/vagrant', type: 'rsync'

Para el _Vagrantfile_ ejecutar el comando

    vagrant rsync

O en su lugar para sincronizaciones aumtomáticas

    vagrant rsync-auto


### NFS

Si usamos un Mac OS X o Linux podremos incrementar la velocidad de Rails, testeado con Vagrant NFS Sincronizando carpetas

Con un server que soporte NFS (Mac OS X lo soporta) y las el siguiente archivo Vagrant

    config.vm.synced_folder '.', '/vagrant', type: 'nfs'
    config.vm.network 'private_network', ip: '192.168.50.4' # ensure this is available

Luego ejecutar

    host $ vagrant up

Por favor chequear la documentación de Vagrant en [NFS synced folders](http://docs.vagrantup.com/v2/synced-folders/nfs.html) para mayor informacion.


## Luego de instalar Vagrant 


Luego instalar vagrant haremos lo siguiente:

$ vagrant up (si aún no lo hicimos)
$ ls
README.md   Vagrantfile puppet

corremos entonces los siguientes comandos dentro de nuestra consola vagrant

$ vagrant ssh

$ rvm install ruby 2.1.2

$ rvm use 2.1.2@gema --create --default

$ gem update --system 

$ gem install rails --version 4.0.5
