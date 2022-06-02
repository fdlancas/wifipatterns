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
Sim, o endereço MAC do seu roteador fica aberto a qualquer pessoa que esteja por perto. Isso é porque, da maneira que os aparelhos se conectam hoje em dia, o endereço MAC é a única coisa que é identificável, ele é único. Então, se tiver duas redes chamadas "Joao WiFi" por perto, mas eu já conectei na sua e meu celular entra nela de novo direto, isso é porque o endereço MAC da placa de rede do seu roteador já foi salvo pra mim. É assim que meu celular sabe que o seu "Joao WiFi" é diferente do "Joao WiFi" do vizinho. Meu celular tenta conectar na rede que tem o MAC salvo, e só aí testa a senha.<br>
<br>
Então, se a sua senha for baseada nesse endereço MAC, dá pra adivinhar, né? Pronto. Temos aí boa partes das redes do país.<br>
?)

# Provedores
Temos diversos provedores. A questão é que muitos deles pertecem a outro. X comprou Y que comprou Z e hoje, na verdade, temos as grandes telefônicas provendo internet. Então se você paga a empresa C ou V ou N, não muda muito. Elas todas compram os aparelhos do mesmo lugar e configuram do mesmo jeito. Ainda bem que isso mudou, mas tem muito modem aí configurado baseado no endereço MAC.<br>
<br>
O endereço MAC é tipo um número serial. Ele representa um monte de coisa: fabricante, versão, ano... ele guarda bastante informação. mas voltando pro foco: o endereço MAC compõe a senha do WiFi de casa. E ele tá aberto.
