# Como fiz o deploy
- Configurar servidor
```shell
# instalando libs
sudo apt update
sudo apt upgrade
sudo apt install nginx
cd /var/www/html
sudo mv html/ html_antigo
git clone https://github.com/torneseumprogramador/app-react-build-deploy-rust.git html

```

- Alterar nginx para 404 enviar para index.html
```nginx
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
            try_files $uri $uri/ /index.html;
    }
}
```

```shell
sudo vim /etc/nginx/sites-available/default # coloque o nginx configurado aqui
sudo systemctl restart nginx
```

# OBS: não esqueça de librar a porta 80 no security group AWS