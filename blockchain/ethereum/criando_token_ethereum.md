# Criando um Token na Ethereum Blockchain

 
Neste tutorial,o objetivo é orientá-lo nas etapas de configuração da sua conta e emitir seu primeiro token na rede Ethereum usando um único contrato inteligente.
O token será um ERC20 padrão, terá as principais funções e pode ser usado como base geral para aplicativos mais sofisticados do que apenas transferi-los.
 
 Endereço Ethereum
Neste tutorial, usaremos uma rede de teste para emitir o token, para que você não gaste o Ether ETH real. Usaremos a rede Ropsten Test. Para começar, vá para MyEtherWallet (MEW) e crie uma conta lá.
 
Para obter a configuração, clique no canto direito, altere a rede para Ropsten ( MyEtherWallet ou MetaMask Wallet ) → clique em Nova Carteira → Digite uma senha que você possa lembrar → Faça o download / salve o seu arquivo Keystore em um espaço seguro → Salve sua chave privada em um cofre espaço. Todo o processo de criação de conta e conexão na rede de teste é bem simples e podemos ir ao novo pass0.
 
# Endereço da carteiro ETH -

Endereço da sua carteira, vá para → Exibir informações da carteira → Chave privada → Digite a chave privada salva → Desbloqueie sua carteira e ela deve estar lá!
Basicamente, o que você terá que fazer em termos simples:
Faça o download do MetaMask em metamask.io .
Selecione Rede Ropsten.
Selecione DEPÓSITO.
Reivindicação 1 Ropsten ETH.
Acionar um faucet para obtenção de moedas ETH testes para criação do seu token.
Transacione para o endereço que você usará para o tutorial em MyCrypto .

 
Contrato
Faça o download do contrato inteligente que o lendário cavaleiro unicórnio Ethereum, BokkyPooBah nos ajudou a fazer, clicando aqui . ⬅️
Você estará editando este código para seu próprio token.

Links:

Issue-your-own-ERC20-token/erc20
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tg9nc1g7c2cizeu8vsnx.png)_tutorial.sol at master · bitfwdcommunity/Issue-your-own-ERC20-token



Agora vamos começar:

Abra o contrato que você baixou no seu Editor de texto.
Vá para a Linha 3–15 e veja a seção de comentários. Embora esta seja uma seção de comentários, isso o ajudará a seguir o caminho. Para mim, 0Fucks foi o meu primeiro :). Basicamente, você envia 0Fucks a alguém quando não se importa.
Altere a Linha 4 para o título do seu contrato inteligente
Altere a Linha 6 para o endereço Ropsten Ethereum que você criou no MyEtherWallet
Altere o símbolo da linha 7 para o respectivo nome de moeda (mantenha-o curto)
Altere a Linha 8 para o nome do seu token



Próximo:
Vá para a linha 102 e altere "FucksToken" para "(YourTokenName)
Faça o mesmo para a linha 115
Vá para a linha 116 e altere o nome do símbolo, o mesmo que você fez na seção de comentários
Faça o mesmo para a linha 117
Alterar o endereço da linha 120 para ser o mesmo que você gerou no MEW
O mesmo vale para a Linha 121
 
Para as casas decimais e o fornecimento total nas Linhas 118 e 119, você pode deixar como está, no entanto, explicarei apenas para obter visibilidade. Na oferta total, existem algumas considerações. O primeiro é que o padrão (e máximo) tem 18 casas decimais, o que significa que uma moeda pode ser dividida em 18 partes.
A segunda é que, digamos, por exemplo, que você queira emitir 100 tokens, na parte do suprimento total você deve colocar 100, seguido pelo número de casas decimais que escolher.
Ex: Se eu quiser emitir 100 tokens, o que colocarei no suprimento total é: 100000000000000000000; e por aí vai.
 


Depois disso, terminamos a edição do código. Sim, isso foi fácil. Agora vamos fazer algumas coisas legais ...
Vá para http://remix.ethereum.org/
No navegador / ballot.sol, cole o código que você acabou de editar! Se algo vermelho aparecer, há algo errado no código. Se houver um aviso amarelo, tudo bem, esperamos o melhor.
Agora em Compilar → Detalhes → Escolha o token que você está criando
Em ByteCode, pressione o botão to para copiar o ByteCode para a área de transferência - (Nesta seção, o que pode aparecer são coisas diferentes no ByteCode. O que você deve copiar é o ByteCode do “objeto”, adicionando 0x no início. terá 0xByteCode.)



Vá para o MEW, onde começaremos a implantar o contrato. Lembre-se de que queremos estar na Ropsten Test Network, portanto, verifique se o canto superior direito diz
Navegue até a guia Contratos → Pressione Implantar contrato
Cole seu ByteCode na caixa ByteCode. Seu limite de gás deve ser atualizado automaticamente
Acesse sua carteira, acessando a Chave privada → Digite sua chave privada → Desbloqueie sua carteira
Agora pressione Assinar transação → Implementar transação
ATENÇÃO: Este é o momento em que você deve cruzar os dedos pela primeira vez durante alguns segundos. 🤞
Clique na transação tx ou acesse https://ropsten.etherscan.io para verificar se o contrato foi aprovado. Caso contrário, comece novamente e tente descobrir o que você errou. Se sim, você é basicamente o Vitalik 2.0, tenha orgulho.
Se tudo der certo, esta é uma imagem de amostra do que você deveria estar vendo.


Agora vamos registrar este contrato. Fazer isso:
Na guia Visão geral → Clique no endereço do contrato
Vá para a guia Código do contrato → Clique em Verificar e publicar



Quase lá ... Os seguintes passos são realmente importantes. Então olhe com cuidado. Basicamente, o que estamos fazendo aqui é tentar garantir que o código se encaixe no que você diz que está implantando e registrando na rede. PARA SEMPRE .
Então, se você cometer erros, estará errado para sempre. O que um amigo me disse isso no Blockchain:
Faça certo uma vez ou erre para sempre.
Agora você tem 5 coisas a fazer nesta página.
Verifique se o campo de endereço do contrato corresponde ao endereço do contrato que você acabou de implantar. Lembre-se de que o endereço do contrato é diferente do endereço MEW que você criou, portanto, certifique-se de não confundi-los

O nome do contrato deve corresponder ao do código, no meu caso é o seguinte: contract FucksToken. Isso estava na linha 102 do seu código
Para verificar qual versão do complier, volte para a página de remix de onde você obteve o BYTECODE e verifique o URL, a versão do complier estará lá. Na maioria dos casos, deve ser: 
v0.4.19 + commit.c4cbbb05.js, mas você deseja tentar os atualizados, se por acaso isso não funcionar.
Em Otimização , escolha Não (não a habilitamos antes).

Em INSIRA O CÓDIGO DE CONTRATO DE SOLIDITY ABAIXO, copie todo o código do Remix e cole nessa área. NÃO O BYTECODE, mas o próprio código. Também pode ser copiado do seu editor de texto.
Agora, deixe os outros campos em branco e clique em Verificar e publicar.
Mas esteja ciente ... Este é o momento que você estava esperando ... Está prestes a acontecer!
DEDOS CRUZADOS NOVAMENTE PELA VITALIK'S. 




O momento da verdade…


                                      Sucesso!


Se uma página de sucesso vier com marcas de verificação verdes e outras coisas, você conseguiu! 
Se aparecer uma mensagem vermelha ... tente novamente e veja onde você pode ter perdido um passo. Fico feliz em ajudar se você deixar um comentário abaixo, mas lembre-se de que o Google é seu melhor amigo 😉
Para confirmar que funciona, vá para https://ropsten.etherscan.io/ e verifique o seu endereço MEW, não o contrato, mas o seu endereço público. Se você pode ver suas moedas lá, agora pode relaxar e viver o sonho de criptografia em paz! Pelo menos até o próximo comício do BTC :)))))

Para poder enviar esses tokens, você precisa acessar sua conta MEW Visualizando Informações da Carteira → Acessando e inserindo sua Chave privada → Desbloqueando Carteira → Selecione a opção Carregar Tokens. Depois disso, eles serão transferíveis.



How To Create Your Own Ethereum Token In An Hour (ERC20 + Verified)
How to do an ICO on Ethereum in less than 20 minutes.

Referências:

https://www.youtube.com/watch?v=o7xoy0gbHO8
https://gist.github.com/Filip3Dev/9d32f54f35719f3b748c36ba75a4833a

http://remix.ethereum.org/

https://ethereum.github.io/browser-solidity

https://faucet.metamask.io/


Imagens:

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/k0a0svh2zwlfdh36dyr3.png)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v1etyzlfw8vtscxp1ohi.png)








