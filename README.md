Mac OS X Setup
==============

* Install Xcode

```bash
$ xcode-select --install
```

* Install [homebrew](http://brew.sh/)

```bash
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

* Clone [my mac os x setup repository](https://github.com/knakayama/mac-os-x-setup)

```bash
$ mkdir -p ~/setup/tmp
$ git clone https://github.com/makotan/mac-os-x-setup ~/setup/mac-os-x-setup
$ python -V 2> ~/setup/tmp/pv
$ cat ~/setup/tmp/pv | tr -d 'Python ' >  ~/setup/tmp/version
```

* Run [Ansible](https://github.com/ansible/ansible)

```bash
$ brew install pyenv pyenv-virtualenv gcc
$ cat >>~/.bash_profile <<'EOT'
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
EOT
$ exec $SHELL
$ pyenv install `cat ~/setup/tmp/version`
$ pyenv global `cat ~/setup/tmp/version`
$ pyenv virtualenv general-env
$ pyenv activate general-env
$ cd  ~/setup/mac-os-x-setup
$ pip install -r requirements.txt
$ ansible-playbook site.yml -vvvv --ask-become-pass
```

