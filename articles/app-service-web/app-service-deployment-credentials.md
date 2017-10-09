---
title: "aaaAzure poświadczenia wdrożenia usługi aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello poświadczenia wdrożenia usługi Azure App Service."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a>Skonfiguruj poświadczenia wdrażania dla usługi Azure App Service
[Usługa aplikacji Azure](http://go.microsoft.com/fwlink/?LinkId=529714) obsługuje dwa rodzaje poświadczenia [lokalnego wdrożenia Git](app-service-deploy-local-git.md) i [wdrożenia FTP/S](app-service-deploy-ftp.md). Są one nie hello taki sam jak swoje poświadczenia usługi Azure Active Directory.

* **Poświadczenia użytkownika na poziomie**: jeden zestaw poświadczeń hello całego konta Azure. Może być używane toodeploy tooApp usługi dla wszystkich aplikacji, w dowolnej subskrypcji, która hello konta Azure ma tooaccess uprawnienia. Są to hello domyślne poświadczenia zestaw, który należy skonfigurować w **usługi aplikacji** > **&lt;nazwa_aplikacji >** > **poświadczenia wdrażania**. To jest również hello domyślnego zestawu, który jest wyświetlana w portalu hello graficznego interfejsu użytkownika (takich jak hello **omówienie** i **właściwości** aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources)).

    > [!NOTE]
    > Podczas delegować dostęp do zasobów tooAzure za pomocą kontroli dostępu na podstawie ról (RBAC) lub współadministratora uprawnienia, każdy użytkownik usługi Azure, który otrzymuje dostęp tooan aplikacji można użyć jego osobistych poświadczeń na poziomie użytkownika do momentu dostęp został odwołany. Te poświadczenia wdrożenia nie powinny być udostępniać innym użytkownikom Azure.
    >
    >

* **Poświadczeń na poziomie aplikacji**: jeden zestaw poświadczeń dla każdej aplikacji. Może być używane toodeploy toothat tylko aplikacji. Witaj poświadczeń dla każdej aplikacji jest generowany automatycznie podczas tworzenia aplikacji i znajduje się w aplikacji hello profilu publikowania. Nie można ręcznie skonfigurować hello poświadczeń, ale można je zresetować w każdej chwili dla aplikacji.

    > [!NOTE]
    > W kolejności toogive komuś dostęp toothese poświadczeń za pomocą roli na podstawie kontroli dostępu (RBAC), należy toomake ich współautora lub nowszej na powitania aplikacji sieci Web. Czytniki nie są dozwolone toopublish i dlatego nie można uzyskać dostępu do tych poświadczeń.
    >
    >

## <a name="userscope"></a>Ustaw i zresetowanie poświadczeń na poziomie użytkownika

Poświadczenia na poziomie użytkownika można skonfigurować w dowolnej aplikacji [bloku zasobów](../azure-resource-manager/resource-group-portal.md#manage-resources). Niezależnie od tego w aplikacji należy skonfigurować te poświadczenia, stosuje tooall aplikacji, a wszystkie subskrypcje w Azure kont. 

tooconfigure poświadczeń na poziomie użytkownika:

1. W hello [portalu Azure](https://portal.azure.com), kliknij opcję usługi aplikacji >  **&lt;any_app >** > **poświadczenia wdrażania**.

    > [!NOTE]
    > W portalu hello musi mieć co najmniej jedną aplikację, zanim dostęp do bloku poświadczenia wdrożenia hello. Jednak w przypadku hello [interfejsu wiersza polecenia Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), można skonfigurować poświadczeń na poziomie użytkownika bez istniejącej aplikacji.

2. Skonfiguruj hello nazwę użytkownika i hasło, a następnie kliknij przycisk **zapisać**.

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

Po ustawieniu poświadczenia wdrażania, można znaleźć hello *Git* username wdrożenia w aplikacji **omówienie**,

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

i i *FTP* username wdrożenia w aplikacji **właściwości**.

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> Azure nie są wyświetlane hasło użytkownika na poziomie wdrożenia. Jeśli zapomnisz hasła hello, nie można go pobrać. Jednak można zresetować swoje poświadczenia, wykonując kroki hello w tej sekcji.
>
>  

## <a name="appscope"></a>Pobierz i zresetowanie poświadczeń na poziomie aplikacji
Dla każdej aplikacji w usłudze App Service, jego poświadczeń na poziomie aplikacji są przechowywane w hello XML profilu publikowania.

tooget poświadczeń na poziomie aplikacji hello:

1. W hello [portalu Azure](https://portal.azure.com), kliknij opcję usługi aplikacji >  **&lt;any_app >** > **omówienie**.

2. Kliknij przycisk **... Więcej** > **profilu publikowania Get**, i uruchamia pobierania. Plik ustawień publikacji.

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. Otwórz hello. Plik ustawień publikacji i Znajdź hello `<publishProfile>` tag z atrybutem hello `publishMethod="FTP"`. Następnie należy pobrać jego `userName` i `password` atrybutów.
Są to hello poświadczeń na poziomie aplikacji.

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    Podobne poświadczeń na poziomie użytkownika toohello, username wdrożenia hello FTP jest w formacie hello `<app_name>\<username>`, oraz nazwy użytkownika wdrożenia Git hello jest po prostu `<username>` bez hello poprzedniego `<app_name>\`.

tooreset poświadczeń na poziomie aplikacji hello:

1. W hello [portalu Azure](https://portal.azure.com), kliknij opcję usługi aplikacji >  **&lt;any_app >** > **omówienie**.

2. Kliknij przycisk **... Więcej** > **Resetowanie profilu publikowania**. Kliknij przycisk **tak** tooconfirm hello resetowania.

    Akcja reset Hello unieważnia żadnego pobrane wcześniej. Pliki ustawień publikacji.

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toouse toodeploy te poświadczenia aplikacji z [lokalnego Git](app-service-deploy-local-git.md) lub przy użyciu [FTP/S](app-service-deploy-ftp.md).
