---
title: "Rozpoczynanie pracy aaaAzure serwer Proxy aplikacji usługi AD - zainstalować łącznik | Dokumentacja firmy Microsoft"
description: "Włącz serwer Proxy aplikacji w portalu Azure hello i zainstaluj hello łączniki dla zwrotnego serwera proxy hello."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ea79ffa92fa223584be04f49019fd31a0bfd8358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-proxy-and-install-hello-connector"></a>Rozpoczynanie pracy z serwera Proxy aplikacji i zainstalować łącznik hello
W tym artykule przedstawiono hello kroki tooenable Microsoft Azure serwera Proxy aplikacji usługi AD dla katalogu w chmurze w usłudze Azure AD.

Jeśli nie masz jeszcze pamiętać hello korzyści zabezpieczeń i wydajności serwera Proxy aplikacji oferuje organizacji tooyour, Dowiedz się więcej o [jak tooprovide bezpiecznego dostępu zdalnego aplikacje lokalne tooon](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Wymagania wstępne serwera proxy aplikacji
Aby można było włączyć i używać serwera Proxy aplikacji usługi, należy toohave:

* [Subskrypcja usługi Microsoft Azure AD w warstwie Podstawowa lub Premium](active-directory-editions.md) i katalog usługi Azure AD, dla którego jesteś administratorem globalnym.
* Serwer z systemem Windows Server 2012 R2 lub 2016, na którym jest instalowany hello łącznika serwera Proxy aplikacji. Serwer Hello musi toobe stanie tooconnect toohello serwera Proxy aplikacji usługi w chmurze hello i hello aplikacji, które są publikowane lokalnymi.
  * Dla tooyour rejestracji jednokrotnej aplikacji opublikowanych przy użyciu ograniczone delegowanie protokołu Kerberos tej maszyny powinny można przyłączonych do domeny w domenie hello tego samego AD jako aplikacji hello, które są publikowane. Aby uzyskać informacje, zobacz [KCD dla logowania jednokrotnego przy użyciu serwera Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md).

Jeśli Twoja organizacja korzysta z serwera proxy toohello tooconnect serwerów internetowych, przeczytaj [pracy przy użyciu istniejących lokalnych serwerów proxy](application-proxy-working-with-proxy-servers.md) szczegóły na jak tooconfigure je, aby uzyskać informacje o pracy z serwera Proxy aplikacji.

## <a name="open-your-ports"></a>Otwieranie portów sieci

tooprepare środowiska dla serwera Proxy aplikacji usługi Azure AD, należy najpierw centrów danych tooAzure komunikacji tooenable. Jeśli w ścieżce hello jest zapora, upewnij się, czy jest otwarty, powitalne tego łącznika można wprowadzać HTTPS (TCP) żąda toohello serwera Proxy aplikacji.

1. Otwórz hello następujących portów za**wychodzących** ruchu:

   | Numer portu | Jak jest używany |
   | --- | --- |
   | 80 | Pobieranie odwołania certyfikatu list podczas sprawdzania poprawności certyfikatu SSL hello |
   | 443 | Cała komunikacja wychodząca z hello usługi Serwer Proxy aplikacji |

   Jeśli Zapora wymusza ruch zgodnie z toooriginating użytkowników, należy otworzyć te porty dla ruchu z usług systemu Windows, które działają jako usługa sieciowa.

   > [!IMPORTANT]
   > Tabela Hello odzwierciedla hello wymagania dotyczące portów dla wersji łącznika 1.5.132.0 i nowszych. Jeśli nadal masz starszą wersję łącznika, należy również hello tooenable następujące porty w too80 dodanie i 443:5671, 8080, 9090 9091, 9350, 9352, 10100 — 10120.
   >
   >Informacji o aktualizowaniu łączniki toohello najnowszej wersji, zobacz [łączniki serwera Proxy aplikacji usługi AD zrozumieć Azure](application-proxy-understand-connectors.md#automatic-updates).

2. Jeśli zapora lub serwer proxy zezwala na listę dozwolonych podobnej DNS, możesz toomsappproxy.net połączeń dozwolonych i servicebus.windows.net. Jeśli nie potrzebujesz toohello dostępu tooallow [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653), które są aktualizowane co tydzień.

3. Firma Microsoft korzysta z czterech certyfikaty tooverify adresów. Zezwalaj na dostęp toohello następujące adresy URL, jeśli nie zostało to jeszcze zrobione dla innych produktów:
   * mscrl.microsoft.com:80
   * CRL.microsoft.com:80
   * OCSP.msocsp.com:80
   * www.microsoft.com:80

4. Łącznik programu potrzebuje toologin.windows.net dostępu i login.microsoftonline.net hello procesu rejestracji.

5. Użyj hello [Azure AD aplikacji serwera Proxy łącznika porty testu narzędzie](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify, że Twoje łącznika może nawiązać połączenie powitania serwera Proxy aplikacji usługi. Co najmniej upewnij się, że hello środkowe stany USA regionu i tooyou najbliższy region hello jest wszystkich zaznaczeń zielony. Ponadto więcej zaznaczeń zielony oznacza większą elastyczność.

## <a name="install-and-register-a-connector"></a>Instalowanie i rejestrowanie łącznika
1. Zaloguj się jako administrator w hello [portalu Azure](https://portal.azure.com/).
2. Bieżący katalog jest wyświetlany w obszarze nazwy użytkownika w prawym górnym rogu hello. Jeśli potrzebujesz toochange katalogów, wybierz tę ikonę.
3. Przejdź za**usługi Azure Active Directory** > **serwera Proxy aplikacji**.

   ![Przejdź tooApplication serwera Proxy](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. Wybierz **Pobierz łącznik**.

   ![Pobierz łącznik](./media/active-directory-application-proxy-enable/download_connector.png)

5. Uruchom **AADApplicationProxyConnectorInstaller.exe** na powitania serwerze przygotowanym zgodnie z toohello wymagania wstępne.
6. Wykonaj instrukcje hello hello tooinstall kreatora. Podczas instalacji to zostanie wyświetlony monit o tooregister hello łącznika z powitania serwera Proxy aplikacji dzierżawy usługi Azure AD.

   * Podaj poświadczenia administratora globalnego usługi Azure AD. Administrator globalny dzierżawy może mieć inne poświadczenia platformy Microsoft Azure niż Twoje.
   * Upewnij się, Witaj, Administratorze kto rejestrów łącznika hello jest hello tym samym katalogu, w którym włączono hello serwera Proxy aplikacji usługi. Na przykład, jeśli domena dzierżawy hello to contoso.com, Witaj, Administratorze powinna być admin@contoso.com lub dowolny inny alias w tej domenie.
   * Jeśli **Konfiguracja zwiększonych zabezpieczeń** ustawiono zbyt**na** na serwerze hello, którym jest instalowany łącznik hello, może nie być wyświetlana hello ekranie rejestracji. tooget dostęp, wykonaj instrukcje hello w komunikacie o błędzie hello. Upewnij się, że pozycja Konfiguracja zwiększonych zabezpieczeń programu Internet Explorer jest wyłączona.

Aby zapewnić wysoką dostępność, należy wdrożyć co najmniej dwa łączniki. Każdy łącznik musi zostać zarejestrowany oddzielnie.

## <a name="test-that-hello-connector-installed-correctly"></a>Testowanie tego łącznika hello zainstalowane prawidłowo

Można potwierdzić, czy nowy łącznik poprawnie zainstalowany poprzez sprawdzenie jego albo hello portalu Azure lub na serwerze. 

W hello portalu Azure, zaloguj się tooyour dzierżawy i przejdź zbyt**usługi Azure Active Directory** > **serwera Proxy aplikacji**. Wszystkie łączniki i grup łącznika są wyświetlane na tej stronie. Wybierz toosee łącznika jego szczegóły, lub przenieś go do grupy różnych łącznika. 

Na serwerze Sprawdź hello listę aktywnych usług dla łącznika hello i hello aktualizator łącznika. Witaj dwie usługi należy natychmiast uruchomione, ale jeśli nie, włącz je: 

   * **Łącznik serwera proxy aplikacji usługi Microsoft AAD** umożliwia łączność

   * **Aktualizator łącznika serwera Proxy aplikacji usługi AAD Microsoft** jest automatyczna usługa aktualizacji. Aktualizator Hello sprawdza dostępność nowych wersji łącznika hello i aktualizacje hello łącznika zgodnie z potrzebami.

   ![Usługi łącznika serwera proxy aplikacji — zrzut ekranu](./media/active-directory-application-proxy-enable/app_proxy_services.png)

Aby uzyskać informacji na temat łączników i jak te komputery pozostaną się toodate, zobacz [łączniki serwera Proxy aplikacji usługi AD zrozumieć Azure](application-proxy-understand-connectors.md).


## <a name="next-steps"></a>Następne kroki
Teraz można przystąpić zbyt[publikowania aplikacji za pomocą serwera Proxy aplikacji](application-proxy-publish-azure-portal.md).

Jeśli masz aplikacje, które znajdują się w różnych sieciach lub innej lokalizacji za pomocą łącznika grup tooorganize hello różnych łączniki do jednostek logicznych. Dowiedz się więcej o [pracy z łącznikami serwera proxy aplikacji](active-directory-application-proxy-connectors-azure-portal.md).
