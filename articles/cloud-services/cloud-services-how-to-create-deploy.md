---
title: "aaaHow toocreate i wdrażania usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i wdrażania usługi w chmurze przy użyciu metody szybkie tworzenie hello na platformie Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Jak tooCreate i wdrażania usługi w chmurze
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-how-to-create-deploy-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-how-to-create-deploy.md)
> 
> 

Witaj klasyczny portal Azure udostępnia dwa sposoby dla Ciebie toocreate i wdrażania usługi w chmurze: **szybkie tworzenie** i **Utwórz niestandardowy**.

W tym temacie opisano sposób toouse hello toocreate metody szybkie tworzenie nowej usługi w chmurze, a następnie użyj **przekazać** tooupload i wdrażanie pakietu usług chmury na platformie Azure. Korzystając z tej metody, hello klasycznego portalu Azure sprawia, że dostępne wygodne łącza ukończenia wszystkich wymagań w trakcie pracy. Jeśli wszystko jest gotowe toodeploy chmury usługi podczas jego tworzenia, możesz to zrobić zarówno na powitania przy użyciu tego samego czasu **Utwórz niestandardowy**.

> [!NOTE]
> Jeśli planujesz toopublish usługi w chmurze z programu Visual Studio Team Services (VSTS), użyj **szybkie tworzenie**, a następnie skonfigurować publikowanie programu VSTS z **Szybki Start** lub hello pulpitu nawigacyjnego.
> 
> 

## <a name="concepts"></a>Pojęcia
W kolejności toodeploy aplikacji jako chmury usługi na platformie Azure wymagane są trzy składniki:

* **Definicja usługi**  
  Witaj chmury pliku definicji usługi (csdef) definiuje hello usługi modelu, w tym hello liczba ról.
* **Konfiguracja usługi**  
  plik konfiguracji usługi chmury Hello (cscfg) zawiera ustawienia konfiguracji dla usługi w chmurze hello i poszczególne role, w tym hello liczby wystąpień roli.
* **Pakiet usługi**  
  pakiet usługi Hello (cspkg) zawiera kod aplikacji hello i konfiguracji i pliku definicji usługi hello.

Dowiedz się więcej na temat tych i w jaki sposób toocreate pakietu [tutaj](cloud-services-model-and-package.md).

## <a name="prepare-your-app"></a>Przygotowanie aplikacji
Przed wdrożeniem usługi w chmurze, należy utworzyć pakiet usługi chmury hello (cspkg) w kodzie aplikacji i pliku konfiguracji usługi chmury (cscfg). Hello Azure SDK zawiera narzędzia do przygotowania te pliki wymagane wdrożenie. Witaj zestawu SDK można zainstalować z hello [Azure pobiera](https://azure.microsoft.com/downloads/) strony w języku hello, w którym chcesz toodevelop kod aplikacji.

Trzy funkcje usługi chmury wymagają specjalnych konfiguracji przed wyeksportowaniem pakietu usług:

* Jeśli chcesz, aby usługa w chmurze, która używa protokołu Secure Sockets Layer (SSL) do szyfrowania danych toodeploy [konfigurowania aplikacji](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) dla protokołu SSL.
* Jeśli chcesz, aby tooconfigure wystąpień toorole połączeń usług pulpitu zdalnego, [konfigurowania ról hello](cloud-services-role-enable-remote-desktop.md) dla pulpitu zdalnego.
* Tooconfigure pełne, monitorowanie dla usługi w chmurze, należy włączyć diagnostyki Azure dla usługi w chmurze hello. *Monitorowanie minimalnego* (domyślnie hello monitorowania poziomu) używa liczniki wydajności zebrane z hello systemy operacyjne hosta dla wystąpień roli (maszyny wirtualne). "Monitorowanie pełne * zbiera dodatkowe metryki na podstawie danych wydajności w ramach hello roli wystąpień tooenable bliżej analizy problemy występujące podczas przetwarzania aplikacji. toofind się, jak tooenable diagnostyki Azure, zobacz [Włączanie diagnostyki na platformie Azure](cloud-services-dotnet-diagnostics.md).

toocreate usługi w chmurze z wdrożeniami role sieci web lub roli proces roboczy musi [Utwórz pakiet usługi hello](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Przed rozpoczęciem
* Nie zainstalowano hello Azure SDK, kliknij przycisk **Zainstaluj zestaw Azure SDK** tooopen hello [Azure pobiera strony](https://azure.microsoft.com/downloads/), a następnie pobrać hello zestawu SDK dla języka hello, w którym chcesz toodevelop kodu. (Należy toodo możliwości to później.)
* Jeśli wszystkie wystąpienia roli jest wymagany certyfikat, należy utworzyć hello certyfikatów. Usługi w chmurze wymagają pliku pfx z kluczem prywatnym. Możesz [przekazać hello certyfikaty tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) podczas tworzenia i wdrażania usługi w chmurze hello.
* Jeśli planujesz grupy koligacji tooan usługi w chmurze hello toodeploy, należy utworzyć grupę koligacji hello. Usługi w chmurze i innych usług Azure toohello służy toodeploy grupy koligacji tej samej lokalizacji w regionie. Można utworzyć grupy koligacji hello w hello **sieci** obszaru hello klasycznego portalu Azure na powitania **grup koligacji** strony.

## <a name="how-to-create-a-cloud-service-using-quick-create"></a>Porady: Tworzenie usługi w chmurze przy użyciu szybkie tworzenie
1. W hello [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **nowy**>**obliczeniowe**>**usługi w chmurze** > **Szybkie tworzenie**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. W **adres URL**, wprowadź toouse nazwę poddomeny w hello publiczny adres URL do uzyskiwania dostępu do usługi w chmurze we wdrożeniach produkcyjnych. format adresu URL Hello wdrożeń produkcyjnych jest: http://*myURL*. cloudapp.net.
3. W **Region lub grupę koligacji**, wybierz hello geograficzne region lub grupę koligacji toodeploy hello usługi w chmurze. Wybierz grupy koligacji, jeśli chcesz toodeploy Twojego toohello usługi chmury tej samej lokalizacji co innymi usługami Azure w ramach regionu.
4. Kliknij pozycję **Utwórz usługę w chmurze**.
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    Można monitorować stan hello procesu hello w obszarze wiadomość hello u dołu okna hello hello.
   
    Witaj **usługi w chmurze** powoduje otwarcie obszaru hello wyświetlane nowe usługi chmury. Po zmianie stanu hello tooCreated tworzenia usługi chmury została pomyślnie ukończona.
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a>Porady: przekazywanie certyfikatu dla usługi w chmurze
1. W hello [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, kliknij nazwę hello hello usługi w chmurze, a następnie kliknij przycisk **certyfikaty**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. Kliknij opcję **przekazać certyfikat** lub **przekazać**.
3. W **pliku**, użyj **Przeglądaj** tooselect hello certyfikatu (pfx).
4. W **hasło**, wprowadź hello klucza prywatnego dla certyfikatu hello.
5. Kliknij przycisk **OK** (znacznikiem wyboru).
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    Możesz obserwować postęp hello przekazywania hello w obszarze wiadomość hello, pokazano poniżej. Po ukończeniu przekazywania hello hello certyfikat zostanie dodany toohello tabeli. W obszarze wiadomość hello kliknij przycisk OK tooclose wiadomość hello.
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a>Porady: Wdrażanie usługi w chmurze
1. W hello [klasycznego portalu Azure](http://manage.windowsazure.com/), kliknij przycisk **usługi w chmurze**, kliknij nazwę hello hello usługi w chmurze, a następnie kliknij przycisk **pulpitu nawigacyjnego**.
2. Kliknij opcję **przekazania nowego wdrożenia produkcyjnego** lub **przekazać**.
3. W **etykieta wdrożenia**, wprowadź nazwę nowego hello wdrożenia — na przykład MyCloudServicev4.
4. W **pakietu**, użyj **Przeglądaj** toouse pakietu usługi tooselect hello w pliku (cspkg).
5. W **konfiguracji**, użyj **Przeglądaj** usługa hello tooselect skonfigurować toouse pliku (cscfg).
6. Jeśli usługa w chmurze hello będą zawierać żadnych ról z tylko jednym wystąpieniem, zaznacz hello **Wdróż, nawet jeśli co najmniej jedna rola zawiera pojedyncze wystąpienie** tooproceed wdrożenia hello tooenable pole wyboru.
   
    Co rola ma co najmniej dwa wystąpienia Azure tylko może zagwarantować usługi w chmurze toohello 99,95% dostępu podczas konserwacji i obsługi aktualizacji. W razie potrzeby można dodać wystąpienia dodatkowych ról na powitania **skali** strony po wdrożeniu usługi w chmurze hello. Aby uzyskać więcej informacji, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/).
7. Kliknij przycisk **OK** wdrożenie usługi chmury hello toobegin (znacznikiem wyboru).
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    Można monitorować stan hello hello wdrożenia w obszarze wiadomość hello. Kliknij przycisk OK toohide wiadomość hello.
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a>Sprawdź wdrożenia ukończone pomyślnie
1. Kliknij przycisk **pulpitu nawigacyjnego**.
   
    Witaj stan powinien pokazują, że usługa hello jest **systemem**.
2. W obszarze **szybkiego dostępu**, kliknij przycisk tooopen adres URL witryny hello usługi w chmurze w przeglądarce sieci web.
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a>Następne kroki
* [Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure.md).
* Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name.md).
* [Usługi w chmurze zarządzanie](cloud-services-how-to-manage.md).
* Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate.md).

