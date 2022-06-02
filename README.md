# wifipatterns
Configurações padrão de empresas de internet geram um sério risco para usuários caseiros.


# Intuito
Tive a ideia desse projeto depois de muitos anos que percebi como as empresas de internet expõe os dados dos usuários. Isso não é mais tão recorrente quanto já foi, porém, como notei que muitas redes continuam com os mesmos padrões, achei válido escrever esse texto e script para alertar usuários e empresas.
O intuito desse script é SOMENTE demonstrar como estamos vulneráveis com nosso Wi-Fi de casa configurado pela empresa de internet e nunca alterando os dados de segurança.
Para testar, pedi a amigos e vizinhos que assinam diferentes serviços de internet, de diferentes empresas para testar os padrões. Obrigado a todos que me ajudaram nesses testes, teria sido impossível sem vocês.

Agora vamos ao que interessa...

# Padrões 
Para configurar roteadores (modems) de forma sequencial, empresas basearam a configuração em padrões. Isso serviu apenas para facilitar e agilizar a configuração dos aparelhos quando eles chegavam do fornecedor.
Estamos em 2010. Imagine que a empresa XYZ entrega 10.000 novos aparelhos por mês pelo paíse. Criar senhas, armazenar, imprimir adesivos para colar atrás do aparelho, configurar todo o sistema para esses dados... não, isso exigiria infraestrutura (gente), desenvolvimento de software e logística de armazenamento de dados - cada aparelho precisaria ter os dados escritos no firmware e cadastrado em uma base de dados.
O mais fácil? Replicar o que vinha do fornecedor - uma senha baseada nos dados que eles tinham, o endereço MAC da placa de rede do aparelho.
