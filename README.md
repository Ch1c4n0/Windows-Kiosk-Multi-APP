# Windows Kiosk Multi APP

Este repositório contém exemplos de arquivos XML para configurar um ambiente Windows Kiosk com múltiplos aplicativos permitidos e fixados no menu iniciar.

## Arquivos

- **AllowedApps.xml**: Lista de aplicativos permitidos no modo Kiosk.
- **Complete_Configuration_kiosk.xml**: Configuração completa do Assigned Access, incluindo perfil, apps permitidos, restrições e pins do menu iniciar.
- **config.xml**: Configuração de conta e perfil padrão.
- **StartPins.xml**: Lista de aplicativos fixados no menu iniciar.

---

## Explicação dos Blocos XML

### AllowedApps.xml
```xml
<AllAppsList>
  <AllowedApps>
    <App AppUserModelId="Microsoft.WindowsCalculator_8wekyb3d8bbwe!App" />
    <App AppUserModelId="Microsoft.WindowsNotepad_8wekyb3d8bbwe!App" />
    <App AppUserModelId="Microsoft.Paint_8wekyb3d8bbwe!App" />
    <App AppUserModelId="Microsoft.Windows.Photos_8wekyb3d8bbwe!App" />
    <App AppUserModelId="windows.immersivecontrolpanel_cw5n1h2txyewy!microsoft.windows.immersivecontrolpanel" />
  </AllowedApps>
</AllAppsList>
```
- **AppUserModelId**: Identificador do aplicativo permitido no modo Kiosk.

### Complete_Configuration_kiosk.xml
```xml
<AssignedAccessConfiguration ...>
  <Profiles>
    <Profile Id="...">
      <AllAppsList>
        <AllowedApps>
          <App DesktopAppPath="C:\Windows\explorer.exe" />
          <App AppUserModelId="Microsoft.WindowsCalculator_8wekyb3d8bbwe!App" />
          <App DesktopAppPath="C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" />
        </AllowedApps>
      </AllAppsList>
      <rs5:FileExplorerNamespaceRestrictions>
        <rs5:AllowedNamespace Name="Downloads" />
        <v3:AllowRemovableDrives />
      </rs5:FileExplorerNamespaceRestrictions>
      <v5:StartPins><![CDATA[{
          "pinnedList":[
            {"packagedAppId":"Microsoft.WindowsCalculator_8wekyb3d8bbwe!App"},
            {"desktopAppLink":"%APPDATA%\\Microsoft\\Windows\\Start Menu\\Programs\\File Explorer.lnk"},
            {"desktopAppLink":"%ALLUSERSPROFILE%\\Microsoft\\Windows\\Start Menu\\Programs\\Microsoft Edge.lnk"}
          ]
        }]]></v5:StartPins>
      <Taskbar ShowTaskbar="true" />
    </Profile>
  </Profiles>
  <Configs>
    <Config>
      <Account>AzureAD\\diegos@lab.cloudinfocus.com.br</Account>
      <DefaultProfile Id="..." />
    </Config>
  </Configs>
</AssignedAccessConfiguration>
```
- **AllowedApps**: Apps permitidos para o usuário Kiosk.
- **FileExplorerNamespaceRestrictions**: Restringe acesso a áreas do Explorer.
- **StartPins**: Apps fixados no menu iniciar.
- **Taskbar**: Exibe ou oculta a barra de tarefas.
- **Account**: Conta do usuário.
- **DefaultProfile**: Perfil padrão do Assigned Access.

### config.xml
```xml
<Config>
  <Account>AzureAD\\diegos@lab.cloudinfocus.com.br</Account>
  <DefaultProfile Id="..." />
</Config>
```
- **Account**: Conta do usuário.
- **DefaultProfile**: Perfil padrão.

### StartPins.xml
```xml
<win11:StartPins>
  <![CDATA[  
    { "pinnedList":[
      {"packagedAppId":"Microsoft.WindowsCalculator_8wekyb3d8bbwe!App"},
      {"packagedAppId":"Microsoft.WindowsNotepad_8wekyb3d8bbwe!App"},
      {"packagedAppId":"Microsoft.Paint_8wekyb3d8bbwe!App"},
      {"packagedAppId":"Microsoft.Windows.Photos_8wekyb3d8bbwe!App"},
      {"packagedAppId":"windows.immersivecontrolpanel_cw5n1h2txyewy!microsoft.windows.immersivecontrolpanel"}
    ] }
  ]]>
</win11:StartPins>
```
- **pinnedList**: Lista de apps fixados no menu iniciar.

---

## Como configurar o Windows Kiosk

1. No Intune ou MDM, crie uma configuração personalizada.
2. Preencha os campos:
   - **Name**: AssignedAccess
   - **Description**: Not Configured
   - **OMA-URI**: ./Vendor/MSFT/AssignedAccess/Configuration
   - **Data type**: String (XML file)
   - **Custom XML**: Faça upload do arquivo XML desejado (ex: Complete_Configuration_kiosk.xml)

---

## Licença

Este projeto está licenciado sob a licença MIT. Consulte o arquivo LICENSE para mais detalhes.
