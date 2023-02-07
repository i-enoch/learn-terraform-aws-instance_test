# learn-terraform-aws-instance_test
Test des instances AWS

** Appel à la commande : terraform apply

 - L'ancien instance aws_instance.app_Server est detruite et remplacer par la nouvelle
 - Une instance aws_security_group est créée avant la nouvelle instance aws_instance.app_server
 - Une nouvelle instance aws_instance.app_server est créée après l'instance aws_security_group  

Plan: 2 to add, 0 to change, 1 to destroy.

Do you want to perform these actions?
    Enter a value: yes    

aws_instance.app_server: Destroying... [id=i-03d70698bd9e842aa]
aws_instance.app_server: Still destroying... [id=i-03d70698bd9e842aa, 10s elapsed]
aws_instance.app_server: Still destroying... [id=i-03d70698bd9e842aa, 20s elapsed]
aws_instance.app_server: Still destroying... [id=i-03d70698bd9e842aa, 30s elapsed]
aws_instance.app_server: Destruction complete after 31s
aws_security_group.instance: Creating...
aws_security_group.instance: Creation complete after 2s [id=sg-0112aecca5edaa958]
aws_instance.app_server: Creating...
aws_instance.app_server: Still creating... [10s elapsed]
aws_instance.app_server: Still creating... [20s elapsed]
aws_instance.app_server: Still creating... [30s elapsed]
aws_instance.app_server: Creation complete after 32s [id=i-092631adf0bdc23a2]

Apply complete! Resources: 2 added, 0 changed, 1 destroyed.

** Appel à la commande : terraform graph
La commande schématise les étapes d'exécution du plan appliqué par la commande "terraform apply" . Les différents appels au provider registry.terraform.io/hashicorp/aws et les dépendances entre les instances.

digraph {
        compound = "true"
        newrank = "true"
        subgraph "root" {
                "[root] aws_instance.app_server (expand)" [label = "aws_instance.app_server", shape = "box"]
                "[root] aws_security_group.instance (expand)" [label = "aws_security_group.instance", shape = "box"]
                "[root] provider[\"registry.terraform.io/hashicorp/aws\"]" [label = "provider[\"registry.terraform.io/hashicorp/aws\"]", shape = "diamond"]mond"]
                "[root] var.security_group_name" [label = "var.security_group_name", shape = "note"]
                "[root] aws_instance.app_server (expand)" -> "[root] aws_security_group.instance (expand)"
                "[root] aws_security_group.instance (expand)" -> "[root] provider[\"registry.terraform.io/hashicorp/aws\"]"
                "[root] aws_security_group.instance (expand)" -> "[root] var.security_group_name"
                "[root] provider[\"registry.terraform.io/hashicorp/aws\"] (close)" -> "[root] aws_instance.app_server (expand)"
                "[root] root" -> "[root] provider[\"registry.terraform.io/hashicorp/aws\"] (close)"
        }
}
                "[root] var.security_group_name" [label = "var.security_group_name", shape = "note"]
                "[root] aws_instance.app_server (expand)" -> "[root] aws_security_group.instance (expand)"
                "[root] aws_security_group.instance (expand)" -> "[root] provider[\"registry.terraform.io/hashicorp/aws\"]"
                "[root] aws_security_group.instance (expand)" -> "[root] var.security_group_name"
                "[root] provider[\"registry.terraform.io/hashicorp/aws\"] (close)" -> "[root] aws_instance.app_server (expand)"
                "[root] root" -> "[root] provider[\"registry.terraform.io/hashicorp/aws\"] (close)"
        }
}