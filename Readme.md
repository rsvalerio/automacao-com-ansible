## 

## Instalação do Ambiente

 - #### Virtual Box
 - #### Vagrant
 - ### Baixar uma box/vm vagrant
```
vagrant box add centos7 https://f0fff3908f081cb6461b407be80daf97f07ac418.googledrive.com/host/0BwtuV7VyVTSkUG1PM3pCeDJ4dVE/centos7.box
```

 - ### Ligar a VM e acessá-la
```
vagrant up
vagrant ssh
```

## Ansible

#### Definições:

 - "Ansible is a radically simple IT automation engine that automates cloud provisioning, configuration management, application deployment, intra-service orchestration, and many other IT needs." -> 
[http://www.ansible.com/how-ansible-works](http://www.ansible.com/how-ansible-works)

 - "Ansible is a free software platform for configuring and managing computers. It combines multi-node software deployment, ad hoc task execution, and configuration management.[1] It manages nodes over SSH or PowerShell and requires Python (2.4 or later) [2] to be installed on them. Modules work over JSON and standard output and can be written in any programming language. The system uses YAML to express reusable descriptions of systems.[3]" -> [https://en.wikipedia.org/wiki/Ansible_(software)](https://en.wikipedia.org/wiki/Ansible_%28software%29)

 - Um dos principais conceitos relacionados ás ferramentas 

#### Principais Componentes

 1. Inventory
 2. Module
 3. Roles
 4. Playbook
 5. Vars
 6. Tasks
 7. Handlers
 

 
##### Inventory
	
Arquivo texto simples com o(s) IP(s) da(s) máquina(s) que serão manipuladas

Pode ter qualquer nome, é passado como paramêtro -i
	
```
ansible-playbook -i hosts
ansible-playbook -i maquinas_antigas
```
	
Conteúdo do arquivo hosts

```
[web]
192.168.100.135
	
[database]
192.168.100.150
```
	
Pode ser organizado por hosts e/ou grupos, possibilitando por exemplo a segregação de variáveis por ambiente ambiente por exmemplo
	
```
├── group_vars
│   └── variaveis.yml
├── homologacao
│   ├── group_vars
│   │   └── variaveis.yml
│   └── inventory
└── producao
    ├── group_vars
    │   └── variaveis.yml
    └── inventory

```

Passando o parâmetro -i homologacao para o ansible-playbook, é suficiente para que as variáveis definidas no ambiente de homologacao sejam utilizadas, mudando para -i producao, serão utilizados os valores definidos para este ambiente.
	
Documentação: [http://docs.ansible.com/ansible/intro_inventory.html](http://docs.ansible.com/ansible/intro_inventory.html)


##### Módulos

Componente de alto-nível, é a camada de abstração do que fazer, por exemplo:
Para iniciar um serviço no centos7:

```
systemctl enable tomcat
systemctl start tomcat
```

Para iniciar um serviço no ubuntu/cento6:

```
services tomcat start
```

O módulo service, abstrai o gerenciador de serviços utilizado pelo Sistema Operacional:

```
- name: Iniciar o serviço do tomcat
  service: name=tomcat state=started enabled=yes
```

É muito fácil criar nosso próprio módulo, basicamente um aqruivo python na pasta library e pronto.

```
- name: Recuperar os usuarios do AD
  acesso_ad: grupo=AdministradoresLinux state=absent
```

Lista com os módulos existentes
[http://docs.ansible.com/ansible/modules_by_category.html](http://docs.ansible.com/ansible/modules_by_category.html)

Categorias de módulos existentes atualmente:

 - Cloud Modules
 - Clustering Modules
 - Commands Modules
 - Database Modules
 - Files Modules
 - Inventory Modules
 - Messaging Modules
 - Monitoring Modules
 - Network Modules
 - Notification Modules
 - Packaging Modules
 - Source Control Modules
 - System Modules
 - Utilities Modules
 - Web Infrastructure Modules
 - Windows Modules



##### Playbook
	
É onde a coisa acontece :)

Onde são escritas as Tasks, criadas variáveis, condicionais, etc.

Anatomia de um playbook





