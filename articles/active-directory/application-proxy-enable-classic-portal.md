---
title: aaaEnable AD serwera Proxy aplikacji Azure w portalu klasycznym hello | Dokumentacja firmy Microsoft
description: "Włącz serwer Proxy aplikacji w hello klasycznego portalu Azure, a następnie zainstaluj hello łączniki dla zwrotnego serwera proxy hello."
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
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Włącz serwer Proxy aplikacji w portalu klasycznym hello i pobierania łączników
W tym artykule przedstawiono hello kroki tooenable Microsoft Azure serwera Proxy aplikacji usługi AD dla katalogu w chmurze w usłudze Azure AD.

Jeśli znasz co serwer Proxy aplikacji można to robić, Dowiedz się więcej o [jak tooprovide bezpiecznego dostępu zdalnego aplikacje lokalne tooon](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Wymagania wstępne serwera proxy aplikacji
Aby można było włączyć i używać serwera Proxy aplikacji usługi, należy toohave:

* [Subskrypcja usługi Microsoft Azure AD w warstwie Podstawowa lub Premium](active-directory-editions.md) i katalog usługi Azure AD, dla którego jesteś administratorem globalnym.
* Serwer z systemem Windows Server 2012 R2 lub 2016, na którym jest instalowany hello łącznika serwera Proxy aplikacji. Witaj serwer wysyła żądania toohello serwera Proxy aplikacji usługi w chmurze hello i musi HTTP lub HTTPS połączenia toohello aplikacji, które są publikowane.
  * Dla tooyour rejestracji jednokrotnej opublikowane aplikacje, tej maszyny powinny być przyłączonych do domeny w domenie hello tego samego AD jako aplikacji hello, które są publikowane. Aby uzyskać informacje, zobacz [rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)
* Jeśli Twoja organizacja korzysta z serwera proxy toohello tooconnect serwerów internetowych, przeczytaj [pracy przy użyciu istniejących lokalnych serwerów proxy](application-proxy-working-with-proxy-servers.md) szczegółowe informacje na temat tooconfigure je.

## <a name="open-your-ports"></a>Otwieranie portów sieci

tooprepare środowiska dla serwera Proxy aplikacji usługi Azure AD, należy najpierw centrów danych tooAzure komunikacji tooenable. Jeśli w ścieżce hello jest zapora, upewnij się, czy jest otwarty, powitalne tego łącznika można wprowadzać HTTPS (TCP) żąda toohello serwera Proxy aplikacji.

1. Otwórz hello następujących portów za**wychodzących** ruchu:

   | Numer portu | Jak jest używany |
   | --- | --- |
   | 80 | Pobieranie odwołania certyfikatu list podczas sprawdzania poprawności certyfikatu SSL hello |
   | 443 | Cała komunikacja wychodząca z hello usługi Serwer Proxy aplikacji |

   Jeśli Zapora wymusza ruch zgodnie z toooriginating użytkowników, należy otworzyć te porty dla ruchu przychodzącego z usług systemu Windows uruchomiona jako usługa sieciowa.

   > [!IMPORTANT]
   > Tabela Hello odzwierciedla hello wymagania dotyczące portów dla wersji łącznika 1.5.132.0 i nowszych. Jeśli nadal masz starszą wersję łącznika, należy również hello tooenable następujące porty: 5671, 8080 9090, 9091, 9350, 9352 i 10100 — 10120.
   >
   >Informacji o aktualizowaniu łączniki toohello najnowszej wersji, zobacz [łączniki serwera Proxy aplikacji usługi AD zrozumieć Azure](application-proxy-understand-connectors.md#automatic-updates).

2. Jeśli zapora lub serwer proxy zezwala na listę dozwolonych podobnej DNS, możesz toomsappproxy.net połączeń dozwolonych i servicebus.windows.net. Jeśli nie potrzebujesz toohello dostępu tooallow [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653), które są aktualizowane co tydzień.

3. Użyj hello [Azure AD aplikacji serwera Proxy łącznika porty testu narzędzie](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify, że Twoje łącznika może nawiązać połączenie powitania serwera Proxy aplikacji usługi. Co najmniej upewnij się, że hello środkowe stany USA regionu i tooyou najbliższy region hello jest wszystkich zaznaczeń zielony. Ponadto więcej zaznaczeń zielony oznacza większą elastyczność.

## <a name="enable-application-proxy-in-azure-ad"></a>Włącz serwer Proxy aplikacji w usłudze Azure AD
1. Zaloguj się jako administrator w hello [klasycznego portalu Azure](https://manage.windowsazure.com/).
2. Przejdź tooActive katalog i wybierz katalog hello, w której ma zostać tooenable serwera Proxy aplikacji.

    ![Active Directory — ikona](./media/active-directory-application-proxy-enable/ad_icon.png)
3. Wybierz **Konfiguruj** na stronie katalogu hello i przewiń w dół za**serwera Proxy aplikacji**.
4. Przełącz **Włącz usługi serwera Proxy aplikacji dla tego katalogu** za**włączone**.

    ![Włączanie serwer proxy aplikacji](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. Wybierz polecenie **Pobierz teraz**. Witaj **Azure AD aplikacji pobieranie łącznika serwera Proxy** otwiera. Przeczytaj i zaakceptuj postanowienia licencyjne hello i kliknij przycisk **Pobierz** toosave hello pliku Instalatora Windows (.exe) hello łącznika.

## <a name="install-and-register-hello-connector"></a>Zainstaluj i zarejestruj hello łącznika
1. Uruchom **AADApplicationProxyConnectorInstaller.exe** na powitania serwerze przygotowanym zgodnie z toohello wymagania wstępne.
2. Wykonaj instrukcje hello hello tooinstall kreatora.
3. Podczas instalacji to zostanie wyświetlony monit o tooregister hello łącznika z powitania serwera Proxy aplikacji dzierżawy usługi Azure AD.

   * Podaj poświadczenia administratora globalnego usługi Azure AD. Administrator globalny dzierżawy może mieć inne poświadczenia platformy Microsoft Azure niż Twoje.
   * Upewnij się, Witaj, Administratorze kto rejestrów łącznika hello jest hello tym samym katalogu, w którym włączono hello serwera Proxy aplikacji usługi. Na przykład, jeśli domena dzierżawy hello to contoso.com, Witaj, Administratorze powinna być admin@contoso.com lub dowolny inny alias w tej domenie.
   * Jeśli **Konfiguracja zwiększonych zabezpieczeń** ustawiono zbyt**na** na serwerze hello hello ekran rejestracji może zostać zablokowany. tooallow dostęp, wykonaj instrukcje hello w komunikacie o błędzie hello. Upewnij się, że pozycja Konfiguracja zwiększonych zabezpieczeń programu Internet Explorer jest wyłączona.
   * Jeśli rejestracja łącznika nie powiedzie się, zobacz [Troubleshoot Application Proxy](active-directory-application-proxy-troubleshoot.md) (Rozwiązywanie problemów z serwerem proxy aplikacji).  
4. Po ukończeniu instalacji Witaj dwie nowe usługi są dodawane tooyour serwera:

   * **Łącznik serwera proxy aplikacji usługi Microsoft AAD** umożliwia łączność

     * **Aktualizator łącznika serwera Proxy aplikacji usługi AAD Microsoft** jest automatyczna usługa aktualizacji. Okresowo sprawdza dostępność nowych wersji łącznika hello i aktualizuje hello łącznika, zgodnie z potrzebami.

     ![Usługi łącznika serwera proxy aplikacji — zrzut ekranu](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. Kliknij przycisk **Zakończ** w oknie instalacji hello.

Aby uzyskać informacje dotyczące łączników, zobacz [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md) (Objaśnienie łączników serwera proxy aplikacji usługi Azure AD).

Aby zapewnić wysoką dostępność, należy wdrożyć co najmniej dwa łączniki. toodeploy więcej łączników, powtórz kroki 2 i 3. Każdy łącznik musi zostać zarejestrowany oddzielnie.

Witaj toouninstall łącznik, odinstaluj zarówno hello usługi łącznika i Updater hello. Uruchom ponownie komputer toofully Usuń hello usługi.

## <a name="next-steps"></a>Następne kroki
Teraz można przystąpić zbyt[publikowania aplikacji za pomocą serwera Proxy aplikacji](active-directory-application-proxy-publish.md).

Jeśli masz aplikacje, które znajdują się w różnych sieciach lub różnych lokalizacjach, można użyć łącznika grup tooorganize hello różnych łączniki do jednostek logicznych. Dowiedz się więcej o [pracy z łącznikami serwera proxy aplikacji](active-directory-application-proxy-connectors.md).
