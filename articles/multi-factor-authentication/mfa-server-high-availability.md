---
title: "aaaConfigure serwera usługi Azure MFA w celu zapewnienia wysokiej dostępności | Dokumentacja firmy Microsoft"
description: "Wdrażanie wielu wystąpień serwera usługi Azure Multi-Factor Authentication w konfiguracji, które zapewniają wysoką dostępność."
services: multi-factor-authentication
keywords: "Usługa Azure MFA"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 8c6b1921c734c7a7273e443b3591fbbb15cd5e6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-high-availability"></a>Konfigurowanie serwera usługi Azure Multi-Factor Authentication wysokiej dostępności

tooachieve wysokiej dostępności z wdrożeniem usługi Azure MFA serwera, należy toodeploy wielu serwerów usługi MFA. Ta sekcja zawiera informacje na tooachieve równoważeniem obciążenia projektowania celów wysokiej dostępności w możesz wdrożenia serwera MFS Azure.

## <a name="mfa-server-overview"></a>Omówienie serwera usługi MFA

Hello Architektura usługi Azure MFA serwera obejmuje kilka składników, pokazane na powitania po diagramu:

 ![Architektura serwera usługi MFA](./media/mfa-server-high-availability/mfa-ha-architecture.png)

Serwer usługi MFA jest Windows Server, który jest hello Azure Multi-Factor Authentication zainstalowane. wystąpienie serwera usługi MFA Hello musi być aktywowany przez hello usługi MFA w toofunction platformy Azure. Więcej niż jeden serwer usługi MFA może być zainstalowana na lokalnym.

Hello jest pierwszy serwer usługi MFA, w którym jest zainstalowany hello głównego serwera usługi MFA podczas aktywacji przez hello usługi Azure MFA domyślnie. serwer główny MFA Hello ma kopię zapisu bazy danych PhoneFactor.pfdata hello. Kolejnych instalacji wystąpienia serwera usługi MFA są nazywane slaves. Witaj MFA slaves ma replikowane tylko do odczytu kopię hello PhoneFactor.pfdata bazy danych. Serwery MFA replikować informacji za pomocą zdalnego wywoływania procedur (RPC). Wszystkie serwery usługi MFA muszą zbiorczo zostać przyłączony do domeny lub autonomiczny tooreplicate informacji.

Zarówno MFA i podrzędna serwerów usługi MFA komunikować się z hello usługi MFA, gdy jest wymagane uwierzytelnianie dwuskładnikowe. Na przykład gdy użytkownik próbuje toogain dostępu tooan aplikację, która wymaga uwierzytelniania dwuskładnikowego, hello użytkownik zostanie najpierw uwierzytelniony przez dostawcę tożsamości, takie jak Active Directory (AD).

Po pomyślnym uwierzytelnieniu w usłudze AD powitania serwera usługi MFA będą komunikować się z hello usługi MFA. powitania serwera usługi MFA czeka na powiadomienie z tooallow usługi MFA hello lub odmówić hello użytkownika dostępu toohello aplikacji.

Jeśli serwer główny MFA hello przejdzie do trybu offline, uwierzytelnienia mogą nadal być przetwarzane, ale operacje wymagające zmiany toohello MFA w bazie danych nie można przetworzyć. (Przykłady: hello dodanie użytkowników samoobsługi zmiany numeru PIN i zmiana informacji o użytkowniku)

## <a name="deployment"></a>Wdrożenie

Należy wziąć pod uwagę hello następujące punkty ważne dla równoważenia obciążenia serwera usługi Azure MFA i jej powiązane składniki.

* **Przy użyciu usługi RADIUS standardowe tooachieve wysokiej dostępności**. Jeśli używasz usługi Azure MFA serwerów jako serwery RADIUS, można skonfigurować jako podstawowy cel uwierzytelniania usługi RADIUS i innymi serwerami usługi MFA Azure jako miejsca docelowe dodatkowego uwierzytelniania potencjalnie jeden serwer usługi MFA. Jednak nie może być przydatna tej metody tooachieve wysokiej dostępności, ponieważ musi czekać na toooccur okres limitu czasu, jeśli uwierzytelnianie nie powiedzie się w celu uwierzytelniania podstawowego hello przed mogą być uwierzytelniane względem hello dodatkowego uwierzytelniania. obiekt docelowy. Jest bardziej wydajne tooload saldo hello ruchu usługi RADIUS między klientem RADIUS hello i hello serwerów RADIUS (w tym przypadku hello Azure MFA serwerów, działając jako serwery RADIUS), aby hello klientów RADIUS można skonfigurować pojedynczy adres URL, który może wskazywać.
* **Należy toomanually wspierania MFA slaves**. Jeśli serwer główny usługi Azure MFA hello przejdzie do trybu offline, hello dodatkowej Azure MFA serwery nadal tooprocess żądania usługi MFA. Jednak dopóki głównego serwera usługi MFA są dostępne, Administratorzy nie można dodać użytkowników lub zmodyfikować ustawienia uwierzytelniania MFA, a użytkownicy nie mogą wprowadzać zmiany przy użyciu portalu użytkowników hello. Promowanie MFA podrzędna toohello rolę wzorca jest zawsze proces ręczny.
* **Odrębność składników**. powitania serwera usługi Azure MFA obejmuje kilka składników, które mogą być instalowane na hello tego samego wystąpienia systemu Windows Server lub w różnych wystąpieniach. Następujące składniki: hello Portal użytkowników, Mobile App Web Service i hello adapter AD FS (agent). To odrębność ułatwia możliwe toouse powitania serwera Proxy aplikacji sieci Web toopublish hello portalu użytkownika i serwera sieci Web aplikacji mobilnej z hello sieci obwodowej. Taka konfiguracja dodaje toohello ogólne bezpieczeństwo projektu, jak pokazano w powitania po diagramu. Hello Portal użytkowników usługi MFA i serwera sieci Web aplikacji mobilnej może również wdrożyć w konfiguracji równoważenia obciążenia wysokiej dostępności.

   ![Serwer usługi MFA w sieci obwodowej](./media/mfa-server-high-availability/mfasecurity.png)

* **Hasła jednorazowego (OTP) za pośrednictwem programu SMS (alias jednokierunkowe SMS) wymaga użycia hello trwałe sesje, jeśli ruch jest równoważeniem obciążenia**. Jednokierunkowe programu SMS to opcja uwierzytelniania, która powoduje, że użytkownicy hello toosend serwera usługi MFA hello wiadomość tekstową zawierającą OTP. w oknie monitu toocomplete hello żądanie uwierzytelniania MFA, Hello użytkownik wprowadza hello OTP. Po załadowaniu saldo Azure MFA serwerów hello tym samym serwerze, który obsłużył żądanie uwierzytelniania początkowego hello musi być powitania serwera, który odbiera wiadomości powitania OTP od użytkowników hello; inny serwer usługi MFA odbiera hello OTP odpowiedzi, hello żądanie uwierzytelnienia nie powiedzie się. Aby uzyskać więcej informacji, zobacz [jedno hasło czas za pośrednictwem dodać SMS tooAzure serwera usługi MFA](https://blogs.technet.microsoft.com/enterprisemobility/2015/03/02/one-time-password-over-sms-added-to-azure-mfa-server).
* **Równoważeniem obciążenia wdrożeń hello portalu użytkowników i Mobile App Web Service wymaga trwałe sesje**. Jeśli jesteś równoważenia obciążenia hello Portal użytkowników usługi MFA i hello Mobile App Web Service, każdej sesji musi toostay na powitania tym samym serwerze.

## <a name="high-availability-deployment"></a>Wdrożenie wysokiej dostępności

Witaj Poniższy diagram przedstawia zakończenia HA równoważeniem obciążenia wdrożenia usługi Azure MFA i jego składników, wraz z usług AD FS dla odwołania.

 ![Azure MFA serwera HA implementacji](./media/mfa-server-high-availability/mfa-ha-deployment.png)

Należy zwrócić uwagę hello następujące elementy dla obszaru powitalne numerowane odpowiednio hello poprzedzających diagramu.

1. Witaj, które są dwa serwery uwierzytelnianie wieloskładnikowe Azure (MFA1 i MFA2) załadować zrównoważony (mfaapp.contoso.com) i są skonfigurowane toouse bazie PhoneFactor.pfdata hello (4443) tooreplicate portu statycznego. Hello zestawu SDK usług sieci Web jest zainstalowany na każdym powitania serwera usługi MFA tooenable komunikacji za pośrednictwem portu TCP 443 hello serwerów usług AD FS. serwery MFA Hello są wdrażane w bezstanowej konfiguracji usługi równoważenia obciążenia. Jednak jeśli chce toouse OTP za pośrednictwem programu SMS, musi użyć równoważenia obciążenia stanowe.
   ![Azure MFA Serwer - App wysokiej dostępności](./media/mfa-server-high-availability/mfaapp.png)

   > [!NOTE]
   > Ponieważ RPC używa portów dynamicznych, zapory tooopen się toohello zakres portów dynamicznych, które mogą za pomocą usługi RPC nie jest zalecane. Jeśli Zapora jest **między** MFA serwerów aplikacji, należy skonfigurować toocommunicate serwera usługi MFA hello na portu statycznego dla hello replikacji ruchu między serwerami główne i podrzędne i otwórz port w zaporze. Możesz wymusić portu statycznego hello tworząc wartości DWORD rejestru na ```HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Positive Networks\PhoneFactor``` o nazwie ```Pfsvc_ncan_ip_tcp_port``` i ustawienie wartości hello tooan dostępny port statyczny. Połączenia są zawsze inicjowane przez hello podrzędna serwerów MFA toohello wzorzec, hello portu statycznego jest wymagana tylko na wzorcu hello, ale ponieważ w dowolnym momencie, możesz podwyższyć poziom wzorca hello toobe podrzędny, należy ustawić portu statycznego hello na wszystkich serwerach usługi MFA.

2. serwery aplikacji mobilnej użytkownika usługi MFA w portalu/Witaj dwie (uwierzytelnianie wieloskładnikowe-UP-MAS1 i MFA-UP-MAS2) jest równoważone w **stateful** konfiguracji (mfa.contoso.com). Odwołaj, że trwałe sesje są wymagania dotyczące równoważenia obciążenia hello MFA użytkownika portalu i usługi aplikacji mobilnej.
   ![Serwer usługi Azure MFA — portalem użytkowników a usługą aplikacji mobilnych wysokiej dostępności](./media/mfa-server-high-availability/mfaportal.png)
3. farmy serwerów usług AD FS Hello jest obciążenia zrównoważonym i opublikowane w sieci obwodowej hello toohello Internet za pośrednictwem równoważenia obciążenia serwerów proxy usług AD FS. Każdy serwer usług AD FS używa toocommunicate agenta usług AD FS hello z hello Azure MFA serwerów przy użyciu jednej z równoważeniem obciążenia adresu URL (mfaapp.contoso.com) za pośrednictwem portu TCP 443.

## <a name="next-steps"></a>Następne kroki

* [Instalowanie i konfigurowanie serwera usługi Azure MFA](multi-factor-authentication-get-started-server.md)
