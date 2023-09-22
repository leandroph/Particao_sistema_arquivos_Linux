# Como Adicionar um Disco e Particionar no Linux

Este tutorial orientará você a adicionar um disco extra à sua máquina virtual Linux no VirtualBox, criar uma partição primária, formatá-la em ext4, monta-la no sistema e configurar a montagem automática durante o boot.

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
7. No armazenamento em disco rígido físico, não iremos nos aprofundar, apenas clique em Próximo.
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

1. Inicie sua VM e abra um terminal ou conecte na Máquina via ssh.

2. Vamos listar os discos que criamos, anteriormente, digite o seguinte comando para listar os discos disponíveis:
```bash
sudo fdisk -l
```

É possível identificar que a máquina possui dois novos discos /dev/sdb e /dev/sdc.

![alt text](imagens/imagem12.png)

3. Iremos criar duas novas partições, utilzando os discos que atachamos a Máquina Virtual, utilitário fdisk:

```bash
$ sudo fdisk /dev/sdb
$ sudo fdisk /dev/sdb
```
No prompt do fdisk, siga estas etapas:

Pressione n para criar uma nova partição.
Escolha a opção padrão para partição primária, pressionando Enter, pois assim você selecionar a opção default.
Pressione novamente o Enter para aceitar o primeiro setor padrão.
Digite +1G para especificar o tamanho da partição como 1GB.
Pressione w para salvar as alterações e sair.
Pressione q para sair do fdisk.

## Passo 3: Formatar a Partição e Obter o UUID

1. Formate a nova partição em ext4 (ou xfs, se preferir):

```bash
$ sudo mkfs.ext4 /dev/sdb1
```
![alt text](imagens/imagem22.png)

```bash
$ sudo mkfs.ext4 /dev/sdc1
```
![alt text](imagens/imagem23.png)
2. Obtenha o UUID da partição recém-formatada:

```bash
$ sudo blkid | grep sdb1
```

Anote o UUID resultante, você precisará dele mais tarde.

![alt text](imagens/imagem24.png)

## Passo 4: Montar a Partição

1. Crie um diretório onde você deseja montar a partição. Vamos usar "/mnt" como exemplo:

```bash
$ sudo mkdir /mnt/mydata
```
2. Monte a partição no diretório criado:

```bash
$ sudo mount /dev/sdb1 /mnt/mydata
```

3. Você pode criar alguns arquivos de teste na partição, se desejar:

```bash
$ sudo touch /mnt/mydata/file{1,2,3,4}.txt
```

## Passo 5: Configurar Montagem Automática no Boot

1. Abra o arquivo "/etc/fstab" em um editor de texto, como o Nano:

```bash
$ sudo nano /etc/fstab
```

2. Adicione uma linha no final do arquivo para montar a partição automaticamente durante o boot. Use o UUID que foi salvo anteriormente:

```bash
UUID=XXXXX /mnt/mydata ext4 defaults 0 0
```
Substitua "XXXXX" pelo UUID real da partição.

3. Salve o arquivo (no Nano, pressione Ctrl + O, depois Enter, e depois Ctrl + X para sair).

4. Teste a configuração do fstab para garantir que não haja erros:

```bash
$ sudo mount -a
```

5. Reinicie a VM para verificar se a partição é montada automaticamente durante o boot:

```bash
$ sudo reboot
```

Após a reinicialização, verifique se a partição está montada corretamente usando o comando df -h. Você terá um disco extra montado automaticamente em sua VM Linux sempre que ela for reiniciada.

![alt text](imagens/imagem25.png)
