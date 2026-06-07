# Pasta de Evidências dos Testes

Esta pasta contém as capturas de tela (screenshots) dos testes de conectividade (ping) e acesso remoto (SSH) que validam o ambiente de rede do Grupo 4.

## Como adicionar as imagens

### 1. Formato das imagens
Use screenshots em formato **PNG** ou **JPG**. Recomendado: **PNG** (melhor compressão).

### 2. Convenção de nomenclatura
Siga o padrão exato usado nos arquivos de teste:

**Para testes de ping:**
- `ping-[origem]-[destino]-[tipo].png`
- Exemplos:
  - `ping-g4pc1vm1-g4pc1vm2-ip.png`
  - `ping-g4pc1vm1-g4pc1vm2-hostname.png`
  - `ping-g4pc1vm1-g4pc1vm2-fqdn.png`

**Para testes de SSH:**
- `ssh-[usuario]-[destino]-[tipo].png`
- Exemplos:
  - `ssh-isaque-g4pc2vm1-ip.png`
  - `ssh-isaque-g4pc2vm1-hostname.png`
  - `ssh-andrezza-g4pc1vm1-fqdn.png`

### 3. Como colocar a imagem no arquivo markdown

No arquivo `.md`, a sintaxe é:
```markdown
![Descrição da imagem](../evidencias/nome-do-arquivo.png)
```

**Exemplo prático:**

Se você tirou um screenshot do ping para G4-PC1-VM2 por IP, salve o arquivo como:
```
evidencias/ping-g4pc1vm1-g4pc1vm2-ip.png
```

E no arquivo `docs/testes-ping.md`, a imagem já está pronta para ser inserida:
```markdown
![Resultado: ping para G4-PC1-VM2 por IP](../evidencias/ping-g4pc1vm1-g4pc1vm2-ip.png)
```

### 4. No Git
A pasta `evidencias/` deve ser versionada (as imagens serão commitadas). Não esqueça de fazer:
```bash
git add evidencias/
git commit -m "docs: adiciona evidências dos testes de ping e SSH"
```

---

## Estrutura esperada
```
evidencias/
├── ping-g4pc1vm1-g4pc1vm2-ip.png
├── ping-g4pc1vm1-g4pc1vm2-hostname.png
├── ping-g4pc1vm1-g4pc1vm2-fqdn.png
├── ... (outros testes de ping)
├── ssh-isaque-g4pc2vm1-ip.png
├── ssh-isaque-g4pc2vm1-hostname.png
├── ... (outros testes de SSH)
└── README.md (este arquivo)
```
