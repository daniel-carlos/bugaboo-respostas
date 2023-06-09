# Questões Teóricas

## 1) Descreva a diferença entre <b>Update</b>, Fixed<b>Update</b> e Late<b>Update</b> no Unity. Quando você usaria cada um deles?
<br>
    <b>Update</b> - será executado a cada atualização da tela (frame). A taxa de atualização (60 fps = função <b>Update</b> chamada 60 vezes por segundo).
    <br>
    É possível usar o Time.deltaTime para obter o tempo decorrido desde a última vez que o <b>Update</b> foi chamado.
    <br>
    Pode ser usado para atualizar o estado das entidades do jogo, posição dos objetos, input etc.
<br>
<br>
    <b>FixedUpdate</b>  - será executada a cada atualização da física do jogo e ocorre numa taxa fixa de vezes por segundo.
    <br>
    É possível usar o <b>Time.fixedDeltaTime</b> para obter o tempo decorrido desde a última vez que o <b>FixedUpdate</b> foi chamado.
    Pode ser usado para atualizar o estado da física dos objetos (como aplicar uma força num Rigidbody, por exemplo).
<br>
<br>
    <b>LateUpdate</b> - é executado após o <b>Update</b>.
    Pode ser usado para resetar o estado dos objetos preparando-os para o próximo frame. Gosto de usar para resetar alguns triggers do Animator (Animator.ResetTrigger()) que só seriam resetados "naturalmente" quando usados para disparar alguma animação. Isso evita que os triggers disparem animações "fora de timing".
<br>
<br>

## 2) Explique o que é e como funciona o sistema de Prefabs no Unity.
O sistema de prefabs possibilita reaproveitar configurações dos mais diversos tipos de objetos criando predefinições desses objetos que serão reutilizados. A Unity permite que o usuário crie um prefab a partir de um GameObject que poderá ter cópias facilmente inseridas na cena por meio do editor (arrasta e solta) ou pela função GameObject.Instantiate().
<br><br>
Também é possível criar variantes dos prefabs.
A utilização de prefabs é potencializada quando usada em conjunto com Scriptable Objects.


## 3) Qual é o propósito da função Awake() e como ela difere de Start()?
A função Awake() é chamada logo quando um gameObject é carregado na cena, enquanto que a função Start() é chamada apenas depois que todos os objetos já foram devidamente carregados e logo antes do primeiro frame da cena ser renderizado.
<br>
<br>
Inicializar objetos no Awake pode dar problemas se esse objeto precisa interagir com outros objetos que podem ainda não terem sido carregados. Por outro lado, usar o Awake pode garantir que um objeto já esteja devidamente configurado quando o Start for chamado.


## 4) Quais são as melhores práticas para gerenciar a memória em um jogo Unity?
1) Evitar chamar várias vezes num mesmo frame funções que custam muito processamento (FindObjectsOfType, SendMessage, etc).

1) Usar InvokeRepeating() em vez do <b>Update</b> para algumas tarefas que não precisam ser estritamente executadas a cada frame (tomar decisões baseadas em IA, por exemplo)

1) Centralizar informações comuns a muitos objetos (exemplo: se dezenas de inimigos compartilham informações, criar um objeto EnemyStrategy para guardar essas informações).

1) Usar object pooling para objectos que são instanciados e destruídos com frequência (exemplo: projéteis)

1) Carregar cenas em background (SceneManager.LoadSceneAsync)
Usar o profiler para encontrar gargalos.


## 5) Como você abordaria o problema de sincronização de estados em um jogo multiplayer?
<br>
    Para sincronizar as informações, usa-se o componente PhotonView (no caso da Photon Unity Network).
<br>
<br>
    Se for um jogo de ação em tempo real, usaria os componentes padrão de sincronização como o Photon Transform View, Photon Rigidbody View ou Photon Rigidbody2D View.
<br>
<br>
    Se for um jogo baseado em turnos, usaria RPCs (Remote Procedure Calls) para manter tudo atualizado.
