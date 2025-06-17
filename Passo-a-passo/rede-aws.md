Para essa topologia iniciaremos configurando a nossa rede virtual na aws. Procure pelo serviço VPC e selecione a opção “criar VPC”   
![][image2]

Depois crie as subnets da rede virtual. Aqui usaremos uma pública, para nossa instancia gerenciadora e uma privada para a instância que será usada de teste para nossa VPN.  
![][image12]  
![][image10]

Depois crie duas tabelas de rotas. Uma relacionada a subnet publica e outra a privada   
![][image5]  
![][image17]  
Agora, crie um gateway de internet   
![][image1]  
após cria-lo associe ele a sua vpc   
![][image13]  
![][image4]  
Crie um nat gateway para a subnet privada, para que a instância possa ter acesso a internet. ![][image19]  
**OBS:** Ao criar o nat é necessário alocar um ip publico para que o nat funcione corretamente

Vá nas tabelas de rotas e selecione a tabela que foi direcionada para a subnet pública  
![][image7]

É necessário criar uma rota para o internet gateway que criamos. Para isso selecione “Routes” e depois “Edit Routes” e adicione uma rota pra o igw.  
![][image8]  
Repita esse processo para a nossa tabela de rotas referente a subnet privada e adicione uma rota para o nosso nat gateway 

![][image3]

Após esse processo procure pelo serviço EC2 e selecione a opção “instâncias” e depois  “criar instância”. Criaremos duas instâncias. Uma para ser nosso bastion-host e outra para testar o ping após criarmos a VPN   
![][image6]  
Edite as configurações de rede   
![][image14]  
![][image18]  
**OBS:** Essas configurações são para o bastion host. Para criar a instância para fazermos o teste, repita o mesmo processo, altere para o nome que desejar e nas configurações de rede aponte para a subnet privada, deixe o ip público desabilitado e crie um grupo de segurança para essa instância, exemplo seria “SgAwsPriv”

As instâncias ficaram assim:  
![][image16]  
**OBS:** Ao acessar o bastion é preciso colocar a chave vockey nessa instância para conseguirmos acessar a outra instância via ssh. E também é necessário liberar o acesso via ssh nos grupos de segurança, por padrão essa regra já vem criada quando criamos a instância, então verifique se a regra está criada no grupo de segurança. Caso não estaja:  

![][image20]  
![][image15]  
Adicione essa regra:   
![][image9]

No grupo de segurança que a instância privada faz parte, crie uma regra para liberar o icmp. Esse processo é necessário para fazermos o teste de ping entre as instâncias privadas de cada nuvem   
![][image11]  


[image1]: ../imagens/img-aws/image1.png

[image2]: ../imagens/img-aws/image2.png

[image3]: ../imagens/img-aws/image3.png

[image4]: ../imagens/img-aws/image4.png

[image5]: ../imagens/img-aws/image5.png

[image6]: ../imagens/img-aws/image6.png

[image7]: ../imagens/img-aws/image7.png

[image8]: ../imagens/img-aws/image8.png

[image9]: ../imagens/img-aws/image9.png

[image10]: ../imagens/img-aws/image10.png

[image11]: ../imagens/img-aws/image11.png

[image12]: ../imagens/img-aws/image12.png

[image13]: ../imagens/img-aws/image13.png

[image14]: ../imagens/img-aws/image14.png

[image15]: ../imagens/img-aws/image15.png

[image16]: ../imagens/img-aws/image16.png

[image17]: ../imagens/img-aws/image17.png

[image18]: ../imagens/img-aws/image18.png

[image19]: ../imagens/img-aws/image19.png

[image20]: ../imagens/img-aws/image20.png