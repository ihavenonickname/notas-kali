# Utilizar autenticação SSH no GitHub

**Gerar um par de chaves RSA**

```bash
ssh-keygen -t rsa
```

**Adicionar a chave no GitHub**

Adicionar a chave pública em https://github.com/settings/keys

A chave pode ser obtida em

```bash
cat /home/gabriel/.ssh/id_rsa.pub
```

**Setar o modo de autenticação SSH do git local**

```bash
git config --global gpg.format ssh
git config --global user.signingkey /home/gabriel/.ssh/id_rsa.pub
```

Agora os repositórios devem ser clonados no modo SSH. Exemplo:

```bash
git clone git@github.com:ihavenonickname/notas-kali.git
```

**(Opcional) Mudar o origin do repositório**

Este passo só é necessário se o repositório já tiver sido clonado no modo HTTPS.

```bash
git remote rm origin
git remote add origin git@github.com:ihavenonickname/notas-kali.git
```

