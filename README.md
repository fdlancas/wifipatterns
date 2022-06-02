# wifipatterns
Configurações padrão de empresas de internet geram um sério risco para usuários caseiros.


# Objetivo
Tive a ideia desse projeto depois de muitos anos que percebi como as empresas de internet expõe os dados dos usuários. Isso não é mais tão recorrente, porém, como notei que muitas redes continuam com os mesmos padrões, achei válido escrever esse texto e script para alertar usuários e empresas.<br>
O intuito desse script é SOMENTE demonstrar como estamos vulneráveis com nosso Wi-Fi de casa configurado pela empresa de internet e nunca alterando os dados de segurança.<br>
Para testar, pedi a amigos e vizinhos que assinam diferentes serviços de internet, de diferentes empresas para testar os padrões. Obrigado a todos que me ajudaram nesses testes, teria sido impossível sem vocês.

Agora vamos ao que interessa...

# Padrões
Para configurar roteadores (modems) de forma sequencial/rápida, empresas basearam a configuração em padrões. Isso serviu apenas para facilitar e agilizar a configuração dos aparelhos quando eles chegavam do fornecedor, podendo enviar para o usuário final rapidamente.<br>
<br>
Estamos em 2010. Imagine que a empresa XYZ entrega 10.000 novos aparelhos por mês pelo país. Criar senhas, armazenar, imprimir adesivos para colar atrás do aparelho, configurar todo o sistema para esses dados... não, isso exigiria infraestrutura (gente), desenvolvimento de software e logística de armazenamento de dados - cada aparelho precisaria ter os dados escritos no firmware e cadastrado em uma base de dados. isso tudo geraria custo.<br>
O mais fácil? Replicar o que vinha do fornecedor - uma senha baseada nos dados que eles tinham, o <b>endereço MAC da placa de rede</b> do aparelho.<br>
<br>
E foi assim que nossos modems/roteadores foram configurados: baseados num número que identifica a placa de rede dentro deles. A melhor parte? Isso fica público.<br>
Sim, o endereço MAC do seu roteador fica aberto a qualquer pessoa que esteja por perto. Isso é porque, da maneira que os aparelhos se conectam hoje em dia, o endereço MAC é a única informação pública verificável. E ele é, de certa maneira, único.<br>
Então, se tiver duas redes chamadas "<i>Joao WiFi</i>" por perto, mas eu já conectei na sua, meu celular entra nela de novo direto. Isso acontece porque o endereço MAC da placa de rede do seu roteador já foi salvo no meu celular, associado ao nome da sua rede. É assim que meu celular sabe que o seu "<i>Joao WiFi</i>" é diferente do "<i>Joao WiFi</i>" do vizinho. Meu celular tenta conectar na rede que tem o MAC salvo, não na rede com o nome salvo.<br>
<br>
Então, se a sua senha for baseada nesse endereço MAC, dá pra descobrir? Isso.

# Provedores
Temos diversos provedores. A questão é que muitos deles pertecem a outro. X comprou Y que comprou Z e hoje, na verdade, temos as grandes telefônicas provendo internet. Então se você paga a empresa C ou V ou N, não muda muito. Elas todas compram os aparelhos do mesmo lugar e configuram do mesmo jeito. Ainda bem que isso mudou, mas tem muito modem aí configurado baseado no endereço MAC.<br>
<br>
O endereço MAC é tipo um número serial. Ele representa um monte de coisa: fabricante, versão, ano... ele guarda bastante informação. mas voltando pro foco: o endereço MAC compõe a senha do WiFi de casa. E ele tá aberto.<br>

# AA:BB:CC:11:22:33
Endereços MAC são compostos por 6 blocos de 2 caracteres cada e estão presentes em toda placa que faz algum tipo de comunicação com outra. É uma forma de placas se identificarem entre si. Esse endereço MAC, então, passou a ser usado por provedores de internet para definir a senha do WiFi de um aparelho quando é configurado, antes de ir para o usuário final.<br>
<br>
Portanto, por um longo período de tempo, os provedores enviavam roteadores/modems usando o MAC inteiro como senha. Até cerca de 2010 era extremamente comum encontrar diversas redes por aí com nomes tipo <b>PROV-2233</b>, sendo "PROV" o nome do provedor e "2233" o final do MAC da placa do roteador. E, adivinhe... a senha era <b>AABBCC112233</b> - o endereço MAC inteiro. E ainda tem muito roteador por aí com esse padrão.<br>
<br>
Após algum tempo, provedores passaram a adicionar alguns caracteres ao nome da rede que não faziam parte do endereço MAC, para aumentar a dificuldade de pessoas sem permissão acessarem redes com a configuração padrão. Então, começaram a definir senhas como <b>AABBCC1122<i>GG</i></b>, onde "GG" são caracteres que não estão no endereço MAC. Parece um pouco mais seguro, correto? O problema é que esses caracteres "randômicos" (GG nesse exemplo) precisavam estar acessíveis de alguma forma. Então começou-se uma fórmula "genial" de colocar eles no nome da rede. Assim, novas redes vinham definidas da seguinte forma:<br>
<br>
Nome: <b>PROV-22GG</b><br>
Senha: <b>AABBCC1122GG</b>
<br>
E é simplesmente por esse tipo de padrão que esse script procura.<br>
Tendo ficado um pouco à toa durante a pandemia de 2020-2021, lembrei desses padrões bobos e resolvi testar. Tendo 2 provedores contratados (caso um deles caia, o outro deve continuar funcionando), simplesmente olhei atrás dos modems/roteadores e notei que seguiam esses padrões.<br>
Resolvi então pedir pra alguns amigos enviarem foto da parte de trás dos modems deles e vários seguiam esses padrões; exceto os aparelhos de 5 anos pra cá - nesses a senha não tem absolutamente nenhuma relação com o endereço MAC.<br>
<br>
Portanto, esse script faz o seguinte:<br>
1. Procura redes com nomes dentro de padrões definidos, tipo <b>PROV_2Gxxxx</b><br>
2. Pega o endereço MAC do roteador<br>
3. Baseado no nome do provedor, monta o que seria a senha padrão<br>
4. Tenta conectar na rede com a senha padrão<br>
5. Caso consiga conectar, faz PING em um servidor DNS para testar conexão<br>
6. Caso o PING retorne OK, acessa um serviço que retorna o IP público do roteador<br>
7. Salva em um banco de dados: nome da rede, senha, IP, última vez que acessou a rede<br>
<br>
E fim.<br>
<br>

# Extra
Depois de alguns testes achei divertido não só salvar esses dados, mas também a localização de cada rede encontrada.<br>
Procurei diversos métodos (posição baseada em IP, baseada no MAC, usando bluetooth, etc.), mas nenhum era preciso suficiente. Existem serviços *gratuitos* que retornam esse tipo de informação, mas eu queria algo que não dependesse de nenhum tipo de conexão com nada. É aí que entra o celular.<br>
<br>
Os celulares de hoje têm GPS interno, o que possibilita pegar essa localização. O problema é onde cada aparelho salva isso e como acessar. Então pensei em uma gambiarra: e se usarmos html5 pra pegar essa localização? Foi aí que decidi criar uma interface. O principal intuito dela não é mostrar redes, mas sim usar o GPS do celular pra pegar a localização. Então, já que precisaria ficar com o celular ligado, com o navegador aberto em um site, escolhi fazer uma interface discreta que simula um tocador de música. Assim, ao chegar num bar, poderia deixar o celular ligado, com essa interface aberta, sem chamar atenção.<br>
<br>
Então, se você não quiser marcar a localização das redes, não precisa abrir o site. Não precisa ter o celular por perto. Basta acessar o aparelho via ssh e rodar o script.<br>
<br>
Porém, tedo feito a interface, adicionei algumas funções básicas: iniciar o script, parar o script, desligar o aparelho, mostrar senha testada com sucesso.
