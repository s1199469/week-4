#  WEEK-4 Opdracht 1
----

vraag: 2x VM met:
- automatisch aangemaakte inventory
- gebruik van roles
- aanmaken van Ansible inventory file met group-variabelen
- uitvoeren Ansible playbook waarbij iedere group de packages krijgt die in de group-variabelen zijn gedefinieerd

----
## Issues

- Het is niet gelukt om de host-groepen in de inventory automatisch te vullen op basis van een vm_group variabelen
Als work-around heb ik de server-identifiers als array in lokale variabelen geplaatst:

locals {

  web_ips=[esxi_guest.Server1[0].ip_address]
  
  db_ips=[esxi_guest.Server2[0].ip_address]
  
}

- update mysql root passwordlukt niet 


----
## Status
Deployment werkt en maakt gebruik van de Ansible roles

----
# automatisch genereren van Ansible inventory file
Het lukt niet om deze te vullen op basis van servernaam of groep-variabelen. Ik heb de inhoud deels handmatig ingevuld maar wel met gebruik van variabelen. 

# Roles
De in de opdracht opgegeven roles zijn per host-group in variabelen geplaatst. Deze worden in de Ansible-playbook aangeroepen
Roles zijn aangemaakt op de beheer-vm met commando ansible role init. Deze maakt de folderstructuur en lege README files aan. Ik gebruik de verkenner van mobaXterm om de folders te kopieren naar de lokale GIT repo op mijn lokale werkstation.

# Gebruik van group-variabelen
De te installeren rollen worden automatisch als group-variabelen toegevoegd aan de inventory. De namen van de rollen staan gedefinieerd in de variables.tf en oef4.auto.tfvars files

# toevoegen in inventory file: 

resource "local_file" "ipaddresses" {

   content = <<-EOT
   
   [${var.vm1_group}]
   
   %{ for ip in local.db_ips }${ip}
   
   %{ endfor }
   
   [${var.vm1_group}:vars]
   
   vm1_role1=${var.vm1_role1}
   
   vm1_role2=${var.vm1_role2}
   
   vm1_role3=${var.vm1_role3}

   .....
   
   EOT


