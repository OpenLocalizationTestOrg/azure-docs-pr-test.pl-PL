---
title: "aaaUpgrade klastra usługi sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "Uaktualnij hello kodu sieci szkieletowej usług i/lub konfigurację, która działa w klastrze usługi sieć szkieletowa usług, w tym ustawieniu trybu aktualizacji klastra, certyfikaty, dodawanie portów aplikacji, sposób poprawek systemu operacyjnego, uaktualnienie i tak dalej. Czego można oczekiwać po hello uaktualnienia są wykonywane?"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a>Uaktualnianie klastra usługi sieć szkieletowa usług Azure
> [!div class="op_single_selector"]
> * [Klastrze platformy Azure](service-fabric-cluster-upgrade.md)
> * [Autonomiczny klastra](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

Systemu nowoczesnych projektowanie na możliwość jest długoterminowym sukcesie tooachieving klucza produktu. Klaster sieci szkieletowej usług Azure jest z zasobem, który jest właścicielem, ale jest częściowo zarządzany przez firmę Microsoft. W tym artykule opisano, co jest zarządzana automatycznie i samodzielnie skonfigurować.

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a>Kontrolowanie hello wersji sieci szkieletowej, która działa w klastrze
Można ustawić sieci szkieletowej automatyczne tooreceive klastra uaktualnień zgodnie z ich wydania przez firmę Microsoft lub wybrać wersji obsługiwanych sieci szkieletowej, która ma toobe Twojego klastra na.

Aby to zrobić, konfiguracja klastra "parametr upgrademode musi mieć" hello ustawienia w portalu hello lub za pomocą Menedżera zasobów w czasie tworzenia hello lub nowsza w klastrze na żywo 

> [!NOTE]
> Upewnij się, że tookeep klastra zawsze uruchomiona wersja obsługiwanych sieci szkieletowej. Gdy firma Microsoft ogłaszamy hello wydaniu nowej wersji platformy service fabric, poprzednia wersja hello jest oznaczony do zakończenia wsparcia po co najmniej 60 dni. Witaj nowości hello są ogłaszane [na blogu zespołu sieci szkieletowej usług hello](https://blogs.msdn.microsoft.com/azureservicefabric/). nową wersję Hello jest następnie toochoose dostępne. 
> 
> 

14 dni wygaśnięcia toohello wcześniejszych wersji hello klaster działa, zdarzenie kondycji jest generowany, który umieszcza klastra ostrzegawczy stan kondycji. Hello klaster będzie pozostawał w stanie ostrzeżenia, do momentu uaktualnienia tooa sieci szkieletowej obsługiwanej wersji.

### <a name="setting-hello-upgrade-mode-via-portal"></a>Ustawianie trybu uaktualniania hello za pośrednictwem portalu
Podczas tworzenia klastra hello można ustawić tooautomatic klastra hello lub ręcznie.

![Create_Manualmode][Create_Manualmode]

Można ustawić tooautomatic klastra hello, lub ręcznie, gdy w klastrze na żywo, za pomocą hello zarządzanie. 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a>Uaktualnianie tooa nową wersję w klastrze, który jest ustawiony tryb tooManual za pośrednictwem portalu.
Nowa wersja tooa tooupgrade toodo wystarczy wybierz z listy rozwijanej hello hello dostępnych wersji i Zapisz. uaktualnienie sieci szkieletowej Hello pobiera rozpoczęte automatycznie. Witaj zasady dotyczące kondycji klastra (kombinacja kondycji węzła i kondycji hello hello wszystkie aplikacje uruchomione w klastrze hello) są przestrzegane tooduring hello uaktualnienia.

Jeśli zasady dotyczące kondycji hello klastra nie są spełnione, uaktualnienie hello zostanie wycofana. Przewiń w dół tego dokumentu tooread więcej na temat tooset tych zasad dotyczących kondycji niestandardowych. 

Po wyeliminowaniu hello problemy, które spowodowało wycofanie hello, należy tooinitiate hello uaktualnianie ponownie, przez następujące hello takie same jak poprzednio kroki.

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a>Ustawianie trybu uaktualniania hello za pomocą szablonu usługi Resource Manager
Dodaj definicję zasobu Microsoft.ServiceFabric/clusters toohello konfiguracji "parametr upgrademode musi mieć" hello i tooone "clusterCodeVersion" hello zestawu z hello obsługiwane wersje sieci szkieletowej, jak pokazano poniżej, a następnie wdrożyć hello szablonu. Prawidłowe wartości Hello "parametr upgrademode musi mieć" to "Ręczny" lub "Automatyczny"

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a>Uaktualnianie tooa nową wersję w klastrze, który jest ustawiony tryb tooManual za pomocą szablonu usługi Resource Manager.
Gdy hello klastra jest w trybie ręcznym tooupgrade tooa nowej wersji zmienić hello "clusterCodeVersion" tooa obsługiwanej wersji i wdrożyć ją. wdrożenia Hello hello szablonu, kopnięć uaktualnienia programu Fabric hello pobiera rozpoczęte automatycznie. Witaj zasady dotyczące kondycji klastra (kombinacja kondycji węzła i kondycji hello hello wszystkie aplikacje uruchomione w klastrze hello) są przestrzegane tooduring hello uaktualnienia.

Jeśli zasady dotyczące kondycji hello klastra nie są spełnione, uaktualnienie hello zostanie wycofana. Przewiń w dół tego dokumentu tooread więcej na temat tooset tych zasad dotyczących kondycji niestandardowych. 

Po wyeliminowaniu hello problemy, które spowodowało wycofanie hello, należy tooinitiate hello uaktualnianie ponownie, przez następujące hello takie same jak poprzednio kroki.

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a>Pobierz listę wszystkich dostępnych wersji dla wszystkich środowisk w ramach danej subskrypcji
Uruchom hello następujące polecenie, a następnie należy pobrać toothis podobne dane wyjściowe.

"supportExpiryUtc" informuje użytkownika w przypadku danej wersji wygaśnie lub jego ważność wygasła. Witaj najnowszej wersji nie ma prawidłowej daty — ma wartość "9999-12-31T23:59:59.9999999", co oznacza tylko, że data wygaśnięcia hello nie jest jeszcze ustawiony.

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a>Zachowanie uaktualnienia sieci szkieletowej, gdy tryb uaktualniania klastra hello jest automatyczny
Firma Microsoft udostępnia hello kodu sieci szkieletowej i konfigurację, która działa w klastrze platformy Azure. Możemy przeprowadzić oprogramowania toohello automatycznych uaktualnień monitorowanych na zgodnie z potrzebami. Te uaktualnienia może być kodu i konfiguracji. toomake się upewnić, że aplikacja wystąpi Brak wpływu lub minimalny wpływ powodu toothese uaktualnień, możemy wykonywać hello uaktualnień w hello następujące etapy:

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a>Faza 1: Uaktualnianie jest przeprowadzane przy użyciu wszystkich zasad dotyczących kondycji klastra
W tej fazie uaktualnień hello kontynuować domeny uaktualnienia pojedynczo i hello aplikacje, które były uruchomione w klastrze hello nadal toorun bez żadnego przestoju. Witaj zasady dotyczące kondycji klastra (kombinacja kondycji węzła i kondycji hello hello wszystkie aplikacje uruchomione w klastrze hello) są przestrzegane tooduring hello uaktualnienia.

Jeśli zasady dotyczące kondycji hello klastra nie są spełnione, uaktualnienie hello zostanie wycofana. Następnie właściciel toohello hello subskrypcji zostanie wysłana wiadomość e-mail. Witaj w wiadomości e-mail zawierają hello następujących informacji:

* Powiadomienie, że było ponownie tooroll uaktualniania klastra.
* Sugerowane akcje naprawcze, jeśli istnieje.
* Witaj liczbę dni (n), dopóki nie możemy wykonać fazy 2.

Spróbujemy hello tooexecute sam uaktualnienia kilka razy w przypadku uaktualniania nie powiodło się ze względów infrastruktury. Po hello n dni od hello Data hello e-mail została wysłana, możemy kontynuować tooPhase 2.

Jeśli zasady dotyczące kondycji klastra hello są spełnione, uaktualnienie hello jest uznawany za pomyślny i oznaczone jako ukończone. Może to nastąpić podczas uaktualniania początkowej hello lub dowolnego powtórki uaktualnienia hello na tym etapie. Nie ma żadnych wiadomości e-mail z potwierdzeniem pomyślnego uruchomienia. Jest to tooavoid wysyłanie zostanie zbyt dużo żądań wiadomości e-mail — odbieranie wiadomości e-mail powinien być traktowany jako toonormal wyjątek. Oczekujemy większość toosucceed uaktualnienia klastra hello bez wpływu na dostępność Twojej aplikacji.

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a>Faza 2: Uaktualnianie jest przeprowadzane przy użyciu tylko zasady dotyczące kondycji domyślne
zasady dotyczące kondycji Hello na tym etapie są ustawiane w taki sposób, że liczba hello aplikacji, które są w dobrej kondycji na początku hello uaktualnienia hello pozostaje hello takie same dla hello czas trwania procesu uaktualniania hello. Jak Faza 1 uaktualnień hello fazy 2 kontynuować domeny uaktualnienia pojedynczo i hello aplikacje, które były uruchomione w klastrze hello nadal toorun bez żadnego przestoju. zasady dotyczące kondycji klastra Hello (kombinacja kondycji węzła i kondycji hello hello wszystkie aplikacje uruchomione w klastrze hello) są toofor przyklejonej hello czas trwania uaktualniania hello.

Jeśli zasady dotyczące kondycji klastra hello skutkuje nie są spełnione, uaktualnienie hello zostanie wycofana. Następnie właściciel toohello hello subskrypcji zostanie wysłana wiadomość e-mail. Witaj w wiadomości e-mail zawierają hello następujących informacji:

* Powiadomienie, że było ponownie tooroll uaktualniania klastra.
* Sugerowane akcje naprawcze, jeśli istnieje.
* Witaj liczbę dni (n), dopóki nie możemy wykonać fazy 3.

Spróbujemy hello tooexecute sam uaktualnienia kilka razy w przypadku uaktualniania nie powiodło się ze względów infrastruktury. Przypomnienie e-mail jest wysyłana kilka dni, n dni są włączone. Po hello n dni od hello Data hello e-mail została wysłana, możemy kontynuować tooPhase 3. wiadomości powitania możemy wysłać Faza 2 należy podjąć poważnie i należy podjąć działania naprawcze.

Jeśli zasady dotyczące kondycji klastra hello są spełnione, uaktualnienie hello jest uznawany za pomyślny i oznaczone jako ukończone. Może to nastąpić podczas uaktualniania początkowej hello lub dowolnego powtórki uaktualnienia hello na tym etapie. Nie ma żadnych wiadomości e-mail z potwierdzeniem pomyślnego uruchomienia.

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a>Faza 3: Uaktualnianie jest przeprowadzane za pomocą zasady dotyczące kondycji aktywnego
Te zasady dotyczące kondycji w tej fazie są przeznaczone dla ukończenia uaktualnienia hello zamiast hello kondycję aplikacji hello. Bardzo mało uaktualnienia klastra przechodzili na tym etapie. Jeśli klaster pobiera toothis fazy, istnieje duże prawdopodobieństwo, że aplikacja staje się nieprawidłowy, i/lub utratę dostępności.

Podobne toohello innych dwóch faz uaktualnienia fazy 3 kontynuować jedną domenę uaktualnienia naraz.

Jeśli zasady dotyczące kondycji hello klastra nie są spełnione, uaktualnienie hello zostanie wycofana. Spróbujemy hello tooexecute sam uaktualnienia kilka razy w przypadku uaktualniania nie powiodło się ze względów infrastruktury. Po wykonaniu tej klastra hello jest przypięty, aby go nie będziesz już otrzymywać pomocy technicznej i/lub uaktualnień.

Właściciel subskrypcji toohello, wraz z czynności zaradczych hello jest wysłana wiadomość e-mail z tymi informacjami. Nie oczekuje się żadnych tooget klastrów w stanie, w którym fazy 3 nie powiodło się.

Jeśli zasady dotyczące kondycji klastra hello są spełnione, uaktualnienie hello jest uznawany za pomyślny i oznaczone jako ukończone. Może to nastąpić podczas uaktualniania początkowej hello lub dowolnego powtórki uaktualnienia hello na tym etapie. Nie ma żadnych wiadomości e-mail z potwierdzeniem pomyślnego uruchomienia.

## <a name="cluster-configurations-that-you-control"></a>Konfiguracje klastrów, które kontrolujesz
Ponadto tryb uaktualniania toohello możliwości tooset hello klastra, w tym miejscu są hello konfiguracje, które można zmienić w klastrze na żywo.

### <a name="certificates"></a>Certyfikaty
Możesz dodać nowe lub łatwo usunąć certyfikaty dla klastra hello i klienta za pośrednictwem portalu hello. Odwołuje się zbyt[tego dokumentu, aby uzyskać szczegółowe instrukcje](service-fabric-cluster-security-update-certs-azure.md)

![Zrzut ekranu pokazujący odciski palców certyfikatów hello portalu Azure.][CertificateUpgrade]

### <a name="application-ports"></a>Porty aplikacji
Porty aplikacji można zmienić, zmieniając właściwości zasobów usługi równoważenia obciążenia hello, które są skojarzone z typem węzła hello. Można użyć portalu hello, lub można użyć programu PowerShell Menedżera zasobów bezpośrednio.

Nowy port na wszystkich maszynach wirtualnych w typie węzła tooopen hello następujące:

1. Dodaj nowy sondowania toohello odpowiedniej usługi równoważenia obciążenia.
   
    Jeśli klaster jest wdrożony za pomocą portalu hello, usługi równoważenia obciążenia hello są nazywane "LB Nazwa grupy zasobów hello-NodeTypename", po jednej dla każdego typu węzła. Ponieważ nazwy usługi równoważenia obciążenia hello różnią się tylko w obrębie grupy zasobów, najlepiej wyszukiwania je w obszarze określonej grupy zasobów.
   
    ![Zrzut ekranu pokazujący Dodawanie tooa sondowania załadować równoważenia w portalu hello.][AddingProbes]
2. Dodaj nowe reguły toohello modułu równoważenia obciążenia.
   
    Dodaj nowy toohello reguły sama usługa równoważenia obciążenia przy użyciu sondowania hello, utworzony w poprzednim kroku hello.
   
    ![Dodawanie nowej reguły równoważenia obciążenia tooa w portalu hello.][AddingLBRules]

### <a name="placement-properties"></a>Właściwości umieszczania
Dla każdego typu węzła hello możesz dodać niestandardowe właściwości umieszczania mają toouse w aplikacji. Typ NodeType jest używanej bez dodawania go jawnie właściwości domyślnej.

> [!NOTE]
> Szczegółowe informacje na temat użycia hello ograniczeń umieszczania, właściwości węzła i jak toodefine, znajduje się w sekcji toohello "Umieszczania ograniczenia i właściwości węzła" hello dokumentu zasobu klastra sieci szkieletowej programu Service Manager w [opisujące Your klastra ](service-fabric-cluster-resource-manager-cluster-description.md).
> 
> 

### <a name="capacity-metrics"></a>Metryki pojemności
Dla każdego typu węzła hello możesz dodać niestandardowe metryki pojemności mają toouse w obciążenia tooreport aplikacji. Szczegółowe informacje dotyczące użycia hello obciążenia tooreport metryki pojemności, toohello dokumentów zasobu klastra sieci szkieletowej programu Service Manager znajduje się w [opisujące Your klastra](service-fabric-cluster-resource-manager-cluster-description.md) i [metryki i obciążenia](service-fabric-cluster-resource-manager-metrics.md).

### <a name="fabric-upgrade-settings---health-polices"></a>Zasady kondycji sieci szkieletowej ustawienia uaktualnienia —
Można określić, czy zasady niestandardowe kondycji dla uaktualnienia programu fabric. Jeśli ustawiono tooAutomatic Twojego klastra sieci szkieletowej uaktualnień, te zasady Pobierz zastosowane toohello pierwszą fazę hello sieci szkieletowej automatycznych uaktualnień.
Jeśli ustawiono klastra sieci szkieletowej ręczne uaktualnienia, a następnie te zasady zastosowane każdorazowo wybrania nowej wersji wyzwalania tookick systemu hello poza uaktualnienia programu fabric hello w klastrze. Jeśli nie zastępują zasady hello, używane są ustawienia domyślne hello.

Można określić zasady dotyczące kondycji niestandardowych hello lub przejrzyj hello bieżące ustawienia w obszarze bloku "uaktualnienia programu fabric" hello, wybierając hello Zaawansowane ustawienia uaktualnienia. Przejrzyj hello poniższej ilustracji na temat. 

![Zarządzanie zasadami kondycji niestandardowych][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a>Dostosowywanie ustawień sieci szkieletowej dla klastra
Odwołuje się zbyt[ustawień sieci szkieletowej klastra sieci szkieletowej usług](service-fabric-cluster-fabric-settings.md) na co jest i jak można dostosować je.

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a>Poprawek systemu operacyjnego na powitania maszyny wirtualne wchodzące w skład klastra hello
Odwołuje się zbyt[poprawki aplikacji aranżacji](service-fabric-patch-orchestration-application.md) którego można wdrożyć na poprawki tooinstall z klastra z usługi Windows Update w sposób orchestrated zachować dostępność usług hello cały czas hello. 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a>Uaktualnień systemu operacyjnego na powitania maszyny wirtualne wchodzące w skład klastra hello
Jeśli musisz uaktualnić hello obrazu systemu operacyjnego na maszynach wirtualnych hello hello klastra, należy to robić jedną maszynę Wirtualną w czasie. Przydadzą się osobom odpowiedzialnym dla tego uaktualnienia — nie ma obecnie nie automatyzacji tego.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak toocustomize niektóre hello [ustawień sieci szkieletowej klastra sieci szkieletowej usług](service-fabric-cluster-fabric-settings.md)
* Dowiedz się, jak za[i wylogowywanie skalowanie klastra](service-fabric-cluster-scale-up-down.md)
* Dowiedz się więcej o [uaktualnienia aplikacji](service-fabric-application-upgrade.md)

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
