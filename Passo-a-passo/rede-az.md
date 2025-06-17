Configuração da nossa rede na azure. Inicie criando o grupo de recurso e os grupos de segurança.   
![][image15]  
![][image9]  
**OBS:** Da mesma forma que criamos grupos de segurança para as duas instâncias da aws, criaremos grupos de segurança para as vms da azure.   
![][image1]  
Depois crie a Rede virtual   
![][image13]  
Avance até endereços IP. Escolha um espaço de endereçamento diferente do Criado na aws. Nesse cenário foi criado a rede **10.0.0.0/16 para aws** e **172.16.0.0/16 para azure**  
![][image14]  
Adicione 3 sub-redes. Uma publica, uma privada e outra para o nosso Gateway, etapa necessária para configurar a VPN. 

- gateway

![][image6]

- sub-rede publica 

![][image2]  
![][image12]

- sub-rede privada 

![][image17]  
![][image4]  
**![][image5]**

Depois de criar as sub-redes revida e cria a nossa rede   
![][image18]

Após criar a rede virtual, crie as máquinas virtuais. Seguindo a mesma lógica que foi feita na aws, criaremos duas máquinas virtuais, uma para ser o bastion-host e outra para fazermos o teste de ping.   
![][image19]  
Criando o Bastion   
![][image7]  
![][image11]  
![][image3]  
![][image10]  
Depois de definir as configurações da sua máquina virtual que servirá como bastion-host faça as mesmas configurações para a outra máquina virtual que servirá como teste, porém como ip público coloque “nenhum” e coloque as informações de rede voltadas para a sub-rede privada.   
Agora, habilite o acesso ssh nos grupos de segurança. Diferente da aws, que ao criar a instância a regra já vem criada no grupo de segurança, na azure é preciso criar essa regra.   
![][image16]

Após permitir o ssh nos grupos de segurança, libere o Icmp no grupo de segurança da máquina virtual privada para fazermos o teste de ping entre as instâncias privadas de cada nuvem. O processo de criação de regra é o mesmo.   
![][image8]


[image1]: ../imagens/img-az/image1.png

[image2]: ../imagens/img-az/image2.png

[image3]: ../imagens/img-az/image3.png

[image4]: ../imagens/img-az/image4.png

[image5]: ../imagens/img-az/image5.png

[image6]: ../imagens/img-az/image6.png

[image7]: ../imagens/img-az/image7.png

[image8]: ../imagens/img-az/image8.png

[image9]: ../imagens/img-az/image9.png

[image10]: ../imagens/img-az/image10.png

[image11]: ../imagens/img-az/image11.png

[image12]: ../imagens/img-az/image12.png

[image13]: ../imagens/img-az/image13.png

[image14]: ../imagens/img-az/image14.png

[image15]: ../imagens/img-az/image15.png

[image16]: ../imagens/img-az/image16.png

[image17]: ../imagens/img-az/image17.png

[image18]: ../imagens/img-az/image18.png

[image19]: ../imagens/img-az/image19.png
