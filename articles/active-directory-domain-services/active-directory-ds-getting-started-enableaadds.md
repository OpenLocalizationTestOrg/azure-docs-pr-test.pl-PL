---
title: "Azure Active Directory Domain Services: Włączanie usług Azure Active Directory Domain Services | Microsoft Docs"
description: "Włączanie usługi Azure Active Directory Domain Services przy użyciu hello klasycznego portalu Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Włączanie usługi Azure Active Directory Domain Services przy użyciu hello klasycznego portalu Azure

## <a name="task-3-enable-azure-active-directory-domain-services"></a>Zadanie 3. Włączanie usług Azure Active Directory Domain Services
W tym zadaniu można włączyć usługi Azure Active Directory Domain Services (Azure AD DS) dla katalogu, wykonując następujące kroki hello:

1. Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com).
2. W okienku po lewej stronie powitania wybierz hello **usługi Active Directory** przycisku.
3. Wybierz dzierżawę usługi Azure Active Directory (Azure AD) hello (katalog) dla której ma zostać tooenable Azure usług AD DS.

    ![Wybieranie katalogu usługi Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Na powitania **katalogu podglądu** kliknij przycisk hello **Konfiguruj** kartę.

    ![Karta Konfigurowanie w katalogu](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. W obszarze **usług domenowych w usłudze**, zmień hello **włączyć usługi domenowe dla tego katalogu** opcję zbyt**tak**.  
    Na stronie powitania pojawią się dodatkowe opcje konfiguracji usług domenowych Azure Active Directory.

    ![Włączanie Usług domenowych](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > Po włączeniu usługi Azure Active Directory Domain Services dla dzierżawy usługi Azure AD generuje i przechowuje hello protokołu Kerberos i NTLM skrótów poświadczeń wymaganych do uwierzytelniania użytkowników.
   >
   >
6. Określ hello **nazwy domeny DNS, usług domenowych**.

   * Domyślna nazwa domeny Hello hello katalogu (z **. onmicrosoft.com** sufiks) jest domyślnie zaznaczona.

   * Witaj lista zawiera wszystkie domeny, które zostały skonfigurowane dla katalogu usługi Azure AD, w tym zarówno zweryfikowane i niezweryfikowanych domen, które są konfigurowane na powitania **domen** kartę.

   * Możesz również podać niestandardową nazwę domeny. W tym przykładzie hello niestandardowa nazwa domeny jest *contoso100.com*.

     > [!WARNING]
     > Prefiks nazwy domeny określonej Hello (na przykład *contoso100* w hello *contoso100.com* nazwa domeny) musi zawierać więcej niż 15 znaków. Nie możesz utworzyć domeny usługi Azure Active Directory Domain Services z prefiksem zawierającym ponad 15 znaków.
     >
     >
7. Upewnij się, tym hello domeny DNS wybrana dla hello zarządzane domeny nie istnieje już w sieci wirtualnej hello. W szczególności sprawdź czy toosee:

   * Masz już domenę z hello tą samą nazwą domeny DNS w sieci wirtualnej hello.

   * Witaj sieć wirtualna wybrana została ma połączenie VPN z siecią lokalną i masz domenę z hello tą samą nazwą domeny DNS w sieci lokalnej.

   * Masz istniejącą usługę w chmurze o tej nazwie na powitania sieci wirtualnej.
8. Wybierz sieć wirtualną, na którym ma być dostępna toobe usług domenowych Azure Active Directory. Wybierz hello sieci wirtualnej i podsieci dedykowanego utworzony w hello **toothis sieci wirtualnej z usług domenowych Connect** listy rozwijanej. Należy również rozważyć następujące hello:

   * Upewnij się, że w tej sieci wirtualnej hello, które zostały określone należy tooan region platformy Azure, który jest obsługiwany przez usługi Azure Active Directory Domain Services. tooascertain hello regiony platformy Azure, w którym usługi Azure Active Directory Domain Services jest dostępna, zobacz [usług Azure według regionu](https://azure.microsoft.com/regions/#services/).

   * Sieci wirtualne należące do regionu tooa których Azure Active Directory Domain Services nie jest obsługiwana nie są wyświetlane na liście rozwijanej hello.

   * Użyj dedykowanych podsieci w sieci wirtualnej hello Azure Active Directory Domain Services. Czy *nie* wybierz hello podsieci bramy. Zobacz [zagadnienia dotyczące pracy w sieci](active-directory-ds-networking.md).

   * Podobnie sieci wirtualnych, które zostały utworzone przy użyciu usługi Azure Resource Manager nie są wyświetlane na liście rozwijanej hello. Sieci wirtualne oparte na usłudze Resource Manager nie są obecnie obsługiwane przez usługi Azure Active Directory Domain Services.
9. Kliknij tooenable Azure Active Directory Domain Services, w okienku zadań hello u dołu strony hello hello **zapisać**.
    * Azure Active Directory Domain Services jest włączana dla katalogu, strona hello Wyświetla stan *oczekujące*.

        ![Okno włączania usług domenowych](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > Usługi Azure Active Directory Domain Services oferują wysoką dostępność na potrzeby domeny zarządzanej. Po włączeniu usług domenowych Azure Active Directory w domenie, które usługi są dostępne w sieci wirtualnej hello adresy IP hello są wyświetlane pojedynczo. Hello drugiego adresu IP jest wyświetlany wkrótce po hello najpierw, jak szybko hello usługa zapewni wysoką dostępność domeny. Gdy skonfigurowano wysokiej dostępności i aktywne dla domeny, powinny być widoczne dwa adresy IP w hello **usług domenowych w usłudze** sekcji hello **Konfiguruj** kartę.
        >
        >
    * Po upływie około 20 minut too30, hello pierwszy adres IP w domenie, które usługi są dostępne w Twojej sieci wirtualnej w hello **adres IP** na powitania **Konfiguruj** strony.

        ![Okno usług domenowych wyświetlające pierwszy aprowizowany adres IP](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * Gdy domena oferuje działającą jest wysoka dostępność, dwa adresy IP są wyświetlane na stronie powitania. Twoja domena zarządzana jest dostępna w wybranej sieci wirtualnej pod tymi dwoma adresami IP.

10. Należy zwrócić uwagę hello dwa adresy IP tak, aby umożliwić aktualizację hello ustawienia DNS dla sieci wirtualnej. Umożliwi to maszyn wirtualnych na powitania sieci wirtualnej tooconnect toohello domeny dla operacji, takich jak przyłączanie do domeny.

    ![Okno usług domenowych wyświetlające oba aprowizowane adresy IP](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> W zależności od rozmiaru hello dzierżawy usługi Azure AD (na przykład hello liczba użytkowników lub grupy) domeny zarządzanej tooyour synchronizacji zajmie trochę czasu. Ten proces synchronizacji jest wykonywany w tle hello. W przypadku dużych dzierżaw z dziesiątkami tysięcy obiektów może potrwać dzień lub dwa dla wszystkich użytkowników, członkostwa w grupach i poświadczeń toobe zsynchronizowane.
>
>

## <a name="next-step"></a>Następny krok
[Zadanie 4: aktualizowanie ustawień DNS hello hello sieci wirtualnej platformy Azure](active-directory-ds-getting-started-update-dns.md)
