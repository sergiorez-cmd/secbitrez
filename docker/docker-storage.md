# Guia de Configuração de Armazenamento do Docker no Linux

Este guia prático demonstra como localizar e editar o arquivo de configuração do Docker Daemon no Linux para gerenciar o local de armazenamento de dados e drivers.

---

## 1. Arquivos de Configuração Principais

No Linux, o comportamento do Docker é controlado por três arquivos principais:

*   **`/etc/docker/daemon.json`**: O principal arquivo de configuração do daemon (serviço) do Docker. *Nota: Por padrão, ele não vem criado em instalações limpas.*
*   **`~/.docker/config.json`**: Guarda as configurações do cliente CLI (como credenciais de login e preferências do usuário).
    **`/etc/containerd/config.toml`**: O principal arquivo de configuração do gerenciador de containers, (baixar imagens, iniciar, parar e interagir com o kernel do sistema operacional). Ele funciona "nos bastidores".
---

## 2. Alterando o Diretório Padrão de Armazenamento (`data-root`)

Por padrão, o Docker armazena todas as imagens, containers e volumes no caminho `/var/lib/docker`. Se o seu disco principal estiver cheio, você pode mover essa estrutura para um HD/SSD secundário ou partição dedicada.

### Passo a Passo

1. **Interrompa o serviço do Docker:**
   ```bash
   sudo systemctl stop docker.socket docker containerd
   ```

2. **Crie ou edite o arquivo de configuração .json:**
   Crie o arquivo `/etc/docker/daemon.json` com o seu editor de texto preferido e adicione a chave `"data-root"` apontando para o novo diretório:
   ```bash
   mkdir -p /mnt/meu_disco/docker
   ```
   ```json
   {
     "data-root": "/mnt/meu_disco/docker"
   }
   ```
3. **Edite o arquivo de configuração .toml:**
   Edite o arquivo `/etc/containerd/config.toml` com o seu editor de texto preferido e adicione a chave `root` apontando para o novo diretório:
   ```bash
   mkdir -p /mnt/meu_disco/containerd
   ```
   ```toml
   disabled_plugins = ["cri"]
   root = "/mnt/meu_disco/containerd"
   ```

5. **Sincronize os dados antigos para o novo local:**
   Para não perder as imagens e containers que você já baixou, copie os arquivos mantendo as permissões originais:
   ```bash
   sudo rsync -aP /var/lib/docker/ /mnt/meu_disco/docker/
   ```
   ```bash
   sudo rsync -aP /var/lib/containerd/ /mnt/meu_disco/containerd/
   ```

6. **Inicie o serviço do Docker novamente:**
   ```bash
   sudo systemctl start docker.socket docker containerd
   ```

---

## 3. Configurando o Storage Driver

O Docker gerencia o espaço em disco das camadas de imagens usando drivers de armazenamento. O padrão moderno e recomendado para a maioria das distribuições Linux atuais é o **`overlay2`**.

Se você precisar declarar explicitamente o driver ou combiná-lo com a mudança de diretório, a estrutura do seu `/etc/docker/daemon.json` deve seguir este padrão:

```json
{
  "storage-driver": "overlay2",
  "data-root": "/mnt/meu_disco/docker"
}
```
*Atenção: Lembre-se de usar a vírgula para separar as propriedades dentro do arquivo JSON.*

---

## 4. Validando as Alterações

Após reiniciar o Docker, execute o comando abaixo para certificar-se de que o daemon carregou as novas configurações de diretório e driver com sucesso:

```bash
sudo docker info | grep -E "Root Dir|Storage Driver"
```
```bash
sudo containerd config migrate
```

O retorno esperado no terminal deverá exibir os novos caminhos e drivers definidos por você.
