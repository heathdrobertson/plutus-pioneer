# Plutus Pioneer
__Learn Plutus and become a certified Plutus Pioneer with our new series of interactive training courses by IOG__

> NOTE: Currently test on x86_64 GNU/Linux only.

## Plutus Development environment in a Docker container.


## QUICK START
1. Build a nix data container:
    1. `docker create --name nix -v nix:/nix nixos/nix sh`
1. Clone the **Plutus Pioneer Program** repo.
    1. `git clone https://github.com/input-output-hk/plutus-pioneer-program.git`


## Terminal Window or Split 1 of 3.
1. `docker run -it --name plutus-dev --privileged --volumes-from nix --volume $(pwd)/plutus-pioneer-program/:/home/ci/ --network host heathdrobertson/ubuntu-nix-plutus:latest`
1. `cd /home/ci/code/week01`
1. `cabal update`


## Terminal Window or Split 2 of 3 start the Playground server.
1. `docker exec -it plutus-dev nix-shell /root/plutus/shell.nix`
1. `cd /root/plutus/plutus-playground-client`
1. `plutus-playground-server`


## Terminal Window or Split 3 of 3 the Playground client.
1. `docker exec -it plutus-dev nix-shell /root/plutus/shell.nix`
1. `cd /root/plutus/plutus-playground-client`
1. `npm run start`
1. `https://localhost:8009/`



---


## To Build Image Locally
1. Download the `Dockerfile` & make your updates.
1. `docker build -t <dockerhubid/reponame>:latest .`
    1. .g. `docker build -t heathdrobertson/ubuntu-nix-plutus:latest .`


---



## Everything You Need To Know

* [Plutus Pioneer Program](https://iohk.io/en/blog/posts/2021/04/01/everything-you-need-to-know-about-our-new-plutus-pioneer-program/)

## Plutus Platform starter project - By IOG (IOHK)

- [Plutus Pioneer Program Repo](https://github.com/input-output-hk/plutus-pioneer-program)
- [Plutus](https://github.com/input-output-hk/plutus.git)
- [Plutus Starter](https://github.com/input-output-hk/plutus-starter)
