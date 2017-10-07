---
title: "aplikacje aaaPublishing na oddzielne sieci i lokalizacje przy użyciu łącznika grup w serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Obejmuje jak toocreate grup łączników w serwera Proxy aplikacji usługi Azure AD i zarządzanie nimi."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publikowanie aplikacji w odrębnych sieci i lokalizacje przy użyciu grup łącznika
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](active-directory-application-proxy-connectors-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-application-proxy-connectors.md)
>

Klienci korzystają z serwera Proxy aplikacji usługi Azure AD dla scenariuszy coraz więcej i aplikacji. Dlatego wprowadziliśmy serwera Proxy aplikacji jeszcze bardziej elastyczne przez włączenie więcej topologii. Można utworzyć grupy łącznika serwera Proxy aplikacji, dzięki czemu można przypisać określone łączniki tooserve określonych aplikacji. Ta funkcja daje więcej toooptimize kontrolki i sposób wdrożenia serwera Proxy aplikacji. 

Każdy łącznik serwera Proxy aplikacji jest przypisany tooa łącznika grupy. Witaj wszystkie łączniki, które należy toohello tej samej grupie łącznik działa jako oddzielny zespół wysokiej dostępności i równoważenia obciążenia. Wszystkie łączniki należy tooa łącznika grupy. Jeśli nie utworzono grup, wszystkie łączniki są grupy domyślnej. Administrator może tworzyć nowe grupy i przypisz toothem łączników w hello portalu Azure. 

Wszystkie aplikacje są przypisywane tooa łącznika grupy. Jeśli nie utworzono grup, wszystkie aplikacje są przypisywane tooa domyślnej grupy. Ale łączniki zorganizować w grupy, należy ustawić toowork każdej aplikacji z grupą określony łącznik. W takim przypadku tylko łączniki hello w tej grupie obsługi aplikacji hello na żądanie. Ta funkcja jest przydatna, jeśli aplikacji znajdują się w różnych lokalizacjach. Można utworzyć grup łącznika na podstawie lokalizacji, dzięki czemu aplikacje zawsze są obsługiwane przez łączniki, które są fizycznie Zamknij toothem.

>[!TIP] 
>Jeśli masz dużego wdrożenia serwera Proxy aplikacji nie przypisano żadnej grupy aplikacji toohello domyślnego łącznika. W ten sposób nowe łączniki nie odbierać ruchu na żywo, do momentu przypisania ich tooan łącznika usługi active grupy. Ta konfiguracja pozwala również tooput łączników w trybie bezczynności przez przeniesienie ich wstecz toohello domyślnej grupy, tak, aby można było wykonać konserwacji bez wywierania wpływu na użytkowników.

## <a name="prerequisites"></a>Wymagania wstępne
toogroup łączników, masz toomake się, że możesz [zainstalować wiele łączników](active-directory-application-proxy-enable.md). Po zainstalowaniu nowego łącznika automatycznie sprzężenia hello **domyślne** grupy łącznika.

## <a name="create-connector-groups"></a>Utwórz grupy dla łącznika
Użyj tych kroków toocreate dowolną liczbę grup łącznika. 

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
1. Wybierz **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **serwera proxy aplikacji**.
2. Wybierz **nową grupę łącznika**. zostanie wyświetlony blok nową grupę łącznika Hello.

   ![Wybierz nową grupę łącznika](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. Nadaj nazwę nowej grupy łącznika, a następnie użyj hello tooselect menu listy rozwijanej, która łączników, należy w tej grupie.
4. Wybierz pozycję **Zapisz**.

## <a name="assign-applications-tooyour-connector-groups"></a>Przypisz tooyour łącznika grup aplikacji
Wykonaj te czynności dla każdej aplikacji, która została już opublikowana przy użyciu serwera Proxy aplikacji. Najpierw opublikować lub można przypisywać te kroki toochange hello przy każdym można przypisać grupę aplikacji tooa łącznika.   

1. Pulpit nawigacyjny zarządzania powitania dla katalogu, zaznacz **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje** > tooassign tooa łącznika grupa aplikacji hello >  **Serwer Proxy aplikacji**.
2. Użyj hello **grupy łącznika** listy rozwijanej menu tooselect hello grupę hello toouse aplikacji.
3. Wybierz **zapisać** tooapply hello zmiany.

## <a name="use-cases-for-connector-groups"></a>Przypadki użycia grup łącznika 

Łącznik grupy są przydatne w przypadku różnych scenariuszy, w tym:

### <a name="sites-with-multiple-interconnected-datacenters"></a>Lokacji z wieloma połączonych centrów danych

Organizacje często mają liczba połączonych centrów danych. W takim przypadku ma tookeep tyle ruchu w ramach centrum danych hello możliwie ponieważ łącza między datacenter są kosztowne i bardzo wolno. Można wdrożyć łączników w każdym datacenter tooserve tylko hello aplikacje znajdujące się w obrębie centrum danych hello. Takie podejście minimalizuje łącza między datacenter i zapewnia całkowicie przezroczysty tooyour użytkowników.

### <a name="applications-installed-on-isolated-networks"></a>Aplikacje zainstalowane w izolowanych sieciach

Aplikacje mogą być przechowywane w sieciach, które nie są częścią sieci firmowej głównego hello. Łącznik grup tooinstall dedykowanego łączników można użyć w izolowanych sieciach tooalso odizolowanego aplikacji toohello sieci. Zazwyczaj dzieje się tak, gdy dostawców przechowuje określonej aplikacji w Twojej organizacji. 

Łącznik grupy umożliwiają możesz tooinstall dedykowanego łączników dla tych sieci, które publikują tylko określonych aplikacji, co ułatwia i bardziej bezpieczne zarządzanie aplikacjami toooutsource toothird dostawców.

### <a name="applications-installed-on-iaas"></a>Aplikacje zainstalowane na IaaS 

Aplikacje zainstalowane na IaaS, aby uzyskać dostęp do chmury łącznik grupy zapewniają wspólnej toosecure hello dostępu tooall hello aplikacje usługi. Łącznik grup nie utworzyć dodatkowe zależności w sieci firmowej lub fragmentu środowisko aplikacji hello. Łączniki można zainstalować na każdym centrum danych w chmurze i służyć tylko te aplikacje, które znajdują się w tej sieci. Można zainstalować wiele łączników tooachieve wysokiej dostępności.

Należy podjąć, na przykład organizacja, która ma kilka maszyn wirtualnych połączony tootheir własnych IaaS hostowanych sieci wirtualnej. toouse pracowników tooallow te aplikacje są tych sieci prywatnych toohello połączonych sieci firmowej przy użyciu sieci VPN lokacja lokacja. To zapewnia dobre dla pracowników znajdujących się w siedzibie firmy. Jednak go może nie być idealne w przypadku pracowników zdalnych, ponieważ wymaga dostępu tooroute infrastruktury dodatkowych lokalnych, jak widać w poniższym diagramie hello:

![AzureAD sieci Iaas](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
Przy użyciu grup łącznika serwera Proxy aplikacji usługi Azure AD można włączyć usługi toosecure hello dostępu tooall aplikacje bez tworzenia dodatkowe zależności w sieci firmowej:

![Dostawców chmury Iaas wielu AzureAD](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a>Łącznik różnych grup dla każdego lasu z obejmującego wiele lasów

Większość klientów, którzy wdrożyli serwera Proxy aplikacji korzystają z jego możliwości jednokrotnej (SSO), wykonując delegowanie ograniczone protokołu Kerberos (KCD). tooachieve to łącznika hello maszyny potrzeby toobe tooa przyłączone do domeny, która można delegować użytkowników hello kierunku aplikacji hello. Delegowanie KCD obsługuje możliwości między lasami. Jednak dla przedsiębiorstw, które mają różne środowiska obejmującego wiele lasów, bez zaufania między nimi, pojedynczy łącznik nie może służyć do wszystkich lasów. 

W takim przypadku określone łączniki mogą być wdrażane dla każdego lasu i zestaw tooserve aplikacje, które zostały opublikowane tooserve hello tylko użytkownicy tego określonego lasu. Każda grupa łącznika reprezentuje innego lasu. Gdy hello dzierżawy i większość środowisko hello jest unified dla wszystkich lasów, użytkownicy mogą być przypisani tootheir lasu aplikacji za pomocą grup usługi Azure AD.
 
### <a name="disaster-recovery-sites"></a>Lokacjach odzyskiwania po awarii

Istnieją dwa różne podejścia, które można wykonać z lokacją odzyskiwanie po awarii, w zależności od sposobu implementacji witryn sieci:

* Jeśli witryna odzyskiwania po awarii jest wbudowana w trybie aktywny / aktywny, gdzie jest dokładnie takie same jak hello lokacji głównej i ma takie same hello sieci i ustawienia usług AD można utworzyć łączniki hello w witrynie hello odzyskiwania po awarii w hello tej samej grupie łącznika co hello lokacji głównej. Dzięki temu usługi Azure AD toodetect pracy w trybie Failover dla Ciebie.
* Jeśli witryna odzyskiwania po awarii jest oddzielony od lokacji głównej hello, można utworzyć grupę inny łącznik w witrynie hello odzyskiwania po awarii, a albo 1) ma aplikacjom kopii zapasowych lub 2) ręcznie kierowanie grupy łącznika toohello DR istniejących aplikacji hello zgodnie z potrzebami.
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a>Obsłużyć wielu firm z pojedynczej dzierżawy

Istnieje wiele różnych sposobów usług dla wielu firm związanych z tooimplement w modelu, w którym pojedynczego usługodawcy wdraża i obsługuje usługę Azure AD. Łącznik grupy ułatwiają Witaj, Administratorze segregowanie hello łączników i aplikacji w różnych grupach. Jedną z metod, które jest odpowiednie dla małych firm, jest toohave pojedynczej dzierżawy usługi Azure AD podczas hello różne przedsiębiorstwa mają własne nazwy domeny i sieci. Dotyczy to również M i scenariusze i sytuacji jeśli pojedynczy dzielenia IT służy firm kilka przyczyn przepisami lub pracy. 

## <a name="sample-configurations"></a>Przykładowe konfiguracje

Przykłady, które można zaimplementować obejmują hello następujące grupy łącznika.
 
### <a name="default-configuration--no-use-for-connector-groups"></a>Domyślna konfiguracja — używana dla łącznika grup

Jeśli nie używasz grup łącznika, konfigurację będzie wyglądała następująco:

![AzureAD żadnych grup łącznika](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
Ta konfiguracja jest odpowiednia dla małych wdrożeń i testy. Może ona również działać prawidłowo, jeśli organizacja ma topologii siecią płaską.
 
### <a name="default-configuration-and-an-isolated-network"></a>Domyślna konfiguracja i sieci izolowanej

Ta konfiguracja jest ewolucji hello domyślny, w którym jest specyficzne dla aplikacji z systemem w sieci izolowanej takich jak IaaS sieci wirtualnej: 

![AzureAD żadnych grup łącznika](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a>Zalecana konfiguracja — kilku określonych grup i domyślnej grupy dla bezczynności

zalecana konfiguracja w przypadku dużych i złożonych organizacji Hello jest toohave hello domyślna łącznika grupy jako grupa nie obsługiwać wszystkich aplikacji, która jest używana dla łączników bezczynności lub nowo zainstalowany. Wszystkie aplikacje są obsługiwane przy użyciu grup niestandardowych łącznika. Dzięki temu wszystkie złożoność hello opisanych powyżej scenariuszy hello.

W poniższym przykładzie hello hello firma dysponuje dwoma centrami danych, A i B, z dwa łączniki, które pełnią każdej lokacji. Każda lokacja ma różne aplikacje, które działają na nim. 

![AzureAD żadnych grup łącznika](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a>Następne kroki

* [Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)
* [Włączanie logowania jednokrotnego](application-proxy-sso-overview.md)


