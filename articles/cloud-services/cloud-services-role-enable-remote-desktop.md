---
title: "aaaEnable pulpitu zdalnego w usługi w chmurze platformy Azure | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure platformy azure w chmurze usługi połączeń pulpitu zdalnego tooallow aplikacji"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Włączanie połączeń usług pulpitu zdalnego dla roli usług w chmurze Azure

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Program Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

Umożliwia Podłączanie pulpitu zdalnego w roli podczas tworzenia przez uwzględnienie hello modułów usług pulpitu zdalnego w definicji usługi. można też tooenable pulpitu zdalnego za pośrednictwem hello rozszerzenia usług pulpitu zdalnego. Hello preferowana metoda się toouse hello pulpitu zdalnego rozszerzenie można włączyć pulpitu zdalnego, nawet po wdrożeniu aplikacji hello bez konieczności tooredeploy aplikacji.

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a>Konfigurowanie pulpitu zdalnego z hello klasycznego portalu Azure
Hello klasycznego portalu Azure używa hello podejście rozszerzenia usług pulpitu zdalnego, więc można włączyć pulpitu zdalnego, nawet po wdrożeniu aplikacji hello. Witaj **Konfiguruj** strony dla usługi w chmurze pozwala tooenable pulpitu zdalnego, zmiana konta administratora lokalnego hello używane maszyny wirtualne toohello tooconnect, hello certyfikat używany podczas uwierzytelniania i ustawić hello Data wygaśnięcia.

1. Kliknij przycisk **usługi w chmurze**, kliknij nazwę hello hello usługi w chmurze, a następnie kliknij przycisk **Konfiguruj**.
2. Kliknij przycisk hello **zdalnego** u dołu hello.

    ![Usługi w chmurze zdalnego](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > Wszystkie wystąpienia roli zostanie ponownie uruchomiony, gdy najpierw włączyć pulpitu zdalnego i kliknij przycisk OK (znacznikiem wyboru). tooprevent ponowne uruchomienie komputera, hello certyfikatu używane tooencrypt hello hasło musi być zainstalowany na powitania roli. tooprevent ponowne uruchomienie, [przekazywanie certyfikatu dla usługi w chmurze hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , a następnie wróć toothis okna dialogowego.

3. W **ról**, wybierz rolę hello tooupdate lub wybierz **wszystkie** dla wszystkich ról.
4. Wprowadź jedną hello następujące zmiany:

   * tooenable pulpitu zdalnego, wybierz opcję hello **Włącz pulpit zdalny** pole wyboru. toodisable pulpitu zdalnego, hello wyczyść pole wyboru.
   * Utwórz konto toouse połączeń pulpitu zdalnego toohello wystąpień roli.
   * Zaktualizuj hasło hello hello istniejącego konta.
   * Wybierz toouse przekazano certyfikat dla uwierzytelniania (przekazywanie hello certyfikatu przy użyciu **przekazać** na powitania **certyfikaty** strony) lub Utwórz nowy certyfikat.
   * Zmień datę wygaśnięcia hello hello konfiguracji pulpitu zdalnego.

5. Po zakończeniu aktualizacji konfiguracji, kliknij przycisk **OK** (znacznikiem wyboru).

## <a name="remote-into-role-instances"></a>Zdalne do wystąpień roli
Włączenie pulpitu zdalnego na powitania role można zdalnego do wystąpienia roli za pomocą różnych narzędzi.

wystąpienie roli tooa tooconnect z hello klasycznego portalu Azure:

1. Kliknij przycisk **wystąpień** tooopen hello **wystąpień** strony.
2. Wybierz wystąpienia roli, który ma pulpitu zdalnego skonfigurowane.
3. Kliknij przycisk **Connect**i wykonaj hello instrukcje tooopen hello pulpitu.
4. Kliknij przycisk **Otwórz** , a następnie **Connect** toostart hello Podłączanie pulpitu zdalnego.

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a>Za pomocą programu Visual Studio tooremote do wystąpienia roli
W programie Visual Studio, Eksploratora serwera:

1. Rozwiń węzeł hello **Azure** > **usługi w chmurze** > **[nazwa usługi w chmurze]** węzła.
2. Rozwiń pozycję **przemieszczania** lub **produkcji**.
3. Rozwiń hello poszczególnych ról.
4. Kliknij prawym przyciskiem myszy jeden z wystąpień roli hello, kliknij przycisk **łączyć się przy użyciu pulpitu zdalnego...** , a następnie wprowadź hello nazwy użytkownika i hasła.

![Pulpit zdalny Eksploratora serwera](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a>Użyj pliku RDP hello tooget środowiska PowerShell
Można użyć hello [Get AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) plik RDP hello tooretrieve polecenia cmdlet. Plik RDP hello można następnie użyć z usługą w chmurze hello tooaccess Podłączanie pulpitu zdalnego.

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a>Programowo Pobierz plik RDP hello za pośrednictwem hello interfejs API REST zarządzania usługami
Można użyć hello [Pobierz plik RDP](https://msdn.microsoft.com/library/jj157183.aspx) plik RDP hello toodownload operacji REST.

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a>tooconfigure pulpitu zdalnego w pliku definicji usługi hello
Ta metoda umożliwia tooenable pulpitu zdalnego dla aplikacji hello podczas programowania. Ta metoda wymaga szyfrowania haseł można przechowywać w konfiguracji usługi plików i wszelkie aktualizacje toohello konfigurację pulpitu zdalnego wymaga ponownego wdrażania aplikacji hello. Jeśli chcesz, aby tooavoid tych downsides, należy użyć rozszerzenia usług pulpitu zdalnego hello na podstawie podejścia opisanego powyżej.  

Można użyć programu Visual Studio za[połączeń usług pulpitu zdalnego włączyć](../vs-azure-tools-remote-desktop-roles.md) podejście pliku definicji usługi hello.  
Poniższe kroki Hello opisano hello zmiany wymagane toohello usługi modelu pliki tooenable pulpitu zdalnego. Visual Studio będzie automatycznie tworzy te zmiany podczas publikowania.

### <a name="set-up-hello-connection-in-hello-service-model"></a>Skonfiguruj połączenie hello w modelu usług hello
Użyj hello **importów** hello tooimport elementu **RemoteAccess** modułu i hello **RemoteForwarder** toohello modułu [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) pliku.

Witaj pliku definicji usługi powinny być podobne toohello poniższy przykład z hello `<Imports>` elementu dodany.

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
Witaj [pliku ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) plik powinien być toohello podobnie poniższy przykład, należy zwrócić uwagę hello `<ConfigurationSettings>` i `<Certificates>` elementy. Witaj określony certyfikat musi być [przekazać usługi w chmurze toohello](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a>Dodatkowe zasoby
[Jak usługi w chmurze tooConfigure](cloud-services-how-to-configure.md)
[usług w chmurze — często zadawane pytania — pulpitu zdalnego](cloud-services-faq.md)
