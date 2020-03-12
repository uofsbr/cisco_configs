# SSH Access Configuration

## 0 - Definig a User
> Router(config)#**username** [*username*] **privilege** [*1-15*] **password** [*password*] 

## 1 - Definig a Host Name
> Router(config)#**hostname** [*hostname*]

## 2 - Definig a Domain-Name
> R1(config)#**ip domain-name** [*domain-name*]

## 3 - Generating keys
> R1(config)#**crypto key generate rsa**

		 The name for the keys will be: [hostname][domain-name]
		 Choose the size of the key modulus in the range of 360 to 2048 for your
		 General Purpose Keys. Choosing a key modulus greater than 512 may take
		 a few minutes.
		 How many bits in the modulus [512]: [360 - 2048]
		 % Generating 2048 bit RSA keys, keys will be non-exportable...[OK]

> R1(config)#

		 Mar 1 1:33:27.329: %SSH-5-ENABLED: SSH 1.99 has been enabled

## 4 - Setting SSH to Version 2
> R1(config)#**ip ssh version 2**

## 5 - Configuring Vty Lines
> R1(config)#**line vty** 0 4 

> R1(config-line)#**transport input ssh**

> R1(config-line)#**login local**

> R1(config-line)# **exec-timeout** [10] [0] (M, S) (Optional)

## 6 - SSH Public Key Authentication
### SSH key pair generation on Linux:
#### Default Key Name
 > user@host:~# ssh-keygen -t rsa -b 4096

 > user@host:~# ls

		id_rsa id_rsa.pub

> user@host:~# fold -b -w 72 /home/user/.ssh/id_rsa.pub

> user@host:~# ssh [*user*]@[*ip*]

#### New Key Name
 > user@host:~# ssh-keygen -t rsa -b 4096

> user@host:~# ls

		id_rsa id_rsa.pub new-key new-key.pub

> user@host:~# ssh [*user*]@[*ip*] -i new-key

> user@host:~# fold -b -w 72 /home/user/.ssh/new-key.pub

### Inserting Key on Device
> R1(config)#**ip ssh pubkey-chain**

> R1(conf-ssh-pubkey)#**username** [*username*]

> R1(conf-ssh-pubkey-user)#**key-string**

> [*paste public key on next line*]
