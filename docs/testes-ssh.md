# Testes de Acesso Remoto (SSH)

Nesta seção são apresentados os resultados dos testes de acesso SSH das VMs do Grupo 4, validando:
- Acesso **por IP**
- Acesso **por hostname** (nome curto)
- Acesso **por FQDN** (nome totalmente qualificado)
- Funcionamento dos **usuários criados**

Para cada teste, executou-se o comando:
```bash
ssh [usuario]@[alvo]
```

---

## 1. Testes de Andrezza (andrezza.magalhaes)

### Em G4-PC1-VM1

Os testes foram executados e documentados nas imagens abaixo:

#### Por IP (192.168.26.49)
```bash
ssh andrezza.magalhaes@192.168.26.49
```
![Andrezza → G4-PC1-VM1 (IP)](../evidencias/ssh-andrezza-g4pc1vm1-ip.png)

#### Por hostname (g4-pc1-vm1)
```bash
ssh andrezza.magalhaes@g4-pc1-vm1
```
![Andrezza → G4-PC1-VM1 (hostname)](../evidencias/ssh-andrezza-g4pc1vm1-hostname.png)

#### Por FQDN
```bash
ssh andrezza.magalhaes@g4-pc1-vm1.grupo4-bsi-26-1.maceio.lab
```
![Andrezza → G4-PC1-VM1 (FQDN)](../evidencias/ssh-andrezza-g4pc1vm1-fqdn.png)

---

### Em G4-PC1-VM2

Os testes foram executados e documentados nas imagens abaixo:
```bash
ssh andrezza.magalhaes@192.168.26.50
```
![Andrezza → G4-PC1-VM2 (IP)](../evidencias/ssh-andrezza-g4pc1vm2-ip.png)

#### Por hostname (g4-pc1-vm2)
```bash
ssh andrezza.magalhaes@g4-pc1-vm2
```
![Andrezza → G4-PC1-VM2 (hostname)](../evidencias/ssh-andrezza-g4pc1vm2-hostname.png)

#### Por FQDN
```bash
ssh andrezza.magalhaes@g4-pc1-vm2.grupo4-bsi-26-1.maceio.lab
```
![Andrezza → G4-PC1-VM2 (FQDN)](../evidencias/ssh-andrezza-g4pc1vm2-fqdn.png)

---

## 2. Testes de Isaque (isaque.braga)

### Em G4-PC2-VM1

Os testes foram executados e documentados nas imagens abaixo:
```bash
ssh isaque.braga@192.168.26.51
```
![Isaque → G4-PC2-VM1 (IP)](../evidencias/ssh-isaque-g4pc2vm1-ip.png)

#### Por hostname (g4-pc2-vm1)
```bash
ssh isaque.braga@g4-pc2-vm1
```
![Isaque → G4-PC2-VM1 (hostname)](../evidencias/ssh-isaque-g4pc2vm1-hostname.png)

#### Por FQDN
```bash
ssh isaque.braga@g4-pc2-vm1.grupo4-bsi-26-1.maceio.lab
```
![Isaque → G4-PC2-VM1 (FQDN)](../evidencias/ssh-isaque-g4pc2vm1-fqdn.png)

---

### Em G4-PC2-VM2

Os testes foram executados e documentados nas imagens abaixo:
```bash
ssh isaque.braga@192.168.26.52
```
![Isaque → G4-PC2-VM2 (IP)](../evidencias/ssh-isaque-g4pc2vm2-ip.png)

#### Por hostname (g4-pc2-vm2)
```bash
ssh isaque.braga@g4-pc2-vm2
```
![Isaque → G4-PC2-VM2 (hostname)](../evidencias/ssh-isaque-g4pc2vm2-hostname.png)

#### Por FQDN
```bash
ssh isaque.braga@g4-pc2-vm2.grupo4-bsi-26-1.maceio.lab
```
![Isaque → G4-PC2-VM2 (FQDN)](../evidencias/ssh-isaque-g4pc2vm2-fqdn.png)

---

## 3. Testes de Maria (maria.santos)

### Em G4-PC3-VM1

Os testes foram executados e documentados nas imagens abaixo:
```bash
ssh maria.santos@192.168.26.53
```
![Maria → G4-PC3-VM1 (IP)](../evidencias/ssh-maria-g4pc3vm1-ip.png)

#### Por hostname (g4-pc3-vm1)
```bash
ssh maria.santos@g4-pc3-vm1
```
![Maria → G4-PC3-VM1 (hostname)](../evidencias/ssh-maria-g4pc3vm1-hostname.png)

#### Por FQDN
```bash
ssh maria.santos@g4-pc3-vm1.grupo4-bsi-26-1.maceio.lab
```
![Maria → G4-PC3-VM1 (FQDN)](../evidencias/ssh-maria-g4pc3vm1-fqdn.png)

---

### Em G4-PC3-VM2

Os testes foram executados e documentados nas imagens abaixo:
```bash
ssh maria.santos@192.168.26.54
```
![Maria → G4-PC3-VM2 (IP)](../evidencias/ssh-maria-g4pc3vm2-ip.png)

#### Por hostname (g4-pc3-vm2)
```bash
ssh maria.santos@g4-pc3-vm2
```
![Maria → G4-PC3-VM2 (hostname)](../evidencias/ssh-maria-g4pc3vm2-hostname.png)

#### Por FQDN
```bash
ssh maria.santos@g4-pc3-vm2.grupo4-bsi-26-1.maceio.lab
```
![Maria → G4-PC3-VM2 (FQDN)](../evidencias/ssh-maria-g4pc3vm2-fqdn.png)

---

## 4. Testes de Renilson (renilson.santos)

### Em G4-PC4-VM1

Os testes foram executados e documentados nas imagens abaixo:
```bash
ssh renilson.santos@192.168.26.55
```
![Renilson → G4-PC4-VM1 (IP)](../evidencias/ssh-renilson-g4pc4vm1-ip.png)

#### Por hostname (g4-pc4-vm1)
```bash
ssh renilson.santos@g4-pc4-vm1
```
![Renilson → G4-PC4-VM1 (hostname)](../evidencias/ssh-renilson-g4pc4vm1-hostname.png)

#### Por FQDN
```bash
ssh renilson.santos@g4-pc4-vm1.grupo4-bsi-26-1.maceio.lab
```
![Renilson → G4-PC4-VM1 (FQDN)](../evidencias/ssh-renilson-g4pc4vm1-fqdn.png)

---

### Em G4-PC4-VM2

Os testes foram executados e documentados nas imagens abaixo:
```bash
ssh renilson.santos@192.168.26.56
```
![Renilson → G4-PC4-VM2 (IP)](../evidencias/ssh-renilson-g4pc4vm2-ip.png)

#### Por hostname (g4-pc4-vm2)
```bash
ssh renilson.santos@g4-pc4-vm2
```
![Renilson → G4-PC4-VM2 (hostname)](../evidencias/ssh-renilson-g4pc4vm2-hostname.png)

#### Por FQDN
```bash
ssh renilson.santos@g4-pc4-vm2.grupo4-bsi-26-1.maceio.lab
```
![Renilson → G4-PC4-VM2 (FQDN)](../evidencias/ssh-renilson-g4pc4vm2-fqdn.png)

---

## 5. Resumo

**Total de testes:** 24 prints (8 máquinas × 3 tipos cada = IP, hostname, FQDN)

Todos os testes de SSH foram bem-sucedidos, demonstrando:
- ✅ Acesso remoto funcionando com todos os usuários
- ✅ Resolução de nomes por IP habilitada
- ✅ Resolução de nomes por hostname habilitada
- ✅ Resolução de nomes por FQDN habilitada
- ✅ Autenticação funcionando em todas as máquinas
- ✅ Comunicação SSH segura estabelecida
