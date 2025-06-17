Após criar as duas redes, e as maquinas virtuais em cada nuvem, vamos criar nossa VPN Site-to-site.   
Na azure, crie um Virtual network gateway

![][image1]  
![][image2]

Após a criação, copie o ip gerado e abra o portal da aws.   

![][image7]

Na Aws, no serviço da VPC procure por VPN e Customer gateways. Crie um customer gateway e na opção de IP coloque o IP público que foi gerado na azure.  

![][image5]  
![][image4]

Depois crie um Virtual private gateways.  

![][image5]  
**OBS:** Abaixo do Customer gateways

![][image15]  

Após criar, associe ele a vpc criada.  

![][image9]  
![][image21]  

Agora crie uma VPN connections   

![][image18]  
![][image17]  
**OBS:** No static IP preferences aponte para a sub-rede privada da azure, já que a instância que realizaremos a comunicação está nessa sub-rede.

Após criar, selecione a vpn e baixe suas configurações   

![][image8]  
![][image20]

Abra o arquivo de configuração baixado e procure por “IPSec Tunnel \#1” e guarde o “Pre-Shared Key” e o “Virtual Private Gateway” depois por “IPSec Tunnel \#2” e guarda o “Pre-Shared Key” e o “Virtual Private Gateway”. Usaremos esses dois dados na azure, o Virtual Private Gateway para configurar o local network gateway (apontado o caminho do túnel )e o Pre-Shared Key para conectar os túneis. 

Agora na azure, crie um  local network gateway  

![][image3]  
**OBS:** Coloque o endereço ip do virtual gateway do primeiro túnel e aponte a rede da nossa VPC no espaço de endereço, no caso 10.0.0.0/16. Depois revise e crie o gateway de rede local  

Faça novamente essa etapa, criando assim um novo gateway de rede local, mas agora apontando para o virtual gateway do segundo túnel   

![][image10]
![][image13]

Ainda na azure, abra o Virtual network gateway que criamos no início do processo e procure por conexões   

![][image19]  

Adicione duas novas conexões, uma para cada túnel. Para o tunel 1   

![][image6]  
![][image14]  
**OBS:** Na chave compartilhada coloque o “Pre-Shared Key” do “IPSec Tunnel \#1” e repita esse processo, colocando o outro gateway de rede local que criamos, o lng-azure-aws-standby, e coloque na chave compartilhada coloque o “Pre-Shared Key” do “IPSec Tunnel \#2”.

Depois de conectarmos os dois lados da VPN, precisamos criar uma rota na aws. Conforme a topologia a nossa vpn é entre as sub-redes privadas, então precisamos adicionar uma rota na nossa tabela de rotas privada.  
 
![][image12]  
**OBS:** Aponte para sub-rede privada da azure, coloque o virtual private gateway que criamos e salve a rota. 

Agora, logue nas máquinas virtuais através do basion e tente pingar as redes. 

- Vm da Aws pingando a rede da Azure 

![][image16]

- Vm da azure pingando a rede da aws

![][image11]


[image1]: ../imagens/img-vpn/image1.png

[image2]: ../imagens/img-vpn/image2.png

[image3]: ../imagens/img-vpn/image3.png

[image4]: ../imagens/img-vpn/image4.png

[image5]: ../imagens/img-vpn/image5.png

[image6]: ../imagens/img-vpn/image6.png

[image7]: ../imagens/img-vpn/image7.png

[image8]: ../imagens/img-vpn/image8.png

[image9]: ../imagens/img-vpn/image9.png

[image10]: ../imagens/img-vpn/image10.png

[image11]: ../imagens/img-vpn/image11.png

[image12]: ../imagens/img-vpn/image12.png

[image13]: ../imagens/img-vpn/image13.png

[image14]: ../imagens/img-vpn/image14.png

[image15]: ../imagens/img-vpn/image15.png

[image16]: ../imagens/img-vpn/image16.png

[image17]: ../imagens/img-vpn/image17.png

[image18]: ../imagens/img-vpn/image18.png

[image19]: ../imagens/img-vpn/image19.png

[image20]: ../imagens/img-vpn/image20.png

[image21]: ../imagens/img-vpn/image21.png