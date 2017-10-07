---
title: "Azure Active Directory Domain Services: Aktualizowanie ustawień DNS dla sieci wirtualnej platformy Azure hello | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do usługi Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a>Aktualizowanie ustawień DNS dla hello sieci wirtualnej platformy Azure
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Zadanie 4: Aktualizowanie ustawień DNS na potrzeby hello sieci wirtualnej platformy Azure
W hello poprzedzających zadania konfiguracji została pomyślnie włączona Azure Active Directory Domain Services dla katalogu. następne zadanie Hello jest tooensure, że komputery w sieci wirtualnej hello łączyć i korzystanie z tych usług. W tym artykule należy zaktualizować ustawienia serwera DNS hello sieci wirtualnej toopoint toohello dwa adresy IP gdzie usług domenowych Azure Active Directory jest dostępny w sieci wirtualnej hello.

> [!NOTE]
> Po włączeniu usługi Azure Active Directory Domain Services dla katalogu hello Uwaga hello adresów IP dla usługi Azure Active Directory Domain Services, które są wyświetlane na powitania **Konfiguruj** katalogu.
>
>

tooupdate hello ustawienia serwera DNS dla sieci wirtualnej hello, w której włączono usługi Azure Active Directory Domain Services, pełną hello następujące kroki:

1. Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. Wybierz w okienku po lewej stronie powitania **sieci**.  
    Witaj **sieci** zostanie otwarte okno.

    ![Okno Sieci wirtualne](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. Na powitania **sieci wirtualnych** kartę, zaznacz hello sieci wirtualnej, w której włączono usługi Azure Active Directory Domain Services tooview jego właściwości.
4. Kliknij przycisk hello **Konfiguruj** kartę.

    ![Okno Sieci wirtualne](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. W hello **serwerów DNS** wprowadź zarówno hello adresów IP, które były wyświetlane w hello **usług domenowych w usłudze** sekcji na powitania **Konfiguruj** katalogu.
6. Kliknij przycisk Ustawienia serwera DNS hello toosave tej sieci wirtualnej, w okienku zadań hello u dołu okna hello hello **zapisać**.

   ![Zaktualizuj ustawienia serwera DNS hello hello sieci wirtualnej](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  Maszyny wirtualne w sieci hello pobierają tylko nowe ustawienia DNS powitania po ponownym uruchomieniu. Jeśli potrzebne ustawienia DNS tooget hello zaktualizowane od razu, wyzwolić ponowne uruchomienie komputera przez hello portal, programu PowerShell lub hello interfejsu wiersza polecenia.
>
>

## <a name="next-steps"></a>Następne kroki
Zadanie 5: [włączyć tooAzure synchronizacji haseł usług domenowych w usłudze Active Directory](active-directory-ds-getting-started-password-sync.md)
