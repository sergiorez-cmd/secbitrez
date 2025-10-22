# Método alternativo para acessar rede Tor experimental Oniux

https://blog.torproject.org/introducing-oniux-tor-isolation-using-linux-namespaces

https://www.rust-lang.org/pt-BR/tools/install

1° Instalar Rust
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
```
rustc –version
```
2° Instalar Oniux
```
cargo install --git https://gitlab.torproject.org/tpo/core/oniux --tag v0.4.0 oniux
```
```
oniux curl ifconfig.so, $oniux curl ipinfo.io 
```
```
oniux firefox
``` 
## Links de sites para teste

https://bgp.he.net 
    
https://ipinfo.io/what-is-my-ip
