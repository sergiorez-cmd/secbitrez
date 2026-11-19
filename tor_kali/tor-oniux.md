# Método alternativo para acessar rede Tor experimental Oniux

https://blog.torproject.org/introducing-oniux-tor-isolation-using-linux-namespaces

https://www.rust-lang.org/pt-BR/tools/install

1° Instalar Rust
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
```bash
rustc –version
```
2° Instalar Oniux
```bash
cargo install --git https://gitlab.torproject.org/tpo/core/oniux --tag v0.4.0 oniux
```
```bash
oniux curl ifconfig.so
```
```bash
oniux curl ipinfo.io 
``` 
```bash
oniux firefox
``` 
## Links de sites para teste
```text
https://bgp.he.net 
```
```text    
https://ipinfo.io/what-is-my-ip
```
