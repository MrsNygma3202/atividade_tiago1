# GameManager - Atividade Avaliativa

## Descrição

Este projeto implementa um **GameManager** que segue o padrão **Singleton** e gerencia:
- **Estados do jogo** usando enum (Iniciando, MenuPrincipal, Gameplay)
- **Carregamento de cenas** como ponto único de acesso
- **Alocação de inputs** para jogadores usando o Input System

## Arquitetura

### Estrutura de Cenas

1. **_Boot** (Cena Inicial)
   - Contém todos os Managers singletons do jogo
   - Inicializa o GameManager
   - Carrega automaticamente a cena Splash

2. **Splash** (Cena de Apresentação)
   - Exibe uma imagem por 2 segundos
   - Carrega automaticamente a cena MenuPrincipal

3. **MenuPrincipal** (Cena de Menu)
   - Interface UGUI com 2 botões
   - **Botão "Iniciar Jogo"**: Carrega SampleScene
   - **Botão "Sair"**: Encerra a aplicação

4. **SampleScene** (Cena de Gameplay)
   - Cena de jogabilidade principal
   - GameManager muda para estado Gameplay

### Componentes C#

- **GameManager.cs**: Singleton que gerencia estados, carregamento de cenas e inputs
- **GameState.cs**: Enum com os estados possíveis do jogo
- **BootManager.cs**: Gerencia a inicialização da cena _Boot
- **SplashScreenManager.cs**: Controla o tempo de exibição do Splash
- **MainMenuManager.cs**: Gerencia botões do menu principal
- **SceneSetupHelper.cs**: Script editor que cria automaticamente as cenas

## Como Usar

### Primeira Execução

1. Abra o projeto no Unity
2. Vá em **Game → Setup Scenes** no menu superior
3. Isso criará automaticamente todas as cenas necessárias
4. Aguarde a conclusão do processo

### Executar o Jogo

1. Selecione a cena **_Boot** em `Assets/Scenes/_Boot.unity`
2. Pressione **Play** para iniciar
3. O fluxo será:
   - _Boot (Estado: Iniciando) 
   - → Splash (mostra imagem por 2 segundos)
   - → MenuPrincipal (Estado: MenuPrincipal)
   - → SampleScene (Estado: Gameplay)

### Monitorar Estados

Abra o **Console** (Window → General → Console) para ver:
- Mudanças de estado do GameManager
- Carregamento de cenas
- Status de inicialização

### Build Settings

O arquivo `EditorBuildSettings.asset` será atualizado automaticamente com a seguinte ordem:
- 0: Assets/Scenes/_Boot.unity
- 1: Assets/Scenes/Splash.unity
- 2: Assets/Scenes/MenuPrincipal.unity
- 3: Assets/Scenes/SampleScene.unity

## Estados do Jogo

```csharp
public enum GameState
{
    Iniciando,      // Cena _Boot
    MenuPrincipal,  // Cena MenuPrincipal
    Gameplay        // Cena SampleScene
}
```

## Padrão Singleton - GameManager

O GameManager implementa o padrão Singleton garantindo:
- Apenas uma instância existe durante o jogo
- Persiste entre cenas usando `DontDestroyOnLoad`
- Acesso global via `GameManager.Instance`

```csharp
// Acessar de qualquer lugar
GameManager.Instance.LoadScene("SampleScene");
GameManager.Instance.CurrentState  // Obtém estado atual
```

## Input System

O GameManager aloca automaticamente o `PlayerInput` do Input System configurado no projeto:
- Acessa o arquivo de ações: `InputSystem_Actions.inputactions`
- Prepara o sistema para receber inputs dos jogadores

## Debug Logs

Todos os eventos importantes são logados no Console:
```
[GameManager] Singleton inicializado
[GameManager] GameManager iniciado no estado: Iniciando
[GameManager] Input alocado para o jogador
[GameManager] Estado do jogo mudou para: Iniciando
[BootManager] Boot iniciado - Carregando configuração inicial
[BootManager] Carregando cena Splash
[SplashScreenManager] Exibindo splash screen por 2 segundos
[GameManager] Carregando cena: MenuPrincipal
[GameManager] Cena carregada: MenuPrincipal
[GameManager] Estado do jogo mudou para: MenuPrincipal
[MainMenuManager] Menu Principal iniciado
```

## Próximas Melhorias

- [ ] Adicionar transições entre cenas
- [ ] Sistema de sons
- [ ] Sistema de salvamento e carregamento
- [ ] Suporte para múltiplos jogadores
- [ ] Sistema de events para comunicação entre componentes

## Requisitos

- Unity 2023 LTS ou superior
- Input System configurado
- UGUI (Canvas, Button, Image, Text)

## Notas Importantes

1. A cena **_Boot** deve sempre ser a primeira a ser carregada
2. O **GameManager** não pode ser destruído entre cenas
3. Qualquer carregamento de cena deve passar pelo **GameManager.LoadScene()**
4. Os estados do jogo são sincronizados com as cenas automaticamente

## Autor

Atividade Avaliativa - Gerenciamento de Estados e Cenas em Unity

