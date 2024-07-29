# abridge-tinysearch-dev
This repo was setup to demonstrate the current issue with building and using tinysearch.
This will allow others to quickly and easily reproduce the issue.


## Install dependencies and build tinysearch from source:

```bash
sudo apt install build-essential
sudo apt install make gcc cmake binaryen curl git
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
sudo reboot

cargo install wasm-pack

git clone https://github.com/tinysearch/tinysearch
cd tinysearch
cargo build --release --features=bin
```

## Download Zola site that uses tinysearch:

```bash
cd ..

git clone https://github.com/Jieiku/abridge-tinysearch-dev
cd abridge-tinysearch-dev
```

## Build tinysearch wasm and copy to static directory:

```bash
~/.dev/tinysearch/target/release/tinysearch  -e "path=\"$HOME/.dev/tinysearch\"" --optimize public/data_tinysearch/index.html
rsync -avz wasm_output/* static/
```

## Use Zola serve to serve the site locally:

You will need zola installed, or you can download the executable directly from the release page: https://github.com/getzola/zola/releases/tag/v0.19.1

```bash
zola serve
```

Here is the resulting error in the firefox developer console:

<img src="https://raw.githubusercontent.com/Jieiku/abridge-tinysearch-dev/master/error.png"/>
