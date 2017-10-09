---
title: "Azure AD Connect: Certyfikat SSL hello aktualizacji dla farmę serwerów usługi Active Directory Federation Services (AD FS) | Dokumentacja firmy Microsoft"
description: "Ten dokument szczegóły hello kroki tooupdate hello certyfikat SSL farmy usług AD FS przy użyciu usługi Azure AD Connect."
services: active-directory
keywords: "programu Azure ad connect, aktualizacji ssl usług AD FS, aktualizacja certyfikatu usług AD FS, zmienianie certyfikatu usług AD FS, nowego certyfikatu usług AD FS, certyfikat usług AD FS aktualizacji usług AD FS certyfikat ssl, aktualizacja AD FS certyfikat ssl, skonfigurować certyfikat ssl usług AD FS, usługi AD FS, ssl, certyfikatu, certyfikat komunikacji usługi AD FS, federation aktualizacji, konfigurowanie Federacji, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a>Aktualizuj hello certyfikat protokołu SSL dla farmę serwerów usługi Active Directory Federation Services (AD FS)

## <a name="overview"></a>Omówienie
W tym artykule opisano, jak można użyć certyfikatu SSL hello tooupdate Azure AD Connect dla farmę serwerów usługi Active Directory Federation Services (AD FS). Można użyć certyfikatu SSL hello aktualizacji tooeasily hello Azure AD Connect narzędzia hello AD FS farmy programu, nawet jeśli wybrano metodę logowania dla użytkownika hello nie usług AD FS.

Można wykonywać hello całej operacji aktualizowania certyfikat SSL dla hello AD FS farmy we wszystkich federacyjnych i serwerach Proxy aplikacji sieci Web (WAP) w trzy proste kroki:

![Trzy kroki](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
>toolearn więcej informacji na temat certyfikatów, które są używane przez usługi AD FS, zobacz [Opis certyfikatów używane przez usługi AD FS](https://technet.microsoft.com/library/cc730660.aspx).

## <a name="prerequisites"></a>Wymagania wstępne

* **Farmy usług AD FS**: Upewnij się, że farmę usług AD FS jest systemem Windows Server 2012 R2 lub nowszym.
* **Azure AD Connect**: Upewnij się, że hello wersji programu Azure AD Connect jest 1.1.443.0 lub nowszym. Użyjesz zadań hello **aktualizacja AD FS certyfikat**.

![Zadanie aktualizacji protokołu SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a>Krok 1: Podaj informacje farmy usług AD FS

Azure AD Connect podejmuje automatycznie przez tooobtain informacji na temat hello AD FS farmy:
1. Kwerenda hello farmy informacji z usług AD FS (Windows Server 2016 lub nowszy).
2. Odwołuje się do hello informacje z poprzedniego przebiegi, które są przechowywane lokalnie z programem Azure AD Connect.

Można zmodyfikować hello listy serwerów, które są wyświetlane przez dodanie lub usunięcie hello serwerów tooreflect hello bieżącej konfiguracji hello AD FS farmy. Jak podano informacje o serwerze hello, Azure AD Connect Wyświetla hello łączności i bieżący stan certyfikatu SSL.

![Informacje o serwerze programu AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

Jeśli lista hello zawiera serwer, który nie jest już częścią hello AD FS farmy, kliknij przycisk **Usuń** toodelete powitania serwera z hello listę serwerów w farmie serwerów usług AD FS.

![W trybie offline serwer na liście](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> Usuwanie serwera z listy hello serwerów usług AD FS farmy w programie Azure AD Connect jest operacją lokalnych i aktualizacje hello informacje dotyczące hello farmy usług AD FS, zawierającą lokalnie Azure AD Connect. Azure AD Connect nie modyfikuje hello konfiguracji usług AD FS tooreflect hello zmian.    

## <a name="step-2-provide-a-new-ssl-certificate"></a>Krok 2: Podaj nowy certyfikat SSL

Po potwierdzeniu hello informacji na temat serwerów w kolektywie serwerów usług AD FS, Azure AD Connect monituje o podanie hello nowy certyfikat SSL. Podaj chroniony hasłem PFX toocontinue hello instalacji certyfikatu.

![Certyfikat SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

Po podaniu certyfikatu hello Azure AD Connect przechodzi przez szereg wymagań wstępnych. Sprawdź, czy hello tooensure certyfikatu, który hello certyfikat jest poprawny dla farmy usług AD FS hello:

-   Witaj podmiotu nazwy/alternatywny nazwa podmiotu certyfikatu hello jest hello takie same jak nazwa usługi federacyjnej hello albo jest certyfikat wieloznaczny.
-   Witaj certyfikat jest ważny przez dłużej niż 30 dni.
-   łańcuch zaufania certyfikatów Hello jest prawidłowy.
-   Witaj certyfikat jest chroniony hasłem.

## <a name="step-3-select-servers-for-hello-update"></a>Krok 3: Wybierz serwery hello aktualizacji

W następnym kroku hello wybierz serwery hello, wymagające certyfikatów SSL hello toohave zaktualizowane. Nie można wybrać serwery, które są w trybie offline hello aktualizacji.

![Wybierz serwery tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

Po zakończeniu konfiguracji hello Azure AD Connect wyświetla wiadomość hello wskazuje stan hello hello aktualizacji i udostępnia opcję tooverify hello usług AD FS logowania.

![Kończenie konfiguracji](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a>Często zadawane pytania

* **Jakie powinny być hello nazwa podmiotu certyfikatu hello uzyskać nowy certyfikat SSL usług AD FS hello?**

    Azure AD Connect sprawdza, czy nazwa podmiotu nazwy/alternatywny podmiotu hello hello certyfikatu zawiera nazwy usługi federacyjnej hello. Na przykład jeśli nazwa usługi federacyjnej jest fs.contoso.com, nazwa podmiotu nazwy/alternatywny podmiotu hello musi być fs.contoso.com.  Certyfikatów z symbolami wieloznacznymi również są akceptowane.

* **Dlaczego pojawia się pytanie o poświadczenia ponownie na stronie serwer proxy hello?**

    Jeśli poświadczenia hello, które zapewniają połączenia tooAD FS serwerów również nie ma serwerów proxy hello toomanage uprawnień hello, Azure AD Connect zapyta o poświadczenia, które mają uprawnienia administracyjne na powitania serwerów proxy.

* **Serwer Hello jest wyświetlany w trybie offline. Co zrobić?**

    Azure AD Connect nie może wykonać żadnej operacji, jeśli serwer hello jest w trybie offline. Jeżeli serwer hello jest częścią hello farmy usług AD FS, sprawdź hello łączności toohello serwera. Po hello problem został rozwiązany, naciśnij klawisz hello odświeżania ikona tooupdate hello stan hello kreatora. Jeśli serwer hello jest częścią programu hello farmy wcześniej, ale teraz już nie istnieje, kliknij pozycję **Usuń** toodelete przechowuje go z listy hello serwerów, które programu Azure AD Connect. Usuwanie serwera hello z listy hello w programie Azure AD Connect nie powoduje zmian hello konfiguracji usług AD FS, sama. Jeśli korzystasz z usług AD FS w systemie Windows Server 2016 lub nowszym powitania serwera pozostaje w ustawieniach konfiguracji hello i pojawi się ponownie hello następnym hello zadanie zostanie uruchomione.

* **Można aktualizować podzbiór serwerów w kolektywie serwerów z hello nowy certyfikat SSL?**

    Tak. Będzie można uruchamiać zadania hello **certyfikat SSL aktualizacji** ponownie hello tooupdate pozostałych serwerów. Na powitania **wybierz serwery protokołu SSL certyfikatów aktualizacji** strony, można sortować hello listę serwerów na **datę wygaśnięcia SSL** tooeasily dostępu hello serwerów, które nie są jeszcze zaktualizowana.

* **Po usunięciu serwera hello w poprzednim hello uruchomiony, ale jego jest nadal wyświetlane jako w trybie offline i listy na stronie serwery FS hello AD. Dlaczego jest hello nadal istnieje serwer w trybie offline, nawet po usunięciu go?**

    Usuwanie serwera hello z listy hello w programie Azure AD Connect nie powoduje jego usunięcia w hello konfiguracji usług AD FS. Azure AD Connect odwołuje się do usług AD FS (Windows Server 2016 lub nowszego) żadnych informacji o hello farmy. Jeśli serwer hello jest nadal znajdują się na powitania konfiguracji usług AD FS, będzie wyświetlane w hello listy.  

## <a name="next-steps"></a>Następne kroki

- [Program Azure AD Connect a federacja](active-directory-aadconnectfed-whatis.md)
- [Dostosowywanie z programem Azure AD Connect i zarządzania w usłudze Active Directory Federation Services](active-directory-aadconnect-federation-management.md)
