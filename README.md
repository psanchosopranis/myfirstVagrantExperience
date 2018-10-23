# myfirstVagrantExperience

# Lab 01: Setting-up a Fabric Network

## Configuración inicial previa 

```sh
devel1@VBXLFD271:~$ mkdir -pv LDF271/labs/material
mkdir: se ha creado el directorio 'LDF271'
mkdir: se ha creado el directorio 'LDF271/labs'
mkdir: se ha creado el directorio 'LDF271/labs/material'

devel1@VBXLFD271:~$ cd LDF271/labs/material/
```

```sh
devel1@VBXLFD271:~/LDF271/labs/material$ wget https://lms.quickstart.com/custom/863027/Lab01.pdf
--2018-10-21 12:39:50--  https://lms.quickstart.com/custom/863027/Lab01.pdf
Resolviendo lms.quickstart.com (lms.quickstart.com)... 52.206.157.95, 54.85.14.94
Conectando con lms.quickstart.com (lms.quickstart.com)[52.206.157.95]:443... conectado.
Petición HTTP enviada, esperando respuesta... 200 OK
Longitud: 343470 (335K) [application/pdf]
Guardando como: "Lab01.pdf"

Lab01.pdf           100%[===================>] 335,42K   455KB/s    en 0,7s    

2018-10-21 12:39:52 (455 KB/s) - "Lab01.pdf" guardado [343470/343470]

devel1@VBXLFD271:~/LDF271/labs/material$ wget --user=LFtraining --password=Penguin2014 https://training.linuxfoundation.org/cm/LFD271/fabric-fundamentals.box
--2018-10-21 12:47:51--  https://training.linuxfoundation.org/cm/LFD271/fabric-fundamentals.box
Resolviendo training.linuxfoundation.org (training.linuxfoundation.org)... 151.101.133.5
Conectando con training.linuxfoundation.org (training.linuxfoundation.org)[151.101.133.5]:443... conectado.
Petición HTTP enviada, esperando respuesta... 401 Restricted
Autenticación seleccionada: Basic realm="Linux Training"
Conectando con training.linuxfoundation.org (training.linuxfoundation.org)[151.101.133.5]:443... conectado.
Petición HTTP enviada, esperando respuesta... 200 OK
Longitud: 1309069691 (1,2G) [application/octet-stream]
Guardando como: "fabric-fundamentals.box"

fabric-fundamentals.box                    100%[=======================================================================================>]   1,22G   929KB/s    en 1m 52s  

2018-10-21 12:49:43 (11,1 MB/s) - "fabric-fundamentals.box" guardado [1309069691/1309069691]

devel1@VBXLFD271:~/LDF271/labs/material$ wget --user=LFtraining --password=Penguin2014 https://training.linuxfoundation.org/cm/LFD271/md5sums.txt
--2018-10-21 12:50:11--  https://training.linuxfoundation.org/cm/LFD271/md5sums.txt
Resolviendo training.linuxfoundation.org (training.linuxfoundation.org)... 151.101.133.5
Conectando con training.linuxfoundation.org (training.linuxfoundation.org)[151.101.133.5]:443... conectado.
Petición HTTP enviada, esperando respuesta... 401 Restricted
Autenticación seleccionada: Basic realm="Linux Training"
Conectando con training.linuxfoundation.org (training.linuxfoundation.org)[151.101.133.5]:443... conectado.
Petición HTTP enviada, esperando respuesta... 200 OK
Longitud: 58 [text/plain]
Guardando como: "md5sums.txt"

md5sums.txt                                100%[=======================================================================================>]      58  --.-KB/s    en 0s      

2018-10-21 12:50:11 (4,28 MB/s) - "md5sums.txt" guardado [58/58]

devel1@VBXLFD271:~/LDF271/labs/material$ ls -la
total 1278752
drwxr-xr-x 2 devel1 devel1       4096 oct 21 12:50 .
drwxr-xr-x 3 devel1 devel1       4096 oct 21 12:39 ..
-rw-r--r-- 1 devel1 devel1 1309069691 ago 13 18:38 fabric-fundamentals.box
-rw-r--r-- 1 devel1 devel1     343470 sep  6 10:02 Lab01.pdf
-rw-r--r-- 1 devel1 devel1         58 ago 14 02:00 md5sums.txt

devel1@VBXLFD271:~/LDF271/labs/material$ cat md5sums.txt && md5sum fabric-fundamentals.box 
21a5365bc61da9f6309ecf81d4a7aba0  fabric-fundamentals.box
21a5365bc61da9f6309ecf81d4a7aba0  fabric-fundamentals.box
```

### Instalación de Vagrant (1. Download and Install Vagrant)

Visit the Vagrant downloads page (https://www.vagrantup.com/downloads.html) and download and install the
appropriate version for your operating system.
The installer will automatically add vagrant to your system path so that it is available from the terminal (or
command prompt). If it is not found, please try logging out and logging back into your system (this step is
necessary on some versions of Windows).

```sh
devel1@VBXLFD271:~/LDF271/labs/material$ wget https://releases.hashicorp.com/vagrant/2.2.0/vagrant_2.2.0_x86_64.deb
--2018-10-21 12:57:56--  https://releases.hashicorp.com/vagrant/2.2.0/vagrant_2.2.0_x86_64.deb
Resolviendo releases.hashicorp.com (releases.hashicorp.com)... 151.101.133.183, 2a04:4e42:1f::439
Conectando con releases.hashicorp.com (releases.hashicorp.com)[151.101.133.183]:443... conectado.
Petición HTTP enviada, esperando respuesta... 200 OK
Longitud: 40112146 (38M) [application/x-debian-package]
Guardando como: "vagrant_2.2.0_x86_64.deb"

vagrant_2.2.0_x86_64.deb                   100%[=======================================================================================>]  38,25M  31,6MB/s    en 1,2s    

2018-10-21 12:57:57 (31,6 MB/s) - "vagrant_2.2.0_x86_64.deb" guardado [40112146/40112146]

devel1@VBXLFD271:~/LDF271/labs/material$ wget https://releases.hashicorp.com/vagrant/2.2.0/vagrant_2.2.0_SHA256SUMS
--2018-10-21 12:58:46--  https://releases.hashicorp.com/vagrant/2.2.0/vagrant_2.2.0_SHA256SUMS
Resolviendo releases.hashicorp.com (releases.hashicorp.com)... 151.101.133.183, 2a04:4e42:1f::439
Conectando con releases.hashicorp.com (releases.hashicorp.com)[151.101.133.183]:443... conectado.
Petición HTTP enviada, esperando respuesta... 200 OK
Longitud: 821 [text/plain]
Guardando como: "vagrant_2.2.0_SHA256SUMS"

vagrant_2.2.0_SHA256SUMS                   100%[=======================================================================================>]     821  --.-KB/s    en 0s      

2018-10-21 12:58:46 (60,9 MB/s) - "vagrant_2.2.0_SHA256SUMS" guardado [821/821]

devel1@VBXLFD271:~/LDF271/labs/material$ tree
.
+-- fabric-fundamentals.box
+-- Lab01.pdf
+-- md5sums.txt
+-- vagrant_2.2.0_SHA256SUMS
+-- vagrant_2.2.0_x86_64.deb

0 directories, 5 files

devel1@VBXLFD271:~/LDF271/labs/material$ cat vagrant_2.2.0_SHA256SUMS && sha256sum vagrant_2.2.0_x86_64.deb 
af16d67b066c47a38fe031a5f48093709b84db00af1fea4efe169ad4ea025855  vagrant_2.2.0_i686.deb
f6c12594e2247d4c53b4616f8088e59754b77c5c2c0a0dc4b267ac4c87fb0ea2  vagrant_2.2.0_i686.msi
33f610c9cfec9f568925987ca5210a7a4b993a135f544e782cb4fbcc66067c6d  vagrant_2.2.0_i686.rpm
4e12cb35ac7970ae1f2acea958c322a1762b32b7adfbb984268884b7f135b108  vagrant_2.2.0_linux_amd64.zip
f1caad948a8f545d5d7d2442396fe8a3bcdfd0fc8f643bd0576c81942e7be43b  vagrant_2.2.0_x86_64.deb
016bf5470cf940df50dceae7fd5f0d333617ca42835f106846c91669b3305255  vagrant_2.2.0_x86_64.dmg
5be450b7a1c89f8a44ccef88c2a737fd7973cbf528e5279772966ea0c7683567  vagrant_2.2.0_x86_64.msi
d37c543e90926c375ad00484e069d7afb1d8878eea2f648b40be16abc70aa2c5  vagrant_2.2.0_x86_64.rpm
331ee4ccbe70a539c2a138417b1981dabb6f580f5f5956a675039a1622831b1d  vagrant_2.2.0_x86_64.tar.xz
f1caad948a8f545d5d7d2442396fe8a3bcdfd0fc8f643bd0576c81942e7be43b  vagrant_2.2.0_x86_64.deb

devel1@VBXLFD271:~/LDF271/labs/material$ sudo dpkg -i vagrant_2.2.0_x86_64.deb 
Seleccionando el paquete vagrant previamente no seleccionado.
(Leyendo la base de datos ... 146238 ficheros o directorios instalados actualmente.)
Preparando para desempaquetar vagrant_2.2.0_x86_64.deb ...
Desempaquetando vagrant (1:2.2.0) ...
Configurando vagrant (1:2.2.0) ...

devel1@VBXLFD271:~/LDF271/labs/material$ vagrant --help
WARNING: This command has been deprecated in favor of `vagrant cloud auth login`
Usage: vagrant [options] <command> [<args>]

    -v, --version                    Print the version and exit.
    -h, --help                       Print this help.

Common commands:
     box             manages boxes: installation, removal, etc.
     cloud           manages everything related to Vagrant Cloud
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login           
     package         packages a running vagrant environment into a box
     plugin          manages plugins: install, uninstall, update, etc.
     port            displays information about guest port mappings
     powershell      connects to machine via powershell remoting
     provision       provisions the vagrant machine
     push            deploys code in this environment to a configured destination
     rdp             connects to machine via RDP
     reload          restarts vagrant machine, loads new Vagrantfile configuration
     resume          resume a suspended vagrant machine
     snapshot        manages snapshots: saving, restoring, etc.
     ssh             connects to machine via SSH
     ssh-config      outputs OpenSSH valid configuration to connect to the machine
     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     upload          upload to machine via communicator
     validate        validates the Vagrantfile
     version         prints current and latest Vagrant version
     winrm           executes commands on a machine via WinRM
     winrm-config    outputs WinRM configuration to connect to the machine

For help on any individual command run `vagrant COMMAND -h`

Additional subcommands are available, but are either more advanced
or not commonly used. To see all subcommands, run the command
`vagrant list-commands`.

devel1@VBXLFD271:~/LDF271/labs/material$ vagrant --version
Vagrant 2.2.0

```

### Preparación de directorios para la realización del laboratorio 

```sh
devel1@VBXLFD271:~$ mkdir -pv /home/devel1/LDF271/labs/lab1
mkdir: se ha creado el directorio '/home/devel1/LDF271/labs/lab1'
devel1@VBXLFD271:~$ tree /home/devel1/LDF271
/home/devel1/LDF271
└── labs
    ├── lab1
    └── material
        ├── fabric-fundamentals.box
        ├── Lab01.pdf
        ├── md5sums.txt
        ├── vagrant_2.2.0_SHA256SUMS
        └── vagrant_2.2.0_x86_64.deb

3 directories, 5 files
devel1@VBXLFD271:~$ 
```

### Register fabric-fundamentals.box as a new box in your Vagrant environment, by running the following:

```sh
vagrant box add --name fabric-fundamentals fabric-fundamentals.box
```

```sh
devel1@VBXLFD271:~$ vagrant box add -h
Usage: vagrant box add [options] <name, url, or path>

Options:

    -c, --clean                      Clean any temporary download files
    -f, --force                      Overwrite an existing box if it exists
        --insecure                   Do not validate SSL certificates
        --cacert FILE                CA certificate for SSL download
        --capath DIR                 CA certificate directory for SSL download
        --cert FILE                  A client SSL cert, if needed
        --location-trusted           Trust 'Location' header from HTTP redirects and use the same credentials for subsequent urls as for the initial one
        --provider PROVIDER          Provider the box should satisfy
        --box-version VERSION        Constrain version of the added box

The box descriptor can be the name of a box on HashiCorp's Vagrant Cloud,
or a URL, or a local .box file, or a local .json file containing
the catalog metadata.

The options below only apply if you're adding a box file directly,
and not using a Vagrant server or a box structured like 'user/box':

        --checksum CHECKSUM          Checksum for the box
        --checksum-type TYPE         Checksum type (md5, sha1, sha256)
        --name BOX                   Name of the box
    -h, --help                       Print this help

devel1@VBXLFD271:~$ vagrant box add --name fabric-fundamentals /home/devel1/LDF271/labs/material/fabric-fundamentals.box 
==> box: Box file was not detected as metadata. Adding it directly...
==> box: Adding box 'fabric-fundamentals' (v0) for provider: 
    box: Unpacking necessary files from: file:///home/devel1/LDF271/labs/material/fabric-fundamentals.box
==> box: Successfully added box 'fabric-fundamentals' (v0) for 'virtualbox'!

```

```sh
devel1@VBXLFD271:~/LDF271/labs/lab1$ tree -ph $HOME/.vagrant.d/
/home/devel1/.vagrant.d/
├── [drwxr-xr-x 4.0K]  boxes
│   └── [drwxr-xr-x 4.0K]  fabric-fundamentals
│       └── [drwxr-xr-x 4.0K]  0
│           └── [drwxr-xr-x 4.0K]  virtualbox
│               ├── [-rw------- 1.2G]  box-disk1.vmdk
│               ├── [-rw-------  70K]  box-disk2.vmdk
│               ├── [-rw-------  12K]  box.ovf
│               ├── [drwxr-xr-x 4.0K]  include
│               │   └── [-rw-r--r--  772]  _Vagrantfile
│               ├── [-rw-r--r--   25]  metadata.json
│               ├── [-rw-r--r--  630]  Vagrantfile
│               └── [-rw------- 1.6K]  vagrant_private_key
├── [drwxr-xr-x 4.0K]  data
│   ├── [-rw-r--r--  288]  checkpoint_cache
│   ├── [-rw-r--r--  293]  checkpoint_signature
│   └── [drwxr-xr-x 4.0K]  machine-index
│       └── [-rw-r--r--    0]  index.lock
├── [drwxr-xr-x 4.0K]  gems
│   └── [drwxr-xr-x 4.0K]  2.4.4
├── [-rw------- 1.6K]  insecure_private_key
├── [drwxr-xr-x 4.0K]  rgloader
│   └── [-rw-r--r--  354]  loader.rb
├── [-rw-r--r--    3]  setup_version
└── [drwxr-xr-x 4.0K]  tmp

11 directories, 13 files

```

```sh
devel1@VBXLFD271:~/LDF271/labs/lab1$ more $HOME/.vagrant.d/boxes/fabric-fundamentals/0/virtualbox/include/_Vagrantfile 
$script = <<SCRIPT
cd /home/vagrant/fabric-fundamentals
. /home/vagrant/.nvm/nvm.sh
nohup mdserver &> ~/mdserver.log &
SCRIPT

Vagrant.configure('2') do |config|
  config.ssh.username = "vagrant"
  config.vm.network "forwarded_port", guest: 3000, host: 3000, host_ip: "127.0.0.1", auto_correct: true
  config.vm.network "forwarded_port", guest: 3333, host: 3333, host_ip: "127.0.0.1", auto_correct: true
  config.vm.network "forwarded_port", guest: 8080, host: 8080, host_ip: "127.0.0.1", auto_correct: true
  config.vm.provider "virtualbox" do |vb|
#    vb.customize [ "modifyvm", :id, "--uartmode1", "file", "fabric-labs.log" ]
    vb.customize [ 'modifyvm', :id, '--uartmode1', 'disconnected']
  end
  config.vm.provision :shell, inline: $script, privileged: false
end

```


```sh
devel1@VBXLFD271:~$ vagrant box list --box-info
fabric-fundamentals (virtualbox, 0)
```

### 4. Initialize your Vagrant environment by running the following command:
```sh
vagrant init fabric-fundamentals
```

```sh
devel1@VBXLFD271:~$ cd LDF271/labs/lab1/
devel1@VBXLFD271:~/LDF271/labs/lab1$ pwd
/home/devel1/LDF271/labs/lab1
```

```sh
devel1@VBXLFD271:~/LDF271/labs/lab1$ vagrant init --help
Usage: vagrant init [options] [name [url]]

Options:

        --box-version VERSION        Version of the box to add
    -f, --force                      Overwrite existing Vagrantfile
    -m, --minimal                    Use minimal Vagrantfile template (no help comments). Ignored with --template
        --output FILE                Output path for the box. '-' for stdout
        --template FILE              Path to custom Vagrantfile template
    -h, --help                       Print this help
```


This creates a new Vagrantfile in the current directory - which describes the type of virtual machine
the project will use and how to configure and provision the virtual machine. You may modify this file if
you need to.
devel1@VBXLFD271:~/LDF271/labs/lab1$ vagrant init fabric-fundamentals
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "fabric-fundamentals"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end

```

### 5. Now you are ready to run the Vagrant virtual machine/box, by running:
```sh
vagrant up
```

```sh
devel1@VBXLFD271:~/LDF271/labs/lab1$ vagrant up
No usable default provider could be found for your system.

Vagrant relies on interactions with 3rd party systems, known as
"providers", to provide Vagrant with resources to run development
environments. Examples are VirtualBox, VMware, Hyper-V.

The easiest solution to this message is to install VirtualBox, which
is available for free on all major platforms.

If you believe you already have a provider available, make sure it
is properly installed and configured. You can see more details about
why a particular provider isn't working by forcing usage with
`vagrant up --provider=PROVIDER`, which should give you a more specific
error message for that particular provider.

```
### Instalando el "provider" virtualbox 

```sh
devel1@VBXLFD271:~/LDF271/labs/lab1$ sudo apt install virtualbox
[sudo] contraseña para devel1: 
Leyendo lista de paquetes... Hecho
Creando árbol de dependencias       
Leyendo la información de estado... Hecho
Se instalarán los siguientes paquetes adicionales:
  build-essential dkms dpkg-dev fakeroot g++ g++-8 gcc gcc-8 libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libasan5 libatomic1 libc-dev-bin
  libc6-dev libdouble-conversion1 libfakeroot libgcc-8-dev libgsoap-2.8.60 libitm1 liblsan0 libmpx2 libqt5core5a libqt5dbus5 libqt5gui5 libqt5network5 libqt5opengl5
  libqt5printsupport5 libqt5svg5 libqt5widgets5 libqt5x11extras5 libquadmath0 libsdl1.2debian libstdc++-8-dev libtsan0 libubsan1 libvncserver1 libxcb-xinerama0
  linux-libc-dev make manpages-dev qt5-gtk-platformtheme qttranslations5-l10n virtualbox-dkms virtualbox-qt
Paquetes sugeridos:
  menu debian-keyring g++-multilib g++-8-multilib gcc-8-doc libstdc++6-8-dbg gcc-multilib autoconf automake libtool flex bison gcc-doc gcc-8-multilib gcc-8-locales
  libgcc1-dbg libgomp1-dbg libitm1-dbg libatomic1-dbg libasan5-dbg liblsan0-dbg libtsan0-dbg libubsan1-dbg libmpx2-dbg libquadmath0-dbg glibc-doc
  qt5-image-formats-plugins qtwayland5 libstdc++-8-doc make-doc vde2 virtualbox-guest-additions-iso
Se instalarán los siguientes paquetes NUEVOS:
  build-essential dkms dpkg-dev fakeroot g++ g++-8 gcc gcc-8 libalgorithm-diff-perl libalgorithm-diff-xs-perl libalgorithm-merge-perl libasan5 libatomic1 libc-dev-bin
  libc6-dev libdouble-conversion1 libfakeroot libgcc-8-dev libgsoap-2.8.60 libitm1 liblsan0 libmpx2 libqt5core5a libqt5dbus5 libqt5gui5 libqt5network5 libqt5opengl5
  libqt5printsupport5 libqt5svg5 libqt5widgets5 libqt5x11extras5 libquadmath0 libsdl1.2debian libstdc++-8-dev libtsan0 libubsan1 libvncserver1 libxcb-xinerama0
  linux-libc-dev make manpages-dev qt5-gtk-platformtheme qttranslations5-l10n virtualbox virtualbox-dkms virtualbox-qt
0 actualizados, 46 nuevos se instalarán, 0 para eliminar y 0 no actualizados.
Se necesita descargar 64,8 MB de archivos.
Se utilizarán 281 MB de espacio de disco adicional después de esta operación.
¿Desea continuar? [S/n] 

... ... ...
... ... ...

Configurando build-essential (12.5ubuntu2) ...
Configurando virtualbox-dkms (5.2.18-dfsg-2) ...
Loading new virtualbox-5.2.18 DKMS files...
Building for 4.18.0-10-generic
Building initial module for 4.18.0-10-generic
Done.

vboxdrv:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.18.0-10-generic/updates/dkms/

vboxnetadp.ko:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.18.0-10-generic/updates/dkms/

vboxnetflt.ko:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.18.0-10-generic/updates/dkms/

vboxpci.ko:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.18.0-10-generic/updates/dkms/

depmod.......

DKMS: install completed.
Configurando virtualbox (5.2.18-dfsg-2) ...
vboxweb.service is a disabled or a static unit, not starting it.
Configurando virtualbox-qt (5.2.18-dfsg-2) ...
Procesando disparadores para libc-bin (2.28-0ubuntu1) ...
Procesando disparadores para systemd (239-7ubuntu10) ...

```
### Reintentando comando `vagrant up` ... 

```sh
devel1@VBXLFD271:~/LDF271/labs/lab1$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'fabric-fundamentals'...
Progress: 10%
==> default: Matching MAC address for NAT networking...
==> default: Setting the name of the VM: lab1_default_1540305832647_20808
Vagrant is currently configured to create VirtualBox synced folders with
the `SharedFoldersEnableSymlinksCreate` option enabled. If the Vagrant
guest is not trusted, you may want to disable this option. For more
information on this option, please refer to the VirtualBox manual:

  https://www.virtualbox.org/manual/ch04.html#sharedfolders

This option can be disabled globally with an environment variable:

  VAGRANT_DISABLE_VBOXSYMLINKCREATE=1

or on a per folder basis within the Vagrantfile:

  config.vm.synced_folder '/host/path', '/guest/path', SharedFoldersEnableSymlinksCreate: false
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 3000 (guest) => 3000 (host) (adapter 1)
    default: 3333 (guest) => 3333 (host) (adapter 1)
    default: 8080 (guest) => 8080 (host) (adapter 1)
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
There was an error while executing `VBoxManage`, a CLI used by Vagrant
for controlling VirtualBox. The command and stderr is shown below.

Command: ["startvm", "6fbd1f76-1c11-41e2-b987-0a263fe3642f", "--type", "headless"]

Stderr: VBoxManage: error: VT-x is not available (VERR_VMX_NO_VMX)
VBoxManage: error: Details: code NS_ERROR_FAILURE (0x80004005), component ConsoleWrap, interface IConsole


```
