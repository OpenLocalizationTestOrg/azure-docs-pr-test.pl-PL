---
title: "aaaSet zasady zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia tooconfigure zasad zabezpieczeń w Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3b9e1c15-3cdb-4820-b678-157e455ceeba
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: yurid
ms.openlocfilehash: 59226dd84a1c66a2d8367417060ab10a1ff73848
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-security-policies-in-azure-security-center"></a>Ustawianie zasad zabezpieczeń w usłudze Azure Security Center
Ten dokument ułatwia tooconfigure zasad zabezpieczeń w Centrum zabezpieczeń przeprowadzi Cię przez hello tooperform niezbędne kroki tego zadania.

>[!NOTE] 
>Począwszy od początku czerwca 2017, Centrum zabezpieczeń używa programu Microsoft Monitoring Agent hello toocollect i magazynu danych. Zobacz [migracji Platform Centrum zabezpieczeń Azure](security-center-platform-migration.md) toolearn więcej. Witaj informacje w tym artykule reprezentuje funkcji Centrum zabezpieczeń po toohello przejścia programu Microsoft Monitoring Agent.
>

## <a name="what-are-security-policies"></a>Czym są zasady zabezpieczeń?
Zasady zabezpieczeń definiuje zestaw hello formantów, które są zalecane dla zasobów w ramach hello określonej subskrypcji. W Centrum zabezpieczeń można zdefiniować zasady dla subskrypcji platformy Azure, zgodnie z potrzebami zabezpieczeń firmy tooyour i typem aplikacji hello lub czułości hello danych w każdej subskrypcji.

Na przykład zasoby używane do celów projektowania lub testowania mogą mieć inne wymagania dotyczące zabezpieczeń niż te, które są używane przez aplikacje produkcyjne. Aplikacje z danymi podlegającymi ochronie (takimi jak dane osobowe) mogą wymagać wyższego poziomu zabezpieczeń. Zasady zabezpieczeń, które są włączone w Centrum zabezpieczeń Azure dysku — zalecenia dotyczące zabezpieczeń i monitorowania toohelp znalezienie potencjalnych luk i uniknięcie zagrożeń. Odczyt [przewodnik planowania Centrum zabezpieczeń Azure i obsługi](security-center-planning-and-operations-guide.md) więcej informacji na temat jak toodetermine hello opcji, które jest odpowiednie dla Ciebie.

## <a name="set-security-policies"></a>Ustawianie zasad zabezpieczeń
Zasady zabezpieczeń można skonfigurować dla każdej subskrypcji. toomodify zasady zabezpieczeń, musi być właścicielem lub współautorem subskrypcji. Zaloguj się w portalu Azure toohello i wykonaj hello pomyślne wykonanie czynności, które zasady tooconfigure zabezpieczeń w Centrum zabezpieczeń:

1. Kliknij przycisk hello **zasad** kafelka na pulpicie nawigacyjnym Centrum zabezpieczeń hello.
2. W bloku zasady zabezpieczeń hello, który zostanie otwarty Wybierz subskrypcję hello, na którym ma zostać zasady zabezpieczeń hello tooenable.

    ![Definiowanie zasad](./media/security-center-policies/security-center-policies-fig1-ga.png)
3. Witaj **zasady zabezpieczeń** zostanie otwarty blok hello wybrane subskrypcji z zestawu opcji. Witaj dostępne w tym bloku są następujące opcje:

   * **Zasady zapobiegania**: użycie tej opcji zasad tooconfigure na subskrypcję.  
   * **Powiadomienia e-mail**: Użyj tej opcji tooconfigure wiadomość e-mail z powiadomieniem wysyłanych na powitania pierwsze codzienne wystąpienie alertu i alerty o wysokim znaczeniu. Preferencje poczty e-mail można konfigurować tylko dla zasad dotyczących subskrypcji. Odczyt [podać szczegóły dotyczące kontaktu zabezpieczeń w Centrum zabezpieczeń Azure](security-center-provide-security-contact-details.md) Aby uzyskać więcej informacji o tym, jak tooconfigure wiadomość e-mail z powiadomieniem.
   * **Warstwa cenowa**: Użyj tej opcji hello tooupgrade, wybór warstwy cenowej. Zobacz [cennik Centrum zabezpieczeń](security-center-pricing.md) toolearn więcej o cenach opcje.
4. Upewnij się, że opcja **Zbieraj dane z maszyn wirtualnych** jest włączona (**Wł.**). Ta opcja umożliwia automatyczne zbieranie danych dziennika dla istniejących i nowych zasobów przy użyciu hello Microsoft Monitoring Agent — jest to hello samego agenta używane przez usługę Operations Management Suite i analizy dzienników hello. Będą przechowywane dane z tego agenta jest skojarzone z subskrypcją platformy Azure istniejących obszarów roboczych usługi Analiza dzienników lub nowych obszarów roboczych, uwzględniając geograficzne hello konta z hello maszyny Wirtualnej.

5. W hello **zasady zabezpieczeń** bloku, kliknij przycisk **zasady zapobiegania** toosee hello dostępnych opcji. Kliknij przycisk **na** tooenable hello zalecenia dotyczące zabezpieczeń, które są odpowiednie dla tej subskrypcji.

    ![Wybieranie zasad zabezpieczeń hello](./media/security-center-policies/security-center-policies-fig7.png)

Użyj hello w poniższej tabeli jako toounderstand odwołanie poszczególnych opcji:

| Zasady | Gdy ustawienie jest włączone |
| --- | --- |
| Aktualizacje systemu |Codziennie pobiera listę dostępnych aktualizacji zabezpieczeń i aktualizacji krytycznych z usługi Windows Update lub Windows Server Update Services. Lista pobrane Hello zależy od usługi hello, który jest skonfigurowany dla tej maszyny wirtualnej i zaleca się, że zastosowanie hello brakujących aktualizacji. Dla systemów Linux zasad hello używa hello pakietów dostarczanego distro zarządzania systemu toodetermine pakiety, które są dostępne aktualizacje. Sprawdzane są również aktualizacje zabezpieczeń i aktualizacje krytyczne z maszyn wirtualnych usługi [Azure Cloud Services](../cloud-services/cloud-services-how-to-configure.md). |
| Luki w zabezpieczeniach systemu operacyjnego |Analizuje konfiguracje codzienne toodetermine problemy z systemem operacyjnym wchodzące tooattack narażone hello maszyny wirtualnej. zasady Hello zaleca także tooaddress zmiany konfiguracji te luki w zabezpieczeniach. Zobacz hello [liście zalecanych linii bazowych](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335) Aby uzyskać więcej informacji na temat hello konkretnych konfiguracji, które są monitorowane. (Obecnie system Windows Server 2016 nie jest w pełni obsługiwany). |
| Ochrona punktów końcowych |Zaleca się toobe ochrony punktu końcowego obsługi administracyjnej dla wszystkich maszyn wirtualnych systemu Windows toohelp identyfikację oraz usunięcie wirusów, programów szpiegujących i innego złośliwego oprogramowania. |
| Szyfrowanie dysków |Zaleca włączenie szyfrowania dysku w wszystkich maszyn wirtualnych tooenhance ochrony danych magazynowanych. |
| Grupy zabezpieczeń sieci |Zaleca, aby [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) można toocontrol skonfigurowany dla ruchu przychodzącego i wychodzącego ruchu tooVMs, który ma publiczne punkty końcowe. Grupy zabezpieczeń sieci skonfigurowane dla podsieci są dziedziczone przez wszystkie interfejsy sieciowe maszyny wirtualnej, chyba że określono inaczej. Ponadto toochecking, że grupa zabezpieczeń sieci została skonfigurowana, ta zasada ocenia reguły zabezpieczeń ruchu przychodzącego tooidentify reguł, które zezwalają na ruch przychodzący. |
| Zapora aplikacji sieci Web |Zaleca się, że Zapora aplikacji sieci web można zainicjowana na maszynach wirtualnych, gdy spełniony jest jeden z następujących hello: </br></br>[Wystąpienie poziomu publicznego adresu IP](../virtual-network/virtual-networks-instance-level-public-ip.md) służy (ILPIP) i hello reguły zabezpieczeń ruchu przychodzącego dla skojarzonej sieciowej grupy zabezpieczeń hello są skonfigurowane tooallow dostępu tooport 80/443.</br></br>IP równoważeniem obciążenia jest używany i hello skojarzone równoważenia obciążenia i ruchu przychodzącego adresu translacji adresów reguły są skonfigurowane tooallow dostępu tooport 80/443. Aby uzyskać więcej informacji, zobacz artykuł [Azure Resource Manager support for Load Balancer](../load-balancer/load-balancer-arm.md) (Obsługa usługi Azure Resource Manager dla modułu równoważenia obciążenia). |
| Zapora nowej generacji |Powoduje rozszerzenie ochrony sieci poza grupy zabezpieczeń sieci, które są wbudowane w platformę Azure. Centrum zabezpieczeń wykryje wdrożenia, dla których zaleca się zaporę nowej generacji i Włącz tooprovision urządzenie wirtualne. |
| Inspekcja SQL i wykrywanie zagrożeń |Zaleca przeprowadzanie inspekcji dostępu tooAzure bazy danych można włączone dla zgodności i także zaawansowane wykrywanie zagrożeń do celów dochodzenia. |
| Szyfrowanie SQL |Zaleca się, aby funkcja szyfrowania nieaktywnych danych była włączona dla usługi Azure SQL Database, powiązanych kopii zapasowych i plików dziennika transakcji. Dzięki temu nawet w przypadku włamania się do danych, nie będzie można ich odczytać. |
| Ocena luk w zabezpieczeniach |Zaleca się zainstalowanie na maszynie wirtualnej rozwiązania do oceny luk w zabezpieczeniach. |
| Szyfrowanie w usłudze Storage |Obecnie ta funkcja jest dostępna dla plików i obiektów blob Azure. Po włączeniu szyfrowania w usłudze Storage szyfrowane będą tylko nowe dane, a wszystkie pliki istniejące już na tym koncie magazynu pozostaną niezaszyfrowane. |
| Dostęp do sieci JIT |Gdy tylko w czasie jest włączona, Centrum zabezpieczeń blokuje ruch przychodzący tooyour maszynach wirtualnych platformy Azure przez tworzenie reguły NSG. Wybierz porty hello na powitania toowhich maszyny Wirtualnej można zablokować ruch przychodzący. Aby uzyskać więcej informacji, zobacz [Manage virtual machine access using just in time](https://docs.microsoft.com/azure/security-center/security-center-just-in-time) (Zarządzanie dostępem maszyny wirtualnej przy użyciu funkcji „dokładnie na czas”). |

Po skonfigurowaniu wszystkich opcji kliknij przycisk **OK** w hello **zasady zabezpieczeń** bloku zalecenia hello, a następnie kliknij przycisk **zapisać** w hello **zabezpieczeń Zasady** bloku, który zawiera ustawienia początkowe hello.

> [!NOTE]
> Hello warstwa cenowa jest nadal stosowana na poziomie grupy zasobów hello. Aby uzyskać więcej informacji, odwiedzając hello [cennik](https://azure.microsoft.com/pricing/details/security-center/) strony.
>
>

## <a name="see-also"></a>Zobacz też
W tym dokumencie możesz przedstawiono sposób tooconfigure zasad zabezpieczeń w Centrum zabezpieczeń Azure. toolearn więcej informacji na temat Centrum zabezpieczeń Azure, zobacz następujące hello:

* [Przewodnik planowania i obsługi usługi Azure Security Center](security-center-planning-and-operations-guide.md). Dowiedz się, jak tooplan i zrozumieć zagadnienia dotyczące projektowania hello tooadopt Centrum zabezpieczeń Azure.
* [Monitorowanie kondycji zabezpieczeń w usłudze Azure Security Center](security-center-monitoring.md). Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md). Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w usłudze Azure Security Center](security-center-partner-solutions.md). Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Azure Security Center — często zadawane pytania](security-center-faq.md). Znajdź często zadawane pytania dotyczące korzystania z usługi hello.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/). Wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.
