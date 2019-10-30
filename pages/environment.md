## 3. Ambientes de Sistema

![Ambientes de Sistema](/images/pages/environment.png)

Sumário

- [3.1 Ruby](#3.1)
  - [3.1.1 Scripts Adicionais](#3.1.1)
- [3.2 Rails](#3.2)
- [3.3 node / npm](#3.3)
- [3.4 Yarn](#3.4)
- [3.5 PostgreSQL](#3.5)
- [3.6 Oracle](#3.6)
- [3.7 Docker](#3.7)

## 3.1 Ruby <a name="3.1"></a>

```bash
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
export RUBY_VERSION=2.6; rvm install $RUBY_VERSION && rvm use $RUBY_VERSION --default
gem i bundler
```

### 3.1.1 Scripts Adicionais <a name="3.1.1"></a>

Otimiza a instalação das gems não incluindo a documentação:

```bash
rm -f $HOME/.gemrc && touch $HOME/.gemrc && echo "gem: --no-document" >> $HOME/.gemrc
```

Melhora a saída de texto no console, quando gem 'awesome_print' estiver disponível:

```bash
rm -f $HOME/.irbrc && touch $HOME/.irbrc && echo "require 'awesome_print'\nAwesomePrint.irb\!\n" >> $HOME/.irbrc
```

Otimiza o file system para não acontecer overflow de arquivos abertos:

```bash
echo fs.inotify.max_user_watches=524288 | sudo tee /etc/sysctl.d/40-max-user-watches.conf && sudo sysctl --system
```

Otimiza o bundler para usar todos os núcleos do processador:

```bash
bundle config $(nproc)
```

## 3.2 Rails <a name="3.2"></a>

Proceder com instalação do Ruby e então:

```bash
gem i rails
```

## 3.3 node / npm <a name="3.3"></a>

```bash
sudo apt -fy install git curl
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
source $HOME/.nvm/nvm.sh
nvm ls-remote && nvm install --lts && nvm alias default node
```

## 3.4 Yarn <a name="3.4"></a>

```bash
sudo apt -fy install curl
sudo apt remove cmdtest -y
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update && sudo apt install --no-install-recommends -y yarn
```

## 3.5 PostgreSQL <a name="3.5"></a>

```bash
sudo apt update && sudo apt -fy install postgresql postgresql-common postgresql-client
sudo -u postgres createuser $USER -s
```

## 3.6 Oracle <a name="3.6"></a>

Adicionar variáveis de ambiente (bash, zsh, ...etc)

```bash
export ORACLE_HOME=/opt/oracle/instantclient
export LD_LIBRARY_PATH=$ORACLE_HOME:$LD_LIBRARY_PATH
```

```bash
sudo apt install curl libaio1 -fy
curl --compressed http://s3.amazonaws.com/probus.wonder.com.br/docker/oracle/instantclient_12_1.tar.gz > /tmp/instantclient.tar.gz
tar xzf /tmp/instantclient.tar.gz -C /tmp/
sudo mkdir -p $ORACLE_HOME
sudo mv /tmp/instantclient_12_1/* $ORACLE_HOME/
sudo chown -R $USER:${GROUP:-$USER} $ORACLE_HOME
chmod 755 $ORACLE_HOME
ln -s $ORACLE_HOME/libclntsh.so.12.1 $ORACLE_HOME/libclntsh.so
ln -s $ORACLE_HOME/libclntshcore.so.12.1 $ORACLE_HOME/libclntshcore.so
ln -s $ORACLE_HOME/libocci.so.12.1 $ORACLE_HOME/libocci.so
```

## 3.7 Docker <a name="3.7"></a>

```bash
sudo apt install -fy curl apt-transport-https ca-certificates gnupg2 software-properties-common
echo "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker-ce.list
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
sudo apt update && sudo apt install -fy docker-ce docker-ce-cli containerd.io
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo usermod -aG docker $USER
```
