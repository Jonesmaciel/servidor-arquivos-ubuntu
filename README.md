📁 Projeto: Servidor de Arquivos

# Instalação do Samba
sudo apt update
sudo apt install samba -y

# Verificação status do serviço
systemctl status smbd

# Criação da pasta que será compartilhada 
mkdir -p criar a pasta e os diretórios
chmod 2775 permissão de leitura/escrita/execução para dono e grupo, leitura/execução para outros e o "2" faz com que novos arquivos criados dentro herdem o grupo da pasta
chown define dono do grupo

sudo mkdir -p /srv/samba/compartilhado
sudo chmod 2775 /srv/samba/compartilhado
sudo chown $USUARIO:$USUARIO /srv/samba/compartilhado

# Configuração do arquivo smb.conf
[Compartilhado] — o nome que vai aparecer na rede quando alguém procurar o compartilhamento
path — qual pasta física está sendo exposta
browseable = yes — o compartilhamento aparece listado quando alguém navega pela rede
read only = no — permite escrita, não só leitura
valid users — quem tem permissão de acessar

sudo nano /etc/samba/smb.conf

[Compartilhado]
   path = /srv/samba/compartilhado
   browseable = yes
   read only = no
   valid users = Nome do usuário (Exemplo "Jones")

# Criar um usuário Samba
sudo smbpasswd -a seu_usuario

# Aplicar e liberar o firewall
sudo systemctl restart smbd
sudo ufw enable
sudo ufw allow samba
sudo ufw status

# Testar seu host
Windows: Win+R → \\IP\Compartilhado
Mac: Finder → Ir → Conectar ao servidor → smb://IP/Compartilhado
Linux: gerenciador de arquivos → Outros locais → smb://IP/Compartilhado
   

   
