# Plutus Pioneer - Development Environment
__Learn Plutus and become a certified Plutus Pioneer with our new series of interactive training courses by IOG__

> NOTE: Currently test on x86_64 GNU/Linux only.


## Local or Host System <a id="ubuntu-nix-plutus"></a>

### Setup

#### Make a working project directory.

```bash
mkdir plutus-dev
cd plutus-dev
```

#### Git Clone Plutus & Plutus Pioneer Program repos

```bash
git clone https://github.com/input-output-hk/plutus.git
```

```text
git clone https://github.com/input-output-hk/plutus-pioneer-program.git
```

## Ubuntu Nix Container<a id="ubuntu-nix-plutus"></a>

A Docker Image with Ubuntu Core and Nix for Plutus Development.  

If you have a separate namespace setup for your Docker environment, you will  need to disable this setting in your daemon, `/etc/docker/daemon.json`

and restart your Docker daemon.  The Plutus development environment will not run outside the host namespace.  If you are a Docker wizard and know how to do this, I would love to learn how &gt;  [Telegram](https://t.me/HeathDRobertson) 

### Quick Start

#### Nix Data Container

Build a data container for Nix packages.

```text
sudo docker create --name nix -v nix:/nix heathdrobertson/ubuntu-nix:latest sh
```

#### Run a development container.

```text
sudo docker run -it --name plutus-dev \
    --network host \
    --volumes-from nix \
    --volume $(pwd)/:/home/plutus-dev \
    --workdir /home/plutus-dev \
    heathdrobertson/ubuntu-nix:latest
```

```bash
nix-env --version
```

Output: `nix-env (Nix) 2.3.10`

#### IOHK Builds

Update Nix configuration.

```bash
mkdir -p ~/.config/nix
echo 'substituters = https://hydra.iohk.io https://iohk.cachix.org https://cache.nixos.org/' >> ~/.config/nix/nix.conf
echo 'trusted-public-keys = hydra.iohk.io:f/Ea+s+dFdN+3Y/G+FDgSq+a5NEWhJGzdjvKNGv0/EQ= iohk.cachix.org-1:DpRUyj7h7V830dp/i6Nti+NEO2/nhblbov/8MW7Rqoo= cache.nixos.org-1:6NCHdD59X431o0gWypbMrAURkbJ16ZPMQFGspcDShjY=' >> ~/.config/nix/nix.conf
```

```bash
cd /home/plutus-dev/plutus
nix build -f default.nix plutus.haskell.packages.plutus-core
```

#### Refine Your Setup

Update Cabal

```bash
nix-shell
```

```bash
cabal update
```

`exit` the Nix shell.

The Plutus Pioneer Program source is made to compile and run against Plutus for a specific commit hash which is listed in each week's `cabal.project` file.

```bash
cat /home/plutus-dev/plutus-pioneer-program/code/week01/cabal.project | less
```

e.g. tag: 3746610e53654a1167aeb4c6294c6096d16b0502

```bash
git checkout 3746610e53654a1167aeb4c6294c6096d16b0502
```

Then rebuild the Nix environment to match the current weeks builds.

```bash
nix build -f default.nix plutus.haskell.packages.plutus-core
```

`exit` out of you running interactive TTY container session, which will stop the container, and restart `sudo docker start plutus-dev` the container from your host machine.

## Two Termianls
Open two Terminal windows or Tmux panes and run an interactive TTY container session in each:

```bash
sudo docker exec -it plutus-dev nix-shell /home/plutus-dev/plutus/shell.nix
```
### Session #1
```bash
cd /home/plutus-dev/plutus-playground-server
plutus-playground-server
```

### Session #2
```bash
cd plutus-playground-client
npm run start
```
You should now be able to navigate to [https://localhost:8009](https://localhost:8009). The browser will complain about it being a risky website, allow it.

![The End](./the-end.gif)

## Everything You Need To Know
* [Plutus Community Documentation](https://docs.plutus-community.com/)
* [Plutus Pioneer Program](https://iohk.io/en/blog/posts/2021/04/01/everything-you-need-to-know-about-our-new-plutus-pioneer-program/)

## Plutus Platform starter project - By IOG (IOHK)

- [Plutus Pioneer Program Repo](https://github.com/input-output-hk/plutus-pioneer-program)
- [Plutus](https://github.com/input-output-hk/plutus.git)
- [Plutus Starter](https://github.com/input-output-hk/plutus-starter)
