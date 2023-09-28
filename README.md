# Notas Kali

Anotações para que eu não precise decorar tudo que faço.

<details>
<summary>
Habilitar bluetooth
</summary>

## Habilitar bluetooth

O Kali vem com um pacote de dependências para interagir com conexões bluetooth e um serviço configurado.


```bash
cat /etc/systemd/system/bluetooth.target.wants/bluetooth.service
```

Porém este serviço está desabilitado por padrão.

É necessário habilitar o serviço de bluetooth para que este comece a funcionar sempre que o sistema for iniciado.

```bash
sudo systemctl enable bluetooth.service
```

Caso contrário, é preciso iniciar o serviço sempre que o bluetooth for usado.

```bash
sudo systemctl start bluetooth.service
```

**Referências**

- https://www.kali.org/tools/bluez/
</details>

---

<details>
<summary>
Instalar libgconf-2-4
</summary>

## Instalar libgconf-2-4

Este dependência não está mais disponível nos repositórios ppa do Kali e é requerida por vários aplicativos proprietários, tais como Discord e Spotify.

Este pacote está disponível no Ubuntu, então teoricamente é possível adicionar o repositório Universe do Ubuntu no Kali e rodar um `sudo apt install libgconf-2-4`. No entanto, isto é altamente desencorajado na documentação do Kali, uma vez que nem todos os pacotes do Ubuntu são compatíveis com o Kali, apesar de ambos serem baseados no Debian. 

Uma alternativa mais segura é baixar os pacotes .deb e instalá-los localmente.

```bash
cd ~/Downloads
wget wget http://ftp.de.debian.org/debian/pool/main/g/gconf/gconf2-common_3.2.6-8_all.deb
wget wget http://ftp.de.debian.org/debian/pool/main/g/gconf/libgconf-2-4_3.2.6-8_amd64.deb
sudo apt install ./gconf2-common_3.2.6-8_all.deb
sudo apt install ./libgconf-2-4_3.2.6-8_amd64.deb
```

**Referências**

- https://www.kali.org/docs/general-use/kali-linux-sources-list-repositories/#non-kali-repositories
- https://pkgs.org/download/libgconf-2-4
</details>

---

<details>
<summary>
Instalar Docker
</summary>

## Instalar Docker

**Adicionar fonte ppa do Docker**

```bash
printf '%s\n' "deb https://download.docker.com/linux/debian bookworm stable" | sudo tee /etc/apt/sources.list.d/docker-ce.list
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker-ce-archive-keyring.gpg
sudo apt update
```

**Instalar serviços**

```bash
sudo apt install -y docker.io docker-ce docker-ce-cli containerd.io
```

**Adicionar usuário ao grupo do Docker**

(para não ter que usar sudo toda vez)

```bash
sudo usermod -aG docker $USER
```
**Iniciar serviço**

```bash
sudo systemctl enable docker --now
```

**Rebootar o computador**

(Para a adição do usuário ao grupo do Docker ter efeito)

```bash
reboot
```

**Testar se deu certo**

```bash
docker run hello-world
```

**Referências**

- https://www.kali.org/docs/containers/installing-docker-on-kali/
- https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
</details>
