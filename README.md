# Janus Gateway + NDI Plugin (Docker)

Este projeto roda o Janus Gateway com o plugin NDI habilitado, pronto para deploy em servidores Linux.

## Pré-requisitos

- Baixe o [NDI SDK para Linux (v5)](https://www.ndi.tv/sdk/) da NewTek e coloque o arquivo `Install_NDI_SDK_v5_Linux.tar.gz` na raiz deste projeto.
- Docker e Docker Compose instalados.

## Como usar

```sh
git clone https://github.com/<seu-usuario>/janus-ndi-docker.git
cd janus-ndi-docker
# Adicione o Install_NDI_SDK_v5_Linux.tar.gz na pasta do projeto
docker compose build
docker compose up -d
```

- Acesse o Janus REST API em `http://<SEU_IP>:8088/janus`
- O plugin NDI estará disponível para uso em `/janus/plugins/ndi`

## Customização

- Edite `janus.jcfg` e `janus.plugin.ndi.jcfg` conforme necessário.
- Para mais exemplos de integração, consulte a [documentação oficial do plugin NDI](https://github.com/meetecho/janus-gateway-ndi).

## Observações

- O plugin NDI só funciona em ambientes x86_64 com suporte ao NDI SDK.
- O container roda em modo `network: host` para facilitar a comunicação RTP/NDI.
