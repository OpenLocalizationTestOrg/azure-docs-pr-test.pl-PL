---
title: "aaaHow toocreate i wdrażania usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i wdrażania usługi w chmurze przy użyciu hello portalu Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>Jak toocreate i wdrażania usługi w chmurze
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](cloud-services-how-to-create-deploy-portal.md)
> * [Klasyczna witryna Azure Portal](cloud-services-how-to-create-deploy.md)
>
>

Witaj Azure portal udostępnia dwa sposoby dla Ciebie toocreate i wdrażania usługi w chmurze: *szybkie tworzenie* i *Utwórz niestandardowy*.

W tym artykule opisano sposób toouse hello toocreate metody szybkie tworzenie nowej usługi w chmurze, a następnie użyj **przekazać** tooupload i wdrażanie pakietu usług chmury na platformie Azure. Korzystając z tej metody, hello portalu Azure sprawia, że dostępne wygodne łącza ukończenia wszystkich wymagań w trakcie pracy. Jeśli wszystko jest gotowe toodeploy chmury usługi podczas jego tworzenia, możesz to zrobić zarówno na powitania tym samym czasie przy użyciu Utwórz niestandardowy.

> [!NOTE]
> Jeśli planujesz toopublish usługi w chmurze z programu Visual Studio Team Services (VSTS), użyj szybkie tworzenie, a następnie skonfigurować publikowanie programu VSTS z hello Szybki Start Azure lub hello pulpitu nawigacyjnego. Aby uzyskać więcej informacji, zobacz [tooAzure ciągłego dostarczania przy użyciu programu Visual Studio Team Services][TFSTutorialForCloudService], lub można znaleźć w pomocy hello **Szybki Start** strony.
>
>

## <a name="concepts"></a>Pojęcia
Trzy składniki są wymagane toodeploy aplikacji jako usługa w chmurze na platformie Azure:

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

* Jeśli chcesz, aby usługa w chmurze, która używa protokołu Secure Sockets Layer (SSL) do szyfrowania danych toodeploy [konfigurowania aplikacji](cloud-services-configure-ssl-certificate-portal.md#modify) dla protokołu SSL.
* Jeśli chcesz, aby tooconfigure wystąpień toorole połączeń usług pulpitu zdalnego, [konfigurowania ról hello](cloud-services-role-enable-remote-desktop-new-portal.md) dla pulpitu zdalnego.
* Tooconfigure pełne, monitorowanie dla usługi w chmurze, należy włączyć diagnostyki Azure dla usługi w chmurze hello. *Monitorowanie minimalnego* (domyślnie hello monitorowania poziomu) używa liczniki wydajności zebrane z hello systemy operacyjne hosta dla wystąpień roli (maszyny wirtualne). *Monitorowanie pełne* zbiera dodatkowe metryki na podstawie danych wydajności w ramach hello roli wystąpień tooenable bliżej analizy problemy występujące podczas przetwarzania aplikacji. toofind się, jak tooenable diagnostyki Azure, zobacz [Włączanie diagnostyki na platformie Azure](cloud-services-dotnet-diagnostics.md).

toocreate usługi w chmurze z wdrożeniami role sieci web lub roli proces roboczy musi [Utwórz pakiet usługi hello](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Przed rozpoczęciem
* Nie zainstalowano hello Azure SDK, kliknij przycisk **Zainstaluj zestaw Azure SDK** tooopen hello [Azure pobiera strony](https://azure.microsoft.com/downloads/), a następnie pobrać hello zestawu SDK dla języka hello, w którym chcesz toodevelop kodu. (Należy toodo możliwości to później.)
* Jeśli wszystkie wystąpienia roli jest wymagany certyfikat, należy utworzyć hello certyfikatów. Usługi w chmurze wymagają pliku pfx z kluczem prywatnym. Podczas tworzenia i wdrażania usługi w chmurze hello możesz przekazać hello tooAzure certyfikatów.

## <a name="create-and-deploy"></a>Tworzenie i wdrażanie
1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **nowy > obliczeniowe**, a następnie przewiń w dół kliknij tooand **usługi w chmurze**.

    ![Publikowanie usługi w chmurze](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. W nowych hello **usługi w chmurze** bloku, wprowadź wartość dla hello **nazwy DNS**.
4. Utwórz nową **grupy zasobów** lub wybierz istniejący.
5. Wybierz **lokalizację**.
6. Kliknij przycisk **pakietu**. Spowoduje to otwarcie hello **przekazania pakietu** bloku. Wypełnij pola hello wymagane. Jeśli jakieś role zawierają pojedynczego wystąpienia, upewnij się, **Wdróż, nawet jeśli co najmniej jedna rola zawiera pojedyncze wystąpienie** jest zaznaczone.
7. Upewnij się, że **rozpocząć wdrażanie** jest zaznaczone.
8. Kliknij przycisk **OK** którego zostanie zamknięte hello **przekazania pakietu** bloku.
9. Jeśli nie masz żadnych tooadd certyfikatów, kliknij przycisk **Utwórz**.

    ![Publikowanie usługi w chmurze](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>Przekaż certyfikat
Jeśli pakiet wdrażania [skonfigurowanych certyfikatów toouse](cloud-services-configure-ssl-certificate-portal.md#modify), możesz teraz przekazać hello certyfikatu.

1. Wybierz **certyfikaty**, a na powitania **Dodaj certyfikaty** bloku, wybierz plik .pfx certyfikatu SSL hello, a następnie podaj hello **hasło** certyfikatu hello
2. Kliknij przycisk **certyfikatu Attach**, a następnie kliknij przycisk **OK** na powitania **Dodaj certyfikaty** bloku.
3. Kliknij przycisk **Utwórz** na powitania **usługi w chmurze** bloku. Podczas wdrażania hello osiągnęła hello **gotowe** stanu, możesz przejść toohello następne kroki.

    ![Publikowanie usługi w chmurze](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>Sprawdź wdrożenia ukończone pomyślnie
1. Kliknij przycisk wystąpienie usługi w chmurze hello.

    Witaj stan powinien pokazują, że usługa hello jest **systemem**.
2. W obszarze **Essentials**, kliknij przycisk hello **adres URL witryny** tooopen usługi chmury w przeglądarce sieci web.

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>Następne kroki
* [Konfiguracja ogólna usługi w chmurze](cloud-services-how-to-configure-portal.md).
* Skonfiguruj [niestandardowej nazwy domeny](cloud-services-custom-domain-name-portal.md).
* [Usługi w chmurze zarządzanie](cloud-services-how-to-manage-portal.md).
* Skonfiguruj [certyfikaty ssl](cloud-services-configure-ssl-certificate-portal.md).
