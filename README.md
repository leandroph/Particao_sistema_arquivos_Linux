# Como Adicionar um Disco e Particionar no Linux

Este tutorial orientará você a adicionar um disco extra à sua máquina virtual Linux no VirtualBox, criar uma partição primária, formatá-la em ext4, montá-la no sistema e configurar a montagem automática durante o boot.

## Passo 1: Adicionar um Disco Extra no VirtualBox

1. Inicie o VirtualBox e certifique-se de que sua máquina virtual (VM) esteja desligada.
2. Selecione sua VM e clique em "Configurações" (Settings).
![alt text](imagens/imagem1.png)
3. Na seção "Armazenamento", clique em OK.
![alt text](imagens/imagem2.png)
4. Clique na opção "Controladora SATA" e escolha "Adicionar disco rígido virtual" (Add Hard Disk).
![alt text](imagens/imagem3.png)
5. Clique na opção criar.
![alt text](imagens/imagem4.png)
6. No tipo de arquivo de disco rígido, mantenha marcada a opção VDI (Virtual Disk Image), clique em Próximo.
![alt text](imagens/imagem5.png)
7. No armazenamento em disco rígido físico, não iremos nós aprofundar, apenas clique em Próximo.
![alt text](imagens/imagem6.png)
8. Para o tamanho do disco utilizaremos 20GB.
![alt text](imagens/imagem7.png)
9. Faça o mesmo procedimento para criar mais um disco, seguindo da etapa 4 até a 8. Então teremos dois discos, cada um com o armazenamento de 20 GB.
![alt text](imagens/imagem8.png)
10. Selecione o primeiro disco que criamos, e clique em Acrescentar.
![alt text](imagens/imagem9.png)
11. Faça o mesmo procedimento para o segundo disco criado.
![alt text](imagens/imagem10.png)
12. Assim teremos os discos atrelados a nossa Máquina Virtual, para finalizar clique em OK.
![alt text](imagens/imagem11.png)

## Passo 2: Criar uma Partição Primária

Inicie sua VM e abra um terminal.

Digite o seguinte comando para listar os discos disponíveis:
```bash
sudo fdisk -l
```

É possível identificar que a máquina possui dois novos discos /dev/sdb e /dev/sdc.
