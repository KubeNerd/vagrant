
# Guia de Uso do Vagrant

## Introdução

Vagrant é uma ferramenta open-source que ajuda a criar e administrar máquinas virtuais em diferentes plataformas (Windows, Linux, etc.).  
Ele utiliza arquivos de configuração, chamados **Vagrantfile**, para definir as especificações da máquina virtual e automatizar tarefas de provisionamento.  
O Vagrant também permite gerenciar essas máquinas virtuais por meio de uma interface de linha de comando, oferecendo comandos para iniciar, parar, destruir e acessar as máquinas.

Para instalar o Vagrant, acesse: [Instalação do Vagrant](https://developer.hashicorp.com/vagrant/install).

---

## Conceitos Fundamentais

### Boxes

Os **Boxes** são imagens de máquinas virtuais que podem ser usadas no Vagrant.  
Eles podem ser baixados da página [Discover Vagrant Boxes](https://portal.cloud.hashicorp.com/vagrant/discover?query=) e variam conforme o provider escolhido.

### Providers

Os **Providers** são os mecanismos ou hipervisores que gerenciam as máquinas virtuais.  
Exemplos comuns incluem VirtualBox, VMware e Docker.

---

## Criando sua Primeira Máquina Virtual

### Passo 1: Criar o Vagrantfile

No diretório desejado, execute o comando para inicializar o Vagrantfile com a box `ubuntu/trusty64`:

```sh
vagrant init ubuntu/trusty64
```

- **Observação**: Caso já exista um Vagrantfile no diretório, renomeie, mova ou exclua-o.

### Passo 2: Subir a Máquina Virtual

Para iniciar a máquina virtual, execute:

```sh
vagrant up
```

O Vagrant irá:
- Configurar a VM, incluindo rede.
- Instalar o SSH.
- Montar a pasta compartilhada (o diretório atual).

### Passo 3: Comandos Úteis

- **Verificar status da VM**:
  ```sh
  vagrant status
  ```

- **Parar a VM (Stop)**:
  ```sh
  vagrant halt
  ```

- **Excluir a VM (Remove)**:
  ```sh
  vagrant destroy
  ```

- **Reiniciar a VM após alterações no Vagrantfile**:
  ```sh
  vagrant reload
  ```

---

## Personalizando a Máquina Virtual

O Vagrant permite o provisionamento das máquinas virtuais usando scripts de shell ou ferramentas como Ansible, Chef e Puppet.  
Abaixo estão exemplos para usar scripts de shell.

### Provisionamento com Script Inline

Inclua o script diretamente no **Vagrantfile**:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y nginx
  SHELL
end
```

### Provisionamento com Script Externo

Salve o script em um arquivo, por exemplo, `script.sh`:

**Arquivo `script.sh`:**
```sh
#!/bin/bash
apt-get update
apt-get install -y apache2
```

Inclua a referência ao script no **Vagrantfile**:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"
  config.vm.provision "shell", path: "script.sh"
end
```

---

## Próximos Passos

Com os conceitos básicos em mãos, explore mais recursos do Vagrant, como:
- Configuração de redes privadas ou públicas.
- Uso de múltiplas VMs no mesmo Vagrantfile.
- Provisionamento avançado com Ansible, Puppet ou Chef.

Para saber mais sobre esse tipo de ferramenta: [Documentação Oficial do Vagrant](https://developer.hashicorp.com/vagrant/docs)
