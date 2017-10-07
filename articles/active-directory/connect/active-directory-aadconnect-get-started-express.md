---
title: "Azure AD Connect: rozpoczynanie pracy przy użyciu ustawień ekspresowych | Microsoft Docs"
description: "Dowiedz się, jak toodownload, zainstalować i uruchomić hello Kreatora instalacji programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>Rozpoczynanie pracy z programem Azure AD Connect przy użyciu ustawień ekspresowych
Użyj **ustawień ekspresowych** programu Azure AD Connect, jeśli używasz topologii z jednym lasem oraz [synchronizacji haseł](active-directory-aadconnectsync-implement-password-synchronization.md) na potrzeby uwierzytelniania. **Ustawienia ekspresowe** jest opcja domyślna hello i jest używany w scenariuszu hello zwykle wdrażana. Można to tylko kilka kliknięć nieobecności tooextend chmury toohello katalogu lokalnego.

Przed rozpoczęciem instalowania Azure AD Connect, upewnij się, zbyt[Pobierz Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) i pełne hello wstępnymi opisane w temacie [Azure AD Connect: sprzęt i wymagania wstępne](active-directory-aadconnect-prerequisites.md).

Jeśli ustawienia ekspresowe nie są odpowiednie do Twojej topologii, zobacz [dokumentację pokrewną](#related-documentation), aby zapoznać się z innymi scenariuszami.

## <a name="express-installation-of-azure-ad-connect"></a>Ekspresowa instalacja programu Azure AD Connect
Możesz zobaczyć te czynności w praktyce hello [wideo](#videos) sekcji.

1. Zaloguj się jako administrator lokalny serwera toohello, które mają zostać tooinstall Azure AD Connect na. Ten krok należy wykonać na powitania serwera ma toobe hello synchronizacji serwera.
2. Kliknij dwukrotnie tooand Przejdź **AzureADConnect.msi**.
3. Na ekranie powitalnym hello, wybierz hello pole wynoszącego toohello umowy licencyjnej, a następnie kliknij przycisk **Kontynuuj**.  
4. Na ekranie Ustawienia ekspresowe powitania kliknij **Użyj ustawień ekspresowych**.  
   ![Witamy tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)
5. Na ekranie tooAzure AD Connect hello wprowadź hello użytkownika i hasło administratora globalnego usługi Azure AD. Kliknij przycisk **Dalej**.  
   ![Połącz tooAzure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) jeżeli wystąpi błąd lub problem z łącznością, zobacz [Rozwiązywanie problemów z łącznością](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Na ekranie powitania połączenia tooAD DS wprowadź hello użytkownika i hasło dla konta administratora przedsiębiorstwa. Możesz wprowadzić hello domeny w formacie NetBios lub FQDN, czyli FABRIKAM\administrator lub fabrikam.com\administrator. Kliknij przycisk **Dalej**.  
   ![Połącz tooAD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. Witaj [ **Konfiguracja logowania w usłudze Azure AD** ](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) strona zawiera tylko, jeśli nie zostaną wykonane [weryfikowania domen](../active-directory-add-domain.md) w hello [wymagania wstępne](active-directory-aadconnect-prerequisites.md).
   ![Niezweryfikowane domeny](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   Jeśli zobaczysz tę stronę, sprawdź wszystkie domeny z oznaczeniem **Nie dodano** lub **Nie zweryfikowano**. Upewnij się, że używane domeny zostały zweryfikowane w usłudze Azure AD. Po zweryfikowaniu domen, kliknij symbol Odśwież hello.
8. Na ekranie powitania tooconfigure gotowe kliknij **zainstalować**.
   * Opcjonalnie na stronie gotowe tooconfigure hello, możesz usunąć zaznaczenie hello **Uruchom proces synchronizacji hello zaraz po zakończeniu konfiguracji** wyboru. Usuń zaznaczenie tego pola wyboru Jeśli chcesz toodo dodatkowej konfiguracji, takich jak [filtrowania](active-directory-aadconnectsync-configure-filtering.md). Jeśli możesz wyłączyć tę opcję, hello Kreator skonfiguruje funkcję synchronizacji, ale pozostawia hello harmonogramu. Nie jest uruchamiane, dopóki nie zostanie włączona ręcznie przez [ponowne uruchomienie Kreatora instalacji hello](active-directory-aadconnectsync-installation-wizard.md).
   * Jeśli korzystasz z programu Exchange w lokalnej usługi Active Directory, a następnie istnieje również opcja tooenable [ **wdrożenia hybrydowego programu Exchange**](https://technet.microsoft.com/library/jj200581.aspx). Włącz tę opcję, jeśli planujesz toohave skrzynki pocztowe programu Exchange zarówno w chmurze hello lokalnie na powitania sam czas.
     ![Gotowe tooconfigure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. Po ukończeniu instalacji powitania kliknij **zakończenia**.
10. Po zakończeniu instalacji hello Wyrejestruj się i zaloguj się ponownie przed użyciem narzędzia Synchronization Service Manager lub Synchronization Rule Editor.

## <a name="videos"></a>Filmy wideo
Aby obejrzeć wideo na powitania instalacji ekspresowej zobacz:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a>Następne kroki
Teraz, gdy masz Azure AD Connect można [zweryfikować hello instalację i przypisywanie licencji](active-directory-aadconnect-whats-next.md).

Dowiedz się więcej o tych funkcjach, włączonych instalacji hello: [automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md), [Zapobieganie przypadkowemu usuwaniu](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), i [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Dowiedz się więcej na te popularne tematy: [harmonogram i sposób synchronizacji tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

## <a name="related-documentation"></a>Dokumentacja pokrewna
| Temat |
| --- | --- |
| Omówienie programu Azure AD Connect |
| Instalowanie przy użyciu ustawień dostosowanych |
| Uaktualnianie przy użyciu narzędzia DirSync |
| Konta używane do instalacji |

