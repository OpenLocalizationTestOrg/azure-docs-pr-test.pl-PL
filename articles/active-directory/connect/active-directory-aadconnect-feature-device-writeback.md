---
title: "Azure AD Connect: Włączanie zapisywania zwrotnego urządzeń | Dokumentacja firmy Microsoft"
description: "Ten dokument szczegóły, jak tooenable zapisu zwrotnego urządzeń za pomocą usługi Azure AD Connect"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a>Azure AD Connect: Włączanie zapisywania zwrotnego urządzeń
> [!NOTE]
> Subskrypcja tooAzure AD — wersja Premium jest wymagana dla zapisu zwrotnego urządzeń.
> 
> 

powitania po dokumentacji zawiera informacje dotyczące sposobu funkcji zapisywania zwrotnego urządzeń hello tooenable w programie Azure AD Connect. Zapisywanie zwrotne urządzeń jest używany w hello następujące scenariusze:

* Włącz dostęp warunkowy oparte na tooADFS urządzeń (2012 R2 lub nowszej) chronione aplikacje (jednostek uzależnionych).

To dodatkowe bezpieczeństwo i gwarantują, że dostęp tooapplications uzyskuje tylko tootrusted urządzenia. Aby uzyskać więcej informacji dotyczących dostępu warunkowego, zobacz [zarządzania ryzykiem przy użyciu dostępu warunkowego](../active-directory-conditional-access.md) i [Konfigurowanie lokalnego dostępu warunkowego przy użyciu rejestracji urządzeń usługi Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md).

> [!IMPORTANT]
> <li>Urządzenia musi znajdować się w hello sam lasu jako hello użytkowników. Ponieważ urządzenia muszą być zapisane ponownie tooa pojedynczego lasu, ta funkcja nie obsługuje obecnie wdrożenia z wieloma lasami użytkownika.</li>
> <li>Obiekt konfiguracji rejestracji tylko jedno urządzenie można dodać toohello lokalnej usługi Active Directory lasu. Ta funkcja nie jest zgodne z topologią gdzie hello lokalna Usługa Active Directory jest katalogów synchronizowane toomultiple usługi Azure AD.</li>> 

## <a name="part-1-install-azure-ad-connect"></a>Część 1: Instalowanie programu Azure AD Connect
1. Zainstaluj program Azure AD Connect przy użyciu niestandardowych albo ustawienia ekspresowe. Firma Microsoft zaleca toostart z wszystkich użytkowników i grup pomyślnie zsynchronizowano przed włączeniem zapisu zwrotnego urządzeń.

## <a name="part-2-prepare-active-directory"></a>Część 2: Przygotowanie usługi Active Directory
Użyj powitania po tooprepare kroki dotyczące korzystania z funkcji zapisywania zwrotnego urządzeń.

1. Z maszyny hello zainstalowanym Azure AD Connect Uruchom program PowerShell w trybie podniesionych uprawnień.
2. Jeśli hello modułu środowiska PowerShell usługi Active Directory nie jest zainstalowany, zainstaluj go za pomocą następującego polecenia hello:
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. Jeśli nie zainstalowano modułu programu PowerShell usługi Azure Active Directory hello, następnie Pobierz i zainstaluj go z [Azure Active Directory modułu dla środowiska Windows PowerShell (wersja 64-bitowa)](http://go.microsoft.com/fwlink/p/?linkid=236297). Ten składnik ma zależność na powitania Asystenta logowania, która jest instalowana z programem Azure AD Connect.
4. Przy użyciu poświadczeń administratora przedsiębiorstwa uruchom następujące polecenia hello, a następnie zamknij programu PowerShell.
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

Wymagane są poświadczenia administratora przedsiębiorstwa, ponieważ przestrzeń nazw konfiguracji toohello zmiany są potrzebne. Administrator domeny nie ma wystarczających uprawnień.

![Programu PowerShell dla Włączanie zapisywania zwrotnego urządzeń](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

Opis:

* Jeśli już istnieje, tworzy i konfiguruje nowe kontenery i obiekty CN = Device Registration Configuration, CN = Services, CN = Configuration, [nazwa wyróżniająca lasu].
* Jeśli już istnieje, tworzy i konfiguruje nowe kontenery i obiekty CN = RegisteredDevices, [nazwa wyróżniająca domeny]. Obiekty urządzeń zostaną utworzone w tym kontenerze.
* Ustawia odpowiednie uprawnienia na powitania konta łącznika usługi Azure AD toomanage urządzeń w usłudze Active Directory.
* Tylko musi toorun w jednym lesie, nawet jeśli Azure AD Connect jest instalowany na wiele lasów.

Parametry:

* DomainName: Domena usługi Active Directory którym obiekty urządzeń zostanie utworzona. Uwaga: Wszystkie urządzenia dla podanego lasu usługi Active Directory zostanie utworzona w jednej domenie.
* AdConnectorAccount: Konto usługi Active Directory, który będzie używany przez program Azure AD Connect toomanage obiekty w katalogu hello. To konto hello używane przez tooAD tooconnect synchronizacji Azure AD Connect. Jeśli został zainstalowany przy użyciu ustawień ekspresowych, jest ono kontem hello prefiksem MSOL_.

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a>Część 3: Włącz urządzenia funkcji zapisywania zwrotnego w programie Azure AD Connect
Użyj powitania po zapisu zwrotnego urządzeń tooenable procedury w programie Azure AD Connect.

1. Uruchom ponownie Kreatora instalacji hello. Wybierz **Dostosuj opcje synchronizacji** z hello dodatkowych zadań, a następnie kliknij przycisk **dalej**.
   ![Instalacja niestandardowa Dostosuj opcje synchronizacji](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)
2. Na stronie powitania opcjonalnych funkcji zapisywania zwrotnego urządzeń będą już wyszarzone. Należy pamiętać, że jeśli hello Azure AD Connect przygotowywania kroki nie zostały zakończone zapisu zwrotnego urządzeń będzie wyszarzany limit na stronie funkcje opcjonalne hello. Sprawdź pole powitania dla zapisu zwrotnego urządzeń, a następnie kliknij przycisk **dalej**. Jeśli pole wyboru hello nadal jest wyłączone, zobacz hello [Rozwiązywanie problemów z sekcji](#the-writeback-checkbox-is-still-disabled).
   ![Instalacja niestandardowa opcjonalnych funkcji zapisywania zwrotnego urządzeń](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)
3. Na stronie funkcji zapisywania zwrotnego hello zobaczysz domeny hello dostarczone jako hello domyślnego urządzenia zapisywania zwrotnego lasu.
   ![Niestandardowe lasu docelowego zapisywania zwrotnego urządzeń instalacji](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)
4. Ukończy instalację hello hello kreatora bez zmian konfiguracji dodatkowych. W razie potrzeby odwoływać się zbyt[Instalacja niestandardowa programu Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)

## <a name="enable-conditional-access"></a>Włączanie dostępu warunkowego
W tym scenariuszu są dostępne w ramach tooenable szczegółowe instrukcje [Konfigurowanie lokalnego dostępu warunkowego przy użyciu rejestracji urządzeń usługi Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-devices-are-synchronized-tooactive-directory"></a>Sprawdź, czy urządzenia są synchronizowane tooActive katalogu
Teraz można działa poprawnie zapisu zwrotnego urządzeń. Należy pamiętać, że może potrwać godzin too3 tooAD zapisywane wstecz toobe obiektów urządzeń.  tooverify, że urządzenia są synchronizowanego poprawnie, hello następującego po zakończeniu reguły synchronizacji hello:

1. Uruchom Centrum administracyjne usługi Active Directory.
2. Rozwiń RegisteredDevices, w ramach hello domeny, która jest trwa federacyjnych.
   ![Centrum administracyjnego usługi Active Directory zarejestrowanych urządzeń](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)
3. Zostaną wyświetlone bieżące zarejestrowanych urządzeń.
   ![Lista urządzeń zarejestrowanych Centrum administracyjnego usługi Active Directory](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
### <a name="hello-writeback-checkbox-is-still-disabled"></a>pole wyboru funkcji zapisywania zwrotnego Hello nadal jest wyłączona.
Jeśli hello wyboru dla zapisu zwrotnego urządzeń nie jest włączona, nawet po wykonaniu powyższych kroków hello hello następujące kroki przeprowadzi Cię przez jaki instalacji hello sprawdza kreatora przed hello pole jest włączone.

Przede wszystkim pierwszy:

* Upewnij się, że co najmniej jednego lasu systemu Windows Server 2012 R2. Typ obiektu Hello urządzenie musi być obecny.
* Jeśli Kreator instalacji hello jest już uruchomiona, zmiany nie można wykryć. W takim przypadku ukończyć powitalnych Kreatora instalacji i uruchom go ponownie.
* Upewnij się, że konto hello w skrypcie inicjowania hello jest rzeczywiście hello użytkownika używane przez hello łącznika usługi Active Directory. tooverify, wykonaj następujące kroki:
  * Z hello start menu, otwórz **usługi synchronizacji**.
  * Otwórz hello **łączniki** kartę.
  * Znajdź hello łącznika z typem usług domenowych w usłudze Active Directory i zaznacz go.
  * W obszarze **akcje**, wybierz pozycję **właściwości**.
  * Przejdź za**Connect lesie katalogu tooActive**. Sprawdź, że hello domena i nazwa użytkownika określona skryptu toohello ekranu dopasowania hello podane konto.
    ![Konta łącznika w synchronizacji programu Service Manager](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)

Sprawdź konfigurację w usłudze Active Directory:

* Sprawdź, że hello usługi rejestracji urządzeń znajduje się w lokalizacji hello poniżej (CN DeviceRegistrationService, CN = usługi rejestracji urządzeń, CN = = Device Registration Configuration, CN = Services, CN = Configuration) w kontekście nazewnictwa konfiguracji.

![Rozwiązywanie problemów, DeviceRegistrationService w przestrzeni nazw konfiguracji](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* Sprawdź, czy istnieje tylko jeden obiekt konfiguracji, wyszukując hello konfiguracji w przestrzeni nazw. Jeśli istnieje więcej niż jeden, Usuń zduplikowane hello.

![Rozwiązywanie problemów, wyszukaj hello zduplikowane obiekty](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* W obiekcie usługi rejestracji urządzeń hello upewnij się, hello atrybutu msDS-DeviceLocation jest obecny i ma wartość. Wyszukiwanie tej lokalizacji i upewnij się, że jest obecny razem z objectType hello msDS-DeviceContainer.

![Rozwiązywanie problemów, msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![Rozwiązywanie problemów, klasa obiektu RegisteredDevices](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* Sprawdź konto hello używane przez hello się, że łącznik usługi Active Directory ma wymagane uprawnienia w kontenerze zarejestrowane urządzenia hello znalezione przez hello w poprzednim kroku. Jest to hello oczekiwano uprawnienia do tego kontenera:

![Rozwiązywanie problemów, sprawdź uprawnienia do kontenera](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* Sprawdź hello konta usługi Active Directory ma uprawnienia na powitania CN = Device Registration Configuration, CN = Services, CN = obiekt konfiguracji.

![Rozwiązywanie problemów, sprawdź uprawnienia do Konfiguracja rejestracji urządzeń](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a>Dodatkowe informacje
* [Zarządzanie ryzykiem przy użyciu dostępu warunkowego](../active-directory-conditional-access.md)
* [Konfigurowanie lokalnego dostępu warunkowego przy użyciu rejestracji urządzeń usługi Azure Active Directory](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

