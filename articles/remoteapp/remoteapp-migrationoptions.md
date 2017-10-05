---
title: "Opcje migracji z usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Informacje na temat opcji migracji z usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9ab63124e2521ee1922d15c1e388c54d50eb8301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a>Opcje migracji z usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).


Jeśli zatrzymano przy użyciu usługi Azure RemoteApp z powodu [anonsu wycofania](https://go.microsoft.com/fwlink/?linkid=821148) lub ponieważ po zakończeniu oceny, trzeba przeprowadzać migracji wylogowuje usługi Azure RemoteApp do innej usługi aplikacji. Istnieją dwa różne podejścia do migracji: samozarządzanej (często nazywane infrastruktura jako usługa [IaaS]) wdrożenia lub w pełni zarządzana (zwane często platforma jako usługa) lub oprogramowania jako usługi [PaaS/SaaS] oferty. 

Samoobsługowe IaaS stanowi Zrób wdrożenia, które jest zarządzane, obsługiwana i należące do Ciebie bezpośrednio wdrożonych na maszynach wirtualnych (VM) lub systemów fizycznych. Na drugim końcu pełni zarządzana PaaS/SaaS oferty jest bardzo podobne do usługi Azure RemoteApp — partnera zapewnia warstwę usługi na rozwiązanie usług zdalnych, które obsługuje operacyjnej i obsługi, podczas pracy, jako klienta i do zarządzania niektórych obrazu i aplikacji.

[Wyświetl seminaria Internetowe usługi Azure RemoteApp na opcje migracji](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), lub Dowiedz się więcej informacji (wraz z przykładami różnych opcji hostingu).

## <a name="self-managed-iaas-solutions"></a>Samodzielnie zarządzanej rozwiązań (IaaS)
### <a name="rds-on-iaas"></a>**Usługi pulpitu zdalnego na IaaS**
Można wdrożyć natywnego opartymi na sesji usług pulpitu zdalnego (w systemie Windows Server) wdrażania przy użyciu programów RemoteApp i pulpitów lokalnie lub w środowisku hostowanej (jak na maszynach wirtualnych Azure). Usługi pulpitu zdalnego na wdrożenia IaaS są najlepsze w przypadku klientów już znasz i mają istniejących wiedzy technicznej z wdrożeniami usług pulpitu zdalnego. 

> [!NOTE]
> Należy z Software Assurance (SA) dla licencji dostępu klienta usług pulpitu zdalnego do użycia tej opcji wdrożenia licencjonowania zbiorowego.

Wdrażanie usług pulpitu zdalnego na maszynach wirtualnych Azure jest łatwiejsze niż kiedykolwiek użycia wdrożenia i stosowania poprawek szablonów (odczytu [omówienie](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) , a następnie [pobrać je](https://aka.ms/rdautomation)). Ci elastycznej takie same możliwości skalowania wdrożenia klasycznego Azure zasoby modelu (nie Model zasobów Azure zasobów) w usłudze Azure RemoteApp przy użyciu [automatyczne skalowanie skryptu](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), chociaż występują więcej dostosowania i konfiguracji. Podczas wdrażania usług pulpitu zdalnego na maszynach wirtualnych Azure jest obsługiwana w ramach [Azure obsługuje](https://azure.microsoft.com/support/plans/), taka sama obsługuje specjalistów obsługiwane z usługą Azure RemoteApp. Można pobrać koszt wartościami szacunkowymi określonymi na podstawie istniejących użycia kontaktując się z [pomocą techniczną platformy Azure](https://azure.microsoft.com/support/plans/), lub wykonać obliczenia samodzielnie przy użyciu wkrótce się wydane Kalkulator kosztów.  Ponadto z maszynami wirtualnymi serii N (obecnie w podglądzie prywatnym) można dodać vGPU - Zapoznamy się więcej o dodawaniu vGPU i jak [przewodów ulepszenia usług pulpitu zdalnego w systemie Windows Server 2016](https://myignite.microsoft.com/videos/2794) w naszym Ignite sesji.   

Mamy przewodniki krok po kroku wdrożenia dla [systemu Windows Server 2012 R2](http://aka.ms/rdsonazure) i [systemu Windows Server 2016](http://aka.ms/rdsonazure2016) pomocne w danym wdrożeniu. Zapoznaj się z [blogu pulpitu zdalnego](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) Aby uzyskać najnowsze informacje.

### <a name="citrix-on-iaas"></a>**Citrix na IaaS**
Natywny Citrix, wdrożenia oparte na sesji program XenApp lub XenDesktop może być wdrożona lokalnie lub w środowisku hostowanej (takich jak na maszynach wirtualnych Azure). 

Zapoznaj się w przewodniku krok po kroku wdrażania [7.6 XA Citrix na platformie Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), aby uzyskać więcej informacji. Przeczytaj więcej na temat [Citrix na platformie Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), w tym Kalkulator cen. Możesz również znaleźć [kontaktu Citrix](http://citrix.com/English/contact/index.asp) omówimy opcji z.

## <a name="fully-managed-paassaas-offerings"></a>Pełni zarządzana oferty (PaaS/SaaS)

### <a name="citrix-xenapp-essentials-released-april-2017"></a>Citrix program XenApp Essentials (wydane kwietnia 2017)
Teraz dostępne na [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix program XenApp Essentials jest nowej aplikacji usługi wirtualizacji łączenie możliwościach i elastyczności platformy Citrix chmury z prostego, porady i łatwe korzystanie Wizja funkcji RemoteApp systemu Microsoft Azure. 

Istniejących klientów usługi Azure RemoteApp można [zarejestrować bezpłatnej wersji próbnej](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).  Uwaga: Tylko opłat usługi Citrix jest wolnego, zastosuj Azure koszty zasobów obliczeniowych i magazynu

Dowiedz się więcej:
- [Migracja z usługi Azure RemoteApp do program Citrix XenApp Essentials](remoteapp-migrate-citrix.md)
- [Citrix i firmy Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- [Prezentacja Essentials program XenApp Citrix](https://www.youtube.com/watch?v=91Z7CCfQ-9k).  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a>Citrix program XenApp chmury i usługa XenDesktop 

[Citrix program XenApp chmury i usługa XenDesktop](https://www.citrix.com/products/citrix-cloud/services.html) najlepszym rozwiązaniem w celu dostarczania zarówno aplikacje i komputerów stacjonarnych, oraz zaawansowanego zarządzania i możliwości monitorowania. 

#### <a name="conexlink-platform-name-mycloudit"></a>Conexlink (nazwa platformy: MyCloudIT)
[MyCloudIT](https://mycloudit.com) to platforma automatyzacji dla przedsiębiorstw IT uprościć optymalizacji i skalowania migracji i dostarczanie Pulpity zdalne, zdalne aplikacje i infrastrukturę w chmurze Microsoft Azure. 

Platforma MyCloudIT skraca czas wdrażania przez 95% Azure koszt przez 30% i przenosi całą infrastrukturą informatyczną swoich klientów do chmury w sprawie kilku naciśniętych klawiszy. Partnerzy mogą teraz zarządzać klientami z jedną globalnego pulpitu nawigacyjnego, użytkowników końcowych usługi na całym świecie, takich jak wcześniej i powiększania przychodów bez dodawania dodatkowe obciążenie lub szeroką gamę szkolenia Azure.  

> Lokalizacją główną: Dallas, TX, USA
> 
> Operacja regionu: na całym świecie
> 
> Stan partnera: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)
> 
> Dostawcy usług w chmurze firmy Microsoft: tak
> 
> Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno
> 
> Rozwiązania migracji w usłudze Azure RemoteApp: tak, [Dowiedz się więcej](https://mycloudit.com/remote-app-microsoft/)
> 
> Brianowi Garoutte, VP projektowania biznesowych
> 
> Telefon: 972-218-0741
>   
> Adres e-mail:[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)

### <a name="frame"></a>Ramki

Działy IT w organizacji i dla instytucji rządowych, dostawców usług zarządzanych i wiodącymi dostawcami oprogramowania wybierz ramki do tworzenia i zarządzania ich bezpieczne, zdefiniowanych przez oprogramowanie obszarów roboczych w chmurze. Small dużych organizacjach, ramki ułatwia niezwykle zezwala użytkownikom na dostęp do aplikacji systemu Windows w dowolnej przeglądarce na dowolnym urządzeniu. Platforma ramki obejmuje wszystko, co administrator musi wdrożyć aplikacje w chmurze, łącznie z infrastrukturą systemu Azure i licencji usług pulpitu zdalnego (dostarczają własne konto platformy Azure i licencji jest opcjonalny). 

Dowiedz się więcej o [ramki na platformie Azure](https://www.fra.me/ara). 

> Lokalizacją główną: Mateo sieci San, urząd certyfikacji, USA
>
> Operacja regionu: na całym świecie
>
> Partnera firmy Microsoft: tak
> 
> Telefon: 1-480-269-4668

### <a name="awingu"></a>Awingu
Awingu zapewnia rozwiązanie proste obszarów roboczych systemem starsze aplikacje, SaaS i dokumenty przy użyciu przeglądarki html5. Tak udostępniania aplikacji bezpiecznego na typ urządzenia. Usługi SaaS op Single-Sign-On opcje szeroki zakres jest dostępna. Również różnych (w chmurze) systemy plików mogą ściśle zintegrowana z obszaru roboczego. Obok pełne mobilności w Awingu sformatowanego obszarów roboczych zapewni optymalnych zabezpieczeń szczegółową kontrolę (np. Pobieranie/przekazywanie), pełny użycia inspekcji, uwierzytelnianie wieloskładnikowe (np. Azure MFA), sesja rejestrowania i inne. Out-of--box, Awingu umożliwia dokumentu i udostępnianie sesji aplikacji wersją zoptymalizowaną a bezpiecznej współpracy.
Rozwiązanie firmy Awingu jest wielodostępnej, usługi AD i otwarty interfejs API. Jest on używany przez małych i dużych firmach, dostawcom usług w chmurze i [niezależnym dostawcom oprogramowania](http://www.isv2saas.com). Tych klientów docenia szczególnie całkowitego kosztu posiadania łatwe użycia, łatwość do zainstalowania i niski.

Awingu w-jednego jest [dostępne w portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) z 2 wbudowanych równoczesnych użytkowników. Dodatkowe licencje nie są dostępne za pośrednictwem [szeroką gamę dystrybutorów i odsprzedawców](http://www.awingu.com/reseller).

Dowiedz się więcej o [Awingu na jako alternatywne do usługi Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).


> Lokalizacją główną: Belgia
> 
> Operacyjny regionów: EMEA, Ameryki Północnej i Brazylia
> 
> Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno 
> 
> **Globalne**:
> 
> Arnaud Marlière, CMO
> 
> Adres e-mail:[arnaud@awingu.com](mailto:arnaud@awingu.com)
> 
> Telefon: +1 646 583 3025
> 
> **HQ Belgii**:
> 
> B44 Ottergemsesteenweg Zwid 808
> 
> 9000 Gent
> 
> Adres e-mail:[info@awingu.com](mailto:info@awingu.com) 
> 
> Numer telefonu: + 32 9 296 40 11
> 
> **USA**:
> 
> floor 7, Zapisz 1177 z Americas,
> 
> Nowy Jork, NY 10036
> 
> Adres e-mail:[info.us@awingu.com](mailto:info.us@awingu.com)

### <a name="microsoft-hosted-service-provider"></a>Dostawcy usług hostowanych Microsoft
Partnerzy hostingowi oferują zwykle w pełni zarządzana hostowanej pulpitu systemu Windows i usługi aplikacji, która może obejmować zarządzanie zasobami Azure, systemów operacyjnych, aplikacji i pomoc techniczna za pomocą partnera obiektu licencji zbiorowych firmy Microsoft i innych oprogramowanie dostawcy wraz z trwa umowy licencyjnej dostawcy usługi umożliwia odsprzedaż z licencji dostępu subskrybenta (SAL). Poniżej przedstawiono szczegóły i informacje kontaktowe dla niektórych dostawców usług hostingowych specjalizujących udzielania pomocy użytkownikom ich migracji usługi Azure RemoteApp. Zapoznaj się z [bieżącej listy obsługiwanych dostawców usług](http://aka.ms/rdsonazurecertified) który zakończył usług pulpitu zdalnego na IaaS uczenia ścieżkę i oceny.  

### <a name="citrix-service-provider-program"></a>Program dostawcy usługi Citrix
Program dostawcy usługi Citrix ułatwia dla dostawców usług, aby dostarczyć prostotę chmury wirtualne małych i średnich firmach, w środowisku oferowanie ich usługi, które chcą łatwe, z modelu. Dostawcy usług Citrix wzrostu ich firm SPLA firmy Microsoft i rozwiń inwestycji platformy usług pulpitu zdalnego z dowolnego urządzenia, dostęp z dowolnego miejsca, najszerszych obsługę aplikacji, bogate środowisko, zwiększyć bezpieczeństwo i zwiększenia skalowalności. Z kolei Citrix usługodawców przyciągania więcej subskrybentów, bardziej zadowoleni i zmniejszyć koszty operacyjne, ich. [Dowiedz się więcej](http://www.citrix.com/products/service-providers.html) lub [Znajdź partnera](https://www.citrix.com/buy/partnerlocator.html).

#### <a name="acuutech"></a>Acuutech
[Acuutech](http://www.acuutech.com) specjalizuje się w zapewnienie hostowanych rozwiązań pulpitu, dostarczania pełnego pulpitu i aplikacje niezależnego dostawcy oprogramowania środowiska oparte na technologii firmy Microsoft do globalnego podstawowej klienta z platformy Azure i ich centrów danych.

> Lokalizacją główną: Londynie, UK; Singapur; Houston, TX
> 
> Operacja regionu: na całym świecie
> 
> Stan partnera: Gold
> 
> Dostawcy usług w chmurze firmy Microsoft: tak
> 
> Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno
> 
> Rozwiązania migracji w usłudze Azure RemoteApp: tak, [Dowiedz się więcej](http://www.acuutech.com/ara-migration/)
> 
> **Zjednoczone Królestwo**:
>   
> 5/6 Jorku dom, drogowej Langston
>   
> Loughton, Essex IG10 3TQ
>   
> Numer telefonu: + 44 (0) 20 8502 2155
> 
> **Singapuru**:
>   
> Ulica 100 Cecil, #09-02 
>   
> Świecie Singapuru 069532
> 
> Numer telefonu: + 65 6709 4933
>   
> **Ameryka Północna**:
>   
> 3601 S. Sandman St.
>   
> Pakiet 200, Houston, TX 77098
>   
> Telefon: +1 713 691 0800

#### <a name="aspex"></a>ASPEX
[ASPEX](http://www.aspex.be/en) specjalizuje się niezależnym dostawcom oprogramowania przejście do chmury i niezależnego dostawcy oprogramowania "wyszukiwania w celu optymalizacji ich bieżącej konfiguracji chmury. ASPEX oferuje szeroką gamę usług zarządzanych, metodyki devops i usługi konsultingowe.  

> Lokalizacją główną: Antwerpia, Belgia
> 
> Operacja regionu: Europa Zachodnia
> 
> Stan partnera: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)
> 
> Dostawcy usług w chmurze firmy Microsoft: tak
> 
> Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno
> 
> Rozwiązania migracji w usłudze Azure RemoteApp: tak, [Dowiedz się więcej](https://www.aspex.be/en/azure-remote-apps)
> 
> Telefon: +3232202198
> 
> Poczty:[info@aspex.be](mailto:info@aspex.be)
> 
> Sieci Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)

#### <a name="caasecom"></a>Caase.com
[Caase.com](http://www.caase.com/) pomaga firmom, lokalnych, szczebla, -rządowych treści i opieki zdrowotnej instytucje z podróży kierunku inteligentny sposób pracy w Microsoft Cloud. Trwa produktywności i bezpieczeństwo w dowolnym miejscu z dowolnego urządzenia i niskich kosztach IT. Caase.com jest wartość true, specjalistę ds dla Microsoft Office365, Azure, Enterprise Mobility i zabezpieczeń oraz systemu Windows. W naszym doradcze migracji usług, programy wdrożenia, szkolenia zarządzania i obsługi technicznej Caase.com tworzy zoptymalizowane i bezpieczne platformy współpracy dla klientów pracownikom, partnerom i dostawców.
Caase.com jest mastermind zdalnego obszaru roboczego Azure (przenośnych w miejscu pracy) i w miejscu pracy cyfrowych (społecznościowych intranetu). Oba rozwiązania — realizowane za pomocą przyjęcia — są foundation, który gwarantuje, że użytkownicy z tych rozwiązań przyjemne, pomyślnie i najbardziej efektywny doświadczenie w ich trasy do Microsoft Cloud.
Holenderski tłumaczenia ánd obsługi film, w tym miejscu: http://caase.com/over-ons/

> Operacja regionu: holenderski podstawie globalne
> 
> Stan partnera: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)
> 
> Dostawcy usług w chmurze firmy Microsoft: tak
> 
> Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno
> 
> Rozwiązania migracji w usłudze Azure RemoteApp: tak, [więcej](http://caase.com/diensten/microsoft-azure/).
> 
> 
> Holandia:
> 
> Rigtersbleek-Zandvoort 10 (De Spinnerij)
> 
> 7521 BE, Enschede
> 
> Telefon: +31 (0) 88 4320 000


#### <a name="nerdio"></a>Nerdio
[Nerdio dla platformy Azure](http://getnerdio.com/nfa/) to platforma automatyzacji IT, która zapewnia było bardzo proste inicjowania obsługi, zarządzania i optymalizacji pełną środowiska IT w chmurze firmy Microsoft. Wstanie pulpitów wirtualnych, aplikacji zdalnych i serwery w kilka godzin. Administrowanie środowiskiem w trzech kliknięć lub z portalu administracyjnego Nerdio. Użyj inteligentnego automatyczne skalowanie i Zapisz 40 – 60% zasobów IaaS platformy Azure.

> Lokalizacją główną: region operacji Chicago, IL: status partnera na całym świecie: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) dostawcy usług w chmurze firmy Microsoft: tak
> 
> Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno
> 
> Rozwiązania migracji w usłudze Azure RemoteApp: tak
> 
> 
> Zapisz Lincoln 8001
> 
> Suite 212
> 
> Skokie, IL 60077
> 
> Stany Zjednoczone
> 
> Zewnętrzne 4NERDIO (844) 6
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a>**SaaSplaza**
[SaaSplaza](http://www.saasplaza.com/) oferuje pełną Microsoft Dynamics portfolio (NAV AX, zasad grupy, SL, CRM) chmury prywatnej i publicznej (Azure).

> Lokalizacją główną: (Holandia)
> 
> Operacja regionu: na całym świecie
> 
> Stan partnera: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)
> 
> Dostawcy usług w chmurze firmy Microsoft: tak
> 
> Oferowanie programów RemoteApp i pulpitu rozwiązań opartych na sesji: tak, zarówno
> 
> **EMEA**:
> 
> Prins Mauritslaan 29 35
> 
> Badhoevedorp 71 LP
> 
> (Holandia)
> 
> Telefon: 8060 547 20 +31 
> 
>  **Americas**:
> 
> 105 171 Saksonii drogowej, Suite
> 
> 92024 Encinitas, urząd certyfikacji
> 
> Diego sieci SAN
> 
> Stany Zjednoczone
> 
> Telefon: +1 858 385 8900 
> 
> **APAC**:
> 
> 105 Cecil ulica
>    
> \#11-08, ośmiokąt
> 
> Singapuru 069534
> 
> Singapur
>   
> Phone - Singapuru: 6591 6222 + 65
> 
> Phone - Australii: 5568 8310 2 +61 
>    
> Phone — Nowa Zelandia: 0321 488 4 +64
> 
## <a name="need-more-help"></a>Potrzebujesz dodatkowej pomocy?
Nadal potrzebna pomoc, wybierając lub więcej pytań? Aby uzyskać pomoc, użyj jednej z poniższych metod. 

1. Wiadomość e-mail na adres [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
2. Skontaktuj się z [pomocy technicznej platformy Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Uruchamianie przez otwarcie [sprawy pomocy technicznej platformy Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
3. Rozmowa. [Znajdź lokalny numer sprzedaży](https://azure.microsoft.com/overview/sales-number/).

