# Lab 5 : Création d'un Vagrantfile Multi-Machine Simple avec Ubuntu Jammy64

## 🌟 Objectif

Ce laboratoire a pour but de créer un **Vagrantfile multi-machine** simple, utilisant **Ubuntu Jammy64** (Ubuntu 22.04 LTS), permettant de déployer plusieurs machines virtuelles sur un réseau privé.

## 📊 Prérequis

Assurez-vous d'avoir les outils suivants installés :

- **Vagrant** : Gestionnaire de machines virtuelles
- **VirtualBox** : Fournisseur de machines virtuelles
- Une connexion Internet fonctionnelle

## 🚀 Étapes du Lab

### 1. Initialisation du projet

1. Créez un dossier pour le projet :

   ```bash
   mkdir lab-5 && cd lab-5
   ```

2. Initialisez le projet Vagrant :

   ```bash
   vagrant init
   ```

---

### 2. Configuration du Vagrantfile

Utilisez le Vagrantfile ci-dessous pour configurer trois machines virtuelles (« lb », « web1 » et « web2 ») :

```ruby
# Variables pour la configuration commune
CPU = 2
RAM = "2048"
OS = "ubuntu/jammy64"

Vagrant.configure("2") do |config|
  # Configuration commune pour toutes les machines
  config.vm.provider "virtualbox" do |vb|
    vb.memory = RAM
    vb.cpus = CPU
  end

  # Machine 1 : Load Balancer (lb)
  config.vm.define "lb" do |lb|
    lb.vm.box = OS
    lb.vm.network "private_network", ip: "10.0.0.10"
  end

  # Machine 2 : Web Server 1 (web1)
  config.vm.define "web1" do |web1|
    web1.vm.box = OS
    web1.vm.network "private_network", ip: "10.0.0.11"
  end

  # Machine 3 : Web Server 2 (web2)
  config.vm.define "web2" do |web2|
    web2.vm.box = OS
    web2.vm.network "private_network", ip: "10.0.0.12"
  end
end
```

---

### 3. Déploiement des machines virtuelles

1. Lancez toutes les machines :

   ```bash
   vagrant up
   ```

2. Attendez que toutes les machines soient démarrées et provisionnées.

3. Connectez-vous à une machine via SSH :

   ```bash
   vagrant ssh lb
   ```

   Remplacez `lb` par `web1` ou `web2` pour accéder à une autre machine.

---

### 4. Tester la connectivité

1. Depuis la machine `lb`, testez la connexion vers `web1` et `web2` :

   ```bash
   ping 10.0.0.11
   ping 10.0.0.12
   ```

2. Vérifiez que toutes les machines peuvent communiquer entre elles.

---

## 🔧 Commandes Utiles

| Commande                        | Description                              |
|---------------------------------|------------------------------------------|
| `vagrant up`                    | Démarre toutes les machines virtuelles. |
| `vagrant ssh <machine_name>`    | Accède à une machine spécifique via SSH.|
| `vagrant halt`                  | Arrête toutes les machines virtuelles.  |
| `vagrant destroy`               | Supprime toutes les machines.           |

---

## 📈 Résultat Attendu

- Trois machines virtuelles configurées :
  - `lb` : Load Balancer avec l'IP **10.0.0.10**
  - `web1` : Serveur Web 1 avec l'IP **10.0.0.11**
  - `web2` : Serveur Web 2 avec l'IP **10.0.0.12**

- Toutes les machines peuvent communiquer via un réseau privé.

---

## 🌟 Conclusion

Ce laboratoire vous permet de :

1. Créer un environnement **multi-machine** simple avec Vagrant.
2. Configurer des machines avec des adresses IP statiques sur un réseau privé.
3. Comprendre les bases de l'utilisation d'un **Vagrantfile** multi-machine.

🚀 Félicitations ! Vous avez un environnement multi-machine fonctionnel !
