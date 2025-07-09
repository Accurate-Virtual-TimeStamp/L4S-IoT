Relatório de Procedimentos para Conversão e Clonagem de Imagem de Disco do SONiC

# Download do Arquivo

Primeiramente, é necessário baixar o arquivo da imagem de disco a partir do
seguinte link:
[Download da Imagem](https://sonic-build.azurewebsites.net/api/sonic/artifacts?branchName=202311&platform=vs&buildId=654245&target=target%2Fsonic-vs.img.gz).


# Conversão da Imagem
Após o download, a imagem deve ser convertida do formato QCOW2 para o
formato RAW. Isso é feito utilizando o comando qemu-img:
```shell
qemu−img convert −f qcow2 −O raw sonic−vs.img sonic−vs.raw
```
A conversão para o formato RAW é necessária porque este formato é ampla-
mente suportado por diversas ferramentas de clonagem e virtualização. Além
disso, o formato RAW permite acesso direto aos dados do disco, o que pode ser
mais eficiente em termos de desempenho.

# Limpeza do Disco de Destino
Antes de clonar a imagem para o disco de destino, é importante limpar o disco
para remover quaisquer resı́duos de dados anteriores. Isso pode ser feito uti-
lizando a ferramenta wipe:
```shell
sudo wipe /dev/sdX
```
A limpeza do disco de destino é crucial para garantir que não haja resı́duos
de dados que possam interferir no funcionamento do novo sistema operacional.
Isso ajuda a evitar problemas de compatibilidade e desempenho.

# Clonagem da Imagem
Finalmente, a imagem convertida deve ser clonada para o disco de destino uti-
lizando o comando dd:
```
sudo dd if=sonic−vs.raw of=/dev/sdX bs=4M status=progress
```

# Conclusão
Após a conclusão do comando dd, o disco de destino estará clonado e pronto
para uso com o sistema operacional Sonic.
