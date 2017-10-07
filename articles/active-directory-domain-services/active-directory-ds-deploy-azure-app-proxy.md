---
title: "Usługi domenowe w usłudze Azure Active Directory: Wdrażanie serwera Proxy aplikacji usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Użyj serwera Proxy aplikacji usługi Azure AD w domenach zarządzanych usług domenowych Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a>Wdrażanie aplikacji serwera Proxy Azure AD w domenie zarządzanej usług domenowych Azure AD
Serwer Proxy aplikacji usługi Azure Active Directory (AD) pomaga obsługuje pracowników zdalnych, publikując lokalnymi toobe aplikacji udostępnianych za pośrednictwem hello internet. Z usług domenowych Azure AD możesz teraz przyrostu i shift starsze aplikacje lokalne tooAzure infrastruktury usługi. Następnie można opublikować te aplikacje przy użyciu hello AD serwera Proxy aplikacji Azure, tooprovide toousers bezpieczny dostęp zdalny w Twojej organizacji.

Jeśli masz toohello nowego serwera Proxy aplikacji usługi Azure AD, Dowiedz się więcej o tej funkcji z poniższego artykułu hello: [jak tooprovide bezpiecznego dostępu zdalnego aplikacje lokalne tooon](../active-directory/active-directory-application-proxy-get-started.md).


## <a name="before-you-begin"></a>Przed rozpoczęciem
zadania hello tooperform wymienione w tym artykule, potrzebne są:

1. Prawidłowy **subskrypcji platformy Azure**.
2. **Katalog usługi Azure AD** -albo synchronizowane z katalogu lokalnego lub w katalogu tylko w chmurze.
3. **Licencji Azure AD podstawowa lub Premium** jest wymagane toouse hello serwera Proxy aplikacji usługi Azure AD.
4. **Usługi domenowe Azure AD** musi być włączona dla katalogu hello Azure AD. Jeśli nie zostało to jeszcze zrobione, należy wykonać wszystkie zadania hello opisane w hello [Przewodnik wprowadzający](active-directory-ds-getting-started.md).

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a>Zadanie 1 - serwer Proxy aplikacji włączania usługi Azure AD dla katalogu usługi Azure AD
Wykonaj następujące kroki tooenable hello Azure serwera Proxy aplikacji usługi AD dla katalogu usługi Azure AD hello.

1. Zaloguj się jako administrator w hello [portalu Azure](http://portal.azure.com).

2. Kliknij przycisk **usługi Azure Active Directory** toobring się hello directory — omówienie. Kliknij przycisk **aplikacje dla przedsiębiorstw**.

    ![Wybierz katalog usługi Azure AD](./media/app-proxy/app-proxy-enable-start.png)
3. Kliknij przycisk **serwera proxy aplikacji**. Jeśli nie masz subskrypcji usługi Azure AD podstawowa lub Azure AD Premium, zobaczysz tooenable opcji korzystania z wersji próbnej. Przełącz **Włączanie serwera Proxy aplikacji?** za**włączyć** i kliknij przycisk **zapisać**.

    ![Włącz serwer Proxy aplikacji](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. toodownload hello łącznik, kliknij przycisk hello **łącznik** przycisku.

    ![Pobierz łącznik](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. Na stronie pobierania hello, zaakceptuj postanowienia licencyjne hello i ochrony prywatności umowy, a następnie kliknij przycisk hello **Pobierz** przycisku.

    ![Potwierdź pobierania](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a>Zadanie 2 - Provision przyłączonych do domeny serwerów toodeploy hello Azure AD serwera Proxy aplikacji łącznika usługi Windows
Wymagane są przyłączone do domeny systemu Windows Server maszyny wirtualne na których można zainstalować hello łącznika serwera Proxy aplikacji usługi Azure AD. W zależności od aplikacji hello publikowaną można wybrać wiele serwerów, na których jest zainstalowany łącznik hello tooprovision. Ta opcja wdrażania zapewnia większą dostępność i pomaga obsługi większych obciążeń uwierzytelniania.

Świadczenie serwery łącznika hello na hello tej samej sieci wirtualnej (lub połączony/połączyć za pomocą sieci wirtualnej), w którym włączono domeny zarządzanej usług domenowych Azure AD. Podobnie, serwery hello hostowania aplikacji hello opublikować za pośrednictwem serwera Proxy aplikacji hello muszą toobe zainstalowane na powitania tej samej sieci wirtualnej platformy Azure.

serwery łącznika tooprovision, wykonaj zadania hello opisane w artykule hello zatytułowany [Dołącz do domeny zarządzanej tooa maszyny wirtualnej systemu Windows](active-directory-ds-admin-guide-join-windows-vm.md).


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a>Zadanie 3 — Instalowanie i rejestrowanie hello łącznika serwera Proxy aplikacji w usłudze Azure AD
Poprzednio udostępnione maszynę wirtualną systemu Windows Server i opcję dołączenia do niej toohello domeny zarządzanej. W tym zadaniu łącznika serwera Proxy aplikacji usługi Azure AD hello zostanie zainstalowany na tej maszynie wirtualnej.

1. Skopiuj hello łącznika instalacji pakietu toohello VM na którym jest instalowany łącznik serwera Proxy aplikacji sieci Web platformy Azure AD hello.

2. Uruchom **AADApplicationProxyConnectorInstaller.exe** hello maszyny wirtualnej. Zaakceptuj postanowienia licencyjne dotyczące oprogramowania hello.

    ![Zaakceptuj postanowienia instalacji](./media/app-proxy/app-proxy-install-connector-terms.png)
3. Podczas instalacji to zostanie wyświetlony monit o tooregister hello łącznika z powitania serwera Proxy aplikacji z katalogu usługi Azure AD.
    * Podaj Twojej **poświadczenia administratora globalnego usługi Azure AD**. Administrator globalny dzierżawy może mieć inne poświadczenia platformy Microsoft Azure niż Twoje.
    * Witaj łącznika hello tooregister używane konto administratora musi należeć toohello tym samym katalogu, w którym włączono usługę serwera Proxy aplikacji hello. Na przykład, jeśli domena dzierżawy hello to contoso.com, Witaj, Administratorze powinna być admin@contoso.com lub dowolny inny alias prawidłowe w tej domenie.
    * Jeśli Konfiguracja zwiększonych zabezpieczeń programu Internet Explorer jest włączona dla serwera hello podczas instalowania łącznika hello, hello ekran rejestracji może zostać zablokowany. tooallow dostęp, wykonaj instrukcje hello w komunikacie o błędzie hello. Upewnij się, że pozycja Konfiguracja zwiększonych zabezpieczeń programu Internet Explorer jest wyłączona.
    * Jeśli rejestracja łącznika nie powiedzie się, zobacz [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md) (Rozwiązywanie problemów z serwerem proxy aplikacji).

    ![Zainstalowanego łącznika](./media/app-proxy/app-proxy-connector-installed.png)
4. tooensure hello łącznik działa prawidłowo, uruchom hello rozwiązywania łącznika serwera Proxy aplikacji Azure AD. Pomyślne raportu powinna zostać wyświetlona po uruchomionych hello narzędzia do rozwiązywania problemów.

    ![Powodzenie narzędzia do rozwiązywania problemów](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. Powinny pojawić się hello nowo zainstalowany łącznik wyświetlane na stronie serwer proxy aplikacji hello w katalogu usługi Azure AD.

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> Możesz wybrać łączniki tooinstall na wielu serwerach tooguarantee wysokiej dostępności do uwierzytelniania w aplikacjach opublikowanych w usłudze powitania serwera Proxy aplikacji usługi Azure AD. Wykonaj hello te same czynności wymienionych powyżej tooinstall hello łącznika na inne domeny zarządzanej tooyour połączonych serwerów.
>
>

## <a name="next-steps"></a>Następne kroki
Ma ustawienie powitania serwera Proxy aplikacji usługi Azure AD i zintegrować ją z domeny zarządzanej usług domenowych Azure AD.

* **Migrowanie maszyn wirtualnych tooAzure aplikacji:** można przyrostu shift aplikacji z lokalnych serwerów tooAzure maszyn wirtualnych tooyour przyłączone do zarządzanej domeny. Pomoże pozbyć się hello infrastruktury kosztów działających serwerów lokalnych.

* **Publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD:** publikowania aplikacji działających na maszynach wirtualnych platformy Azure przy użyciu powitania serwera Proxy aplikacji usługi Azure AD. Aby uzyskać więcej informacji, zobacz [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](../active-directory/application-proxy-publish-azure-portal.md)


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a>Uwaga wdrożenia — aplikacje publikowania IWA (zintegrowane uwierzytelnianie systemu Windows) przy użyciu serwera Proxy aplikacji usługi Azure AD
Włączanie aplikacji tooyour rejestracji jednokrotnej, przy użyciu zintegrowanego uwierzytelniania systemu Windows (IWA) przez udzielanie uprawnień łączniki serwera Proxy aplikacji tooimpersonate użytkowników oraz wysyłanie i odbieranie tokenów w ich imieniu. Skonfiguruj ograniczone delegowanie protokołu kerberos (KCD) dla hello łącznika toogrant hello wymagane uprawnienia tooaccess zasobów na powitania domeny zarządzanej. Aby zwiększyć bezpieczeństwo, użyj mechanizmu KCD oparte na zasobach hello w domenach zarządzanych.


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a>Włącz oparte na zasobach ograniczonego delegowania protokołu kerberos dla łącznika serwera Proxy aplikacji hello Azure AD
łącznika serwera Proxy aplikacji Azure Hello powinien być skonfigurowany ograniczonego delegowania protokołu kerberos (KCD), dlatego może on personifikować użytkowników dla domeny zarządzanej hello. W domenie zarządzanej usług domenowych Azure AD nie masz uprawnienia administratora domeny. W związku z tym **tradycyjnych KCD poziomie konta nie można skonfigurować w domenie zarządzanej**.

Użyj KCD oparte na zasobach, zgodnie z opisem w tym [artykułu](active-directory-ds-enable-kcd.md).

> [!NOTE]
> Należy toobe członkiem grupy "Administratorzy kontrolera domeny usługi AAD" hello, tooadminister hello zarządzane domeny przy użyciu poleceń cmdlet programu PowerShell usługi AD.
>
>

Za pomocą hello programu PowerShell Get-ADComputer polecenia cmdlet tooretrieve hello ustawień dla hello komputera, na które powitania serwera Proxy aplikacji usługi Azure AD connector jest zainstalowany.
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

Później Użyj tooset polecenia cmdlet Set-ADComputer hello zapasowych oparte na zasobach KCD hello zasobów serwera.
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

Jeśli wiele łączników serwera Proxy aplikacji zostały wdrożone na domeny zarządzanej, należy tooconfigure oparte na zasobach KCD dla każdego wystąpienia łącznika.


## <a name="related-content"></a>Powiązana zawartość
* [Usługi domenowe AD Azure - Przewodnik wprowadzający](active-directory-ds-getting-started.md)
* [Skonfiguruj ograniczone delegowanie protokołu Kerberos w domenie zarządzanej](active-directory-ds-enable-kcd.md)
* [Omówienie delegowania ograniczonego protokołu Kerberos](https://technet.microsoft.com/library/jj553400.aspx)
