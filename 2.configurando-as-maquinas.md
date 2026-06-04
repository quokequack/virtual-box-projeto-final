Após a criação da máquina, é preciso fazer as configurações de rede dela.

<ol>
  <li> Logar via terminal com o usuário e senha administrador criados na etapa anterior </li>
  <li> Criar o usuário `redes` com a senha `admin@Lab92`, conforme solicitado pelo professor: </li> <code> sudo adduser redes </code>
  <li> Dar para esse usuário permissões de admin (sudo) com o comando: </li> <code> sudo usermod -aG sudo redes </code>
  <li> Criar as pastas labredes/VM/BSI/{nome_do_aluno}</li>
  <li> Criar usuários para os componentes do grupo e adicioná-los no grupo de redes: </li> <code> sudo usermod -aG redes aluno </code>
  <li> Instalar o virtual-box-extension-pack via: </li>
  <pre><code>
      su redes 
      sudo apt install virtualbox-ext-pack
    </code></pre>
  <li> Instalar as ferramentas de rede: </li> <code> sudo apt install net-tools -y </code>
  <li> Ir na pasta /etc/netplan/ para encontrar o arquivo .yaml onde o ubuntu faz a configuração de rede d VM</li>
  <li> Modificar o arquivo através do vim: </li> <code> sudo vim /etc/netplan/nome_do_arquivo </code>
  <li> Adicionar as informações: </li>
  <pre><code>
    network:
    ethernets:
        enp0s3:                           # nome da interface que está sendo configurada. Verifique com o comando 'ifconfig -a'
            addresses: [172.17.0.1/24]    # IP e Máscara do Host.
            gateway4: 172.17.0.1          # IP do Gateway
            dhcp4: false                  # dhcp4 false -> cliente DHCP está desabilitado, logo o utilizará o IP do campo 'addresses'
    version: 2
  </code></pre>
  <li> Confirmar as mudanças com: </li> <code> sudo netplan apply </code>
  <li> Para testar a conexão via rede com outras máquinas: </li> <code> ping endereco_outra_maquina </code>
</ol>
