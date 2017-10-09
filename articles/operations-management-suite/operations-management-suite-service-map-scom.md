---
title: Mapa integracji programu System Center Operations Manager aaaService | Dokumentacja firmy Microsoft
description: "Mapa usługi jest rozwiązaniem Operations Management Suite, który automatycznie odnajduje składniki aplikacji w systemie Windows i systemów Linux i map hello komunikacji między usługami. W tym artykule omówiono przy użyciu mapy usługi tooautomatically tworzenie diagramów aplikacji rozproszonej w programie Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>Mapa usług integracji z programem System Center Operations Manager
  > [!NOTE]
  > Ta funkcja jest dostępna w publicznej wersji zapoznawczej.
  > 
  
Mapa usług pakiet zarządzania Operations automatycznie wykrywa składniki aplikacji w systemach Windows i Linux i mapuje hello komunikacji między usługami. Mapy usługi umożliwia tooview swojemu hello serwerów traktować ich jako połączonych systemy, które dostarczają usług krytycznych. Mapa usługi pokazuje połączeń między serwerami, procesów i portów w dowolnej architekturze połączenia TCP, bez konieczności wykonywania konfiguracyjnych wymaganych oprócz hello instalację agenta. Aby uzyskać więcej informacji, zobacz hello [mapy usługi dokumentacji](operations-management-suite-service-map.md).

Dzięki tej integracji między mapy usługi i System Center Operations Manager może automatycznie tworzyć diagramy aplikacji rozproszonej w programie Operations Manager, które są oparte na powitania dynamiczne zależności mapy w mapy usługi.

## <a name="prerequisites"></a>Wymagania wstępne
* Grupy zarządzania programu Operations Manager, który jest zarządzany z zestawu serwerów.
* Obszar roboczy usługi Operations Management Suite z hello włączonej funkcji mapy usługi.
* Zestaw serwerów (co najmniej jeden), które są zarządzane przez programu Operations Manager i wysyłania danych tooService mapy. Serwery z systemem Windows i Linux są obsługiwane.
* Nazwy głównej usługi z toohello dostępu subskrypcji Azure, która jest skojarzona z obszarem roboczym usługi Operations Management Suite hello. Aby uzyskać więcej informacji, przejdź zbyt[Tworzenie nazwy głównej usługi](#creating-a-service-principal).

## <a name="install-hello-service-map-management-pack"></a>Zainstaluj pakiet administracyjny hello mapy usług
Należy włączyć hello integrację programu Operations Manager a Service Map importując hello Microsoft.SystemCenter.ServiceMap pakietu administracyjnego (Microsoft.SystemCenter.ServiceMap.mpb). Witaj pakietu zawiera hello następujące pakiety administracyjne:
* Widoki aplikacji mapy usługi firmy Microsoft
* Wewnętrzny mapy usługi programu Microsoft System Center
* Zastąpienia mapy usługi programu Microsoft System Center
* Mapa usług programu Microsoft System Center

## <a name="configure-hello-service-map-integration"></a>Konfigurowanie hello mapy usługi integracji
Po zainstalowaniu pakietu administracyjnego hello mapy usługi nowy węzeł **mapy usługi**, jest wyświetlana w obszarze **Operations Management Suite** w hello **administracji** okienka. 

tooconfigure mapy usług integracji, hello następujące:

1. tooopen hello Kreatora konfiguracji w hello **omówienie mapy usługi** okienku, kliknij przycisk **Dodawanie obszaru roboczego**.  

    ![W okienku omówienie mapy usług](media/oms-service-map/scom-configuration.png)

2. W hello **konfiguracji połączenia** okna, wprowadź nazwę dzierżawcy hello lub identyfikator, Identyfikatora aplikacji (znanej także jako nazwa użytkownika hello lub clientID) i hasło hello nazwy głównej usługi, a następnie kliknij przycisk **dalej**. Aby uzyskać więcej informacji, przejdź zbyt[Tworzenie nazwy głównej usługi](#creating-a-service-principal).

    ![Witaj konfiguracji połączenia okna](media/oms-service-map/scom-config-spn.png)

3. W hello **wyboru subskrypcji** okna, wybierz hello subskrypcji platformy Azure, grupy zasobów platformy Azure (hello, który zawiera obszar roboczy usługi Operations Management Suite hello) i obszar roboczy usługi Operations Management Suite, a następnie kliknij przycisk **Dalej**.

    ![Witaj obszar roboczy konfiguracji menedżera operacji](media/oms-service-map/scom-config-workspace.png)

4. W hello **wybranej grupy maszyny** okna, możesz wybrać grupy maszyny mapy usługi ma toosync tooOperations Manager. Kliknij przycisk **grupami maszyn Dodaj lub usuń**, wybierz grupy z listy hello **dostępnych grup maszyny**i kliknij przycisk **Dodaj**.  Po wybraniu grup kliknij przycisk **Ok** toofinish.
    
    ![Witaj grup maszyny konfiguracji programu Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. W hello **wybór serwera** okna, konfigurowania hello grupy serwerów mapy usługi z serwerami hello, które mają toosync między programem Operations Manager i mapy usługi. Kliknij przycisk **Dodaj lub Usuń serwery**.   
    
    Aby toobuild integracji hello diagramu aplikacji rozproszonej dla serwera serwer hello musi mieć:

    * Zarządzane przez program Operations Manager
    * Zarządzane przez usługę mapy
    * Na liście hello grupy serwerów mapy usługi

    ![Witaj Grupa konfiguracji programu Operations Manager](media/oms-service-map/scom-config-group.png)

6. Opcjonalnie: Wybierz powitania serwera zarządzania zasobów puli toocommunicate usłudze Operations Management Suite, a następnie kliknij przycisk **Dodaj obszar roboczy**.

    ![Witaj puli zasobów konfiguracji menedżera operacji](media/oms-service-map/scom-config-pool.png)

    Może on potrwać minutę tooconfigure i zarejestruj obszar roboczy usługi Operations Management Suite hello. Po skonfigurowaniu programu Operations Manager inicjuje hello pierwszej synchronizacji mapy usługi Operations Management Suite.

    ![Witaj puli zasobów konfiguracji menedżera operacji](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>Monitor mapy usług
Po podłączeniu obszar roboczy usługi Operations Management Suite hello nowego folderu, mapy usług jest wyświetlana w hello **monitorowanie** okienku hello konsoli programu Operations Manager.

![Witaj okienku Monitoring programu Operations Manager](media/oms-service-map/scom-monitoring.png)

Witaj mapy usługi znajduje się w nim czterech węzłów:
* **Aktywne alerty**: Wyświetla listę wszystkich aktywnych alertów hello o hello komunikacji między programem Operations Manager i mapy usługi.  Należy pamiętać, że te alerty nie są alerty Operations Management Suite jest zsynchronizowany tooOperations menedżera. 

* **Serwery**: Wyświetla hello monitorowane serwery, które są skonfigurowane toosync z mapy usługi.

    ![Witaj w okienku monitorowanie serwerów programu Operations Manager](media/oms-service-map/scom-monitoring-servers.png)

* **Maszyny widoków zależności grup**: Wyświetla listę wszystkich grup maszyny, które są synchronizowane z mapy usługi. Możesz kliknąć tooview wszystkie grupy diagram swojej aplikacji rozproszonej.

    ![diagram aplikacji rozproszonej menedżera operacji Hello](media/oms-service-map/scom-group-dad.png)

* **Widoki zależności serwera**: Wyświetla listę wszystkich serwerów, które są synchronizowane z mapy usługi. Możesz kliknąć tooview dowolnego serwera diagram swojej aplikacji rozproszonej.

    ![diagram aplikacji rozproszonej menedżera operacji Hello](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a>Edytowanie lub usuwanie obszaru roboczego hello
Możesz edytować lub usunąć obszar roboczy hello skonfigurowane za pomocą hello **omówienie mapy usługi** okienka (**administracji** okienko > **Operations Management Suite**  >  **Usługi mapy**). Teraz można skonfigurować tylko jeden obszar roboczy usługi Operations Management Suite.

![w okienku Menedżera Edytuj obszar roboczy usługi Operations Hello](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>Konfigurowanie reguł i zastąpień
Reguła, _Microsoft.SystemCenter.ServiceMapImport.Rule_, jest tworzona tooperiodically pobierania informacji z mapy usługi. toochange chronometrażu synchronizacji, można skonfigurować zastąpienia reguły hello (**tworzenie** okienko > **reguły** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).

![Okno właściwości zastępuje programu Operations Manager Hello](media/oms-service-map/scom-overrides.png)

* **Włączone**: Włącz lub Wyłącz Aktualizacje automatyczne. 
* **IntervalMinutes**: zresetować hello między aktualizacjami. Witaj domyślny interwał to jedna godzina. Chcąc mapy serwera toosync częściej, można zmienić wartości hello.
* **TimeoutSeconds**: hello długość czasu, zanim upłynie limit czasu żądania hello resetowania. 
* **TimeWindowMinutes**: resetowanie przedział czasu hello na potrzeby zapytań o dane. Domyślna to 60-minutowe okna. Hello maksymalna wartość dozwolona przez usługę mapy wynosi 60 min.

## <a name="known-issues-and-limitations"></a>Znane problemy i ograniczenia

Hello bieżący projekt przedstawia hello następujące problemy i ograniczenia:
* Obszar roboczy usługi Operations Management Suite pojedynczego tooa można łączyć.
* Mimo że można dodawać serwery toohello grupy serwerów mapy usługi ręcznie za pośrednictwem hello **tworzenie** okienku hello mapy dla tych serwerów nie zostały zsynchronizowane natychmiast.  Podczas następnego cyklu synchronizacji hello one będą synchronizowane z mapy usługi.
* Jeśli wprowadzisz zmiany toohello rozproszonych aplikacji diagramy utworzone przez pakiet administracyjny hello te zmiany zostaną zastąpione prawdopodobnie na powitania następnej synchronizacji z mapy usługi.

## <a name="create-a-service-principal"></a>Tworzenie nazwy głównej usługi
Oficjalnej dokumentacji platformy Azure o tworzeniu usługę podmiotu zabezpieczeń zobacz:
* [Tworzenie nazwy głównej usługi za pomocą programu PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Tworzenie nazwy głównej usługi przy użyciu wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [Tworzenie nazwy głównej usługi przy użyciu hello portalu Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>Opinia
Masz opinię, abyśmy o mapy usługi lub tej dokumentacji? Można znaleźć w naszych [strony User Voice](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), gdzie można sugeruje funkcje lub oddawać głosy na istniejące sugestie.
