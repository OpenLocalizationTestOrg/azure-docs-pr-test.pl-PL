---
title: Automatyzacja Azure jest aaaWhat | Dokumentacja firmy Microsoft
description: "Dowiedz się, jakie korzyści zapewnia usługi Automatyzacja Azure i uzyskać odpowiedzi toocommon pytania, dzięki czemu możesz rozpocząć pracę tworzeniu, przy użyciu elementów runbook i konfiguracja DSC automatyzacji Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "co to jest usługa automation, azure automation, przykłady usługi azure automation"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 1e5a90e272d6b2beb7b5007e2fea2c110dbd79b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-overview"></a>Omówienie usługi Azure Automation
Automatyzacji Microsoft Azure umożliwia użytkownikom tooautomate hello ręczne, długotrwałą podatne na błędy i często powtarzanych często wykonywane zadania w środowisku cloud i enterprise. Zaoszczędzić czas i zwiększa niezawodność hello regularnych zadań administracyjnych i nawet planuje je toobe automatycznie wykonywane w regularnych odstępach czasu. Można automatyzować procesy za pomocą elementów Runbook lub automatyzować zarządzanie konfiguracją za pomocą konfiguracji żądanego stanu. Ten artykuł zawiera krótkie omówienie usługi Azure Automation i odpowiedzi na często zadawane pytania. Aby uzyskać szczegółowe informacje na powitania różne tematy mogą odwoływać się tooother artykuły w tej bibliotece.

## <a name="automating-processes-with-runbooks"></a>Automatyzacja procesów przy użyciu elementów Runbook
Element Runbook to zestaw zadań wykonujących niektóre zautomatyzowane procesy w usłudze Azure Automation. Może być prosty proces, takie jak uruchamianie maszyny wirtualnej oraz utworzenie wpisu dziennika lub masz złożonego elementu runbook, który łączy inne mniejsze tooperform elementów runbook złożonym procesem w wielu zasobów lub nawet wielu chmury i lokalnych środowisk.  

Na przykład może być ręczne istniejący proces obcinanie bazy danych SQL, jeśli zbliża się maksymalny rozmiar, który obejmuje wiele kroków, takich jak serwer toohello łączący, łączenie toohello bazy danych, Pobierz hello bieżący rozmiar bazy danych, sprawdź, czy Próg przekroczyła obcięcia go i powiadamia użytkownika. Zamiast ręcznie wykonywać każdy z tych kroków, można utworzyć element Runbook, który umożliwi wykonanie wszystkich tych zadań w ramach pojedynczego procesu. Czy uruchomić elementu runbook hello, podaj hello wymagane informacje, takie jak nazwa serwera SQL hello, nazwa bazy danych i adresatów poczty e-mail i następnie znajdują się w trakcie hello proces zostanie zakończony. 

## <a name="what-can-runbooks-automate"></a>Co można automatyzować za pomocą elementów Runbook?
Elementy Runbook w usłudze Azure Automation są oparte na programie Windows PowerShell lub przepływie pracy programu Windows PowerShell, dlatego mogą wykonywać wszystkie czynności programu PowerShell. Jeśli aplikacja lub usługa ma interfejs API, element Runbook może z nim współpracować. Jeśli masz modułu programu PowerShell dla aplikacji hello można załadować tego modułu do automatyzacji Azure i zawierają te polecenia cmdlet w elemencie runbook. Elementy runbook automatyzacji Azure działają w hello chmury Azure i można uzyskać dostępu do żadnych zasobów w chmurze lub zasobów zewnętrznych, które są dostępne z chmury hello. Przy użyciu [hybrydowy proces roboczy elementu Runbook](automation-hybrid-runbook-worker.md), elementy runbook mogą działać w danych lokalnych zasobów lokalnych toomanage center. 

## <a name="getting-runbooks-from-hello-community"></a>Pobieranie elementów runbook z hello społeczności
Witaj [galerię elementów Runbook](automation-runbook-gallery.md#runbooks-in-runbook-gallery) zawiera elementy runbook z firmy Microsoft i hello społeczności, który można użyć bez zmian w Twoim środowisku lub dostosować je do własnych celów. Są one również przydatne tooas odwołania toolearn jak toocreate własnych elementów runbook. Można nawet współtworzyć galerii toohello własnych elementów runbook, że uważasz, że inni użytkownicy mogą być przydatne. 

## <a name="creating-runbooks-with-azure-automation"></a>Tworzenie elementów Runbook przy użyciu usługi Azure Automation
Możesz [tworzenia własnych elementów runbook](automation-creating-importing-runbook.md) z pliki tymczasowe lub modyfikowanie elementów runbook z hello [galerię elementów Runbook](http://msdn.microsoft.com/library/azure/dn781422.aspx) do własnych wymagań. Istnieją cztery [typy elementów Runbook](automation-runbook-types.md), które można wybierać w oparciu o własne wymagania oraz program PowerShell. Jeśli wolisz toowork bezpośrednio z hello kod programu PowerShell, a następnie można użyć [runbook programu PowerShell](automation-runbook-types.md#powershell-runbooks) lub [runbook przepływu pracy programu PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) edycji w trybie offline lub hello [edytor tekstowy](http://msdn.microsoft.com/library/azure/dn879137.aspx) w hello portalu Azure. Jeśli wolisz tooedit elementu runbook nie są widoczne toohello kodu źródłowego, a następnie można utworzyć [graficznym elementem runbook](automation-runbook-types.md#graphical-runbooks) przy użyciu hello [edytora graficznego usługi](automation-graphical-authoring-intro.md) w hello portalu Azure. 

Preferowane jest obserwowanie tooreading? Ma przyjrzeć się hello poniżej wideo z sesji Ignite firmy Microsoft w maja 2015 r. Uwaga: Hello pojęcia i funkcje omówione w tym wideo są poprawne, usługi Automatyzacja Azure zanotowano znacznie ponieważ zarejestrowano ten film, ma szerszej interfejsu użytkownika w portalu Azure hello i obsługuje dodatkowe funkcje.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a>Automatyzacja zarządzania konfiguracją za pomocą konfiguracji żądanego stanu
[DSC środowiska PowerShell](https://technet.microsoft.com/library/dn249912.aspx) to platforma zarządzania, która pozwala toomanage, wdrażać i egzekwować konfiguracji dla hostów fizycznych i maszyn wirtualnych za pomocą deklaratywne składni programu PowerShell. Konfiguracje można definiować na centralnym serwerze ściągania konfiguracji DSC, a maszyny docelowe mogą je pobierać i stosować. DSC udostępnia zestaw poleceń cmdlet programu PowerShell, można toomanage konfiguracji i zasobów.  

[Konfiguracja DSC usługi Azure Automation](automation-dsc-overview.md) to oparte na chmurze rozwiązanie dla konfiguracji PowerShell DSC, które świadczy usługi wymagane w środowiskach przedsiębiorstw.  Możesz zarządzać zasobami usługi Konfiguracja DSC automatyzacji Azure i zastosować toovirtual konfiguracje lub komputerów fizycznych, które je odzyskać z serwera ściągania usługi Konfiguracja DSC w hello chmury Azure.  Rozwiązanie to udostępnia również usługi raportowania, które informują Cię o ważnych zdarzeniach, takich jak odchylenie węzłów od ich przypisanej konfiguracji lub zastosowanie nowej konfiguracji. 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a>Tworzenie własnych konfiguracji DSC przy użyciu funkcji Azure Automation
[Konfiguracji DSC](automation-dsc-overview.md) Określ stan hello żądanego węzła.  Można zastosować wiele węzłów hello tego samego tooassure konfiguracji wszystkich zachowanie stanu identyczne.  Konfigurację można utworzyć przy użyciu dowolnego edytora tekstów na komputerze lokalnym, a następnie zaimportować ją do usługi Azure Automation w celu jej skompilowania i zastosowania w węzłach.

## <a name="getting-modules-and-configurations"></a>Pobieranie modułów i konfiguracji
Możesz uzyskać [moduły programu PowerShell](automation-runbook-gallery.md#modules-in-powershell-gallery) zawierający polecenia cmdlet, których można użyć w elementach runbook i konfiguracji DSC z hello [galerii programu PowerShell](http://www.powershellgallery.com/). Można uruchomić tej galerii z hello portalu Azure i zaimportuj moduły bezpośrednio do usługi Automatyzacja Azure, lub możesz pobrać i zaimportować je ręcznie. Nie można zainstalować moduły hello bezpośrednio z hello portalu Azure, ale można je pobrać je zainstalować, jak w przypadku innych modułów. 

## <a name="example-practical-applications-of-azure-automation"></a>Przykłady praktycznych zastosowań usługi Azure Automation
Poniżej przedstawiono kilka przykładów co to są hello rodzaje scenariuszach automatyzacji w usłudze Automatyzacja Azure. 

* Tworzenie i kopiowanie maszyn wirtualnych w ramach różnych subskrypcji platformy Azure. 
* Planowanie kopii plików z kontenera magazynu obiektów Blob Azure tooan komputera lokalnego. 
* Automatyzowanie funkcji zabezpieczeń, takich jak odrzucanie żądań od klientów po wykryciu ataku typu „odmowa usługi”. 
* Sprawdzanie, czy maszyny działają zgodnie ze skonfigurowanymi zasadami zabezpieczeń.
* Zarządzanie ciągłym wdrażaniem kodu aplikacji w chmurze i infrastrukturze lokalnej. 
* Kompilowanie lasu usługi Active Directory na platformie Azure na potrzeby środowiska laboratoryjnego. 
* Obcinanie tabeli w bazie danych SQL, jeśli rozmiar bazy danych zbliża się do wartości maksymalnej. 
* Zdalne aktualizowanie ustawień środowiska dla witryny sieci Web platformy Azure. 

## <a name="how-does-azure-automation-relate-tooother-automation-tools"></a>Jak usługi Automatyzacja Azure między narzędziami automatyzacji tooother?
[Usługa zarządzania Strukturę automatyzacja](http://technet.microsoft.com/library/dn469260.aspx) jest zamierzone tooautomate zadań zarządzania w chmurze prywatnej hello. Jest ona instalowana lokalnie w centrum danych klienta jako składnik [pakietu Microsoft Azure Pack](https://www.microsoft.com/en-us/server-cloud/). SMA i automatyzacja Azure używają hello tego samego formatu elementu runbook na podstawie środowiska Windows PowerShell i przepływ pracy programu Windows PowerShell, ale nie obsługuje SMA [graficznych elementów runbook](automation-graphical-authoring-intro.md).  

Program [System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) jest przeznaczony do automatyzacji zasobów lokalnych. Go w formacie runbook innego niż Azure Automation i Service Management Automation i ma interfejsu graficznego toocreate runbook bez pisania skryptów. Jego elementy Runbook składają się z działań z pakietów integracyjnych napisanych specjalnie dla programu Orchestrator. 

## <a name="where-can-i-get-more-information"></a>Gdzie można uzyskać więcej informacji?
Zawiera różne zasoby są dostępne dla możesz toolearn więcej informacji na temat usługi Automatyzacja Azure i tworzenia własnych elementów runbook. 

* **Biblioteka usługi Azure Automation** to miejsce, w którym znajdujesz się w tej chwili. Witaj artykuły w tej bibliotece Podaj pełną dokumentację hello konfiguracji i administracji usługi Automatyzacja Azure oraz do tworzenia własnych elementów runbook. 
* [Polecenia cmdlet programu Azure PowerShell](http://msdn.microsoft.com/library/jj156055.aspx) oferują informacje wymagane do automatyzacji operacji platformy Azure wykonywanych za pomocą programu Windows PowerShell. Elementy Runbook za pomocą tych poleceń cmdlet toowork zasobów platformy Azure. 
* [Blog zarządzania](https://azure.microsoft.com/blog/tag/azure-automation/) zawiera hello najnowsze informacje dotyczące automatyzacji Azure i inne technologie zarządzania firmy Microsoft. Najnowsza wersja toostay blogu toothis się toodate z hello powinien subskrypcji hello przez zespół usługi Automatyzacja Azure. 
* [Forum automatyzacji](http://go.microsoft.com/fwlink/p/?LinkId=390561) pozwala toopost pytania dotyczące usługi Automatyzacja Azure toobe adresowane przez firmę Microsoft i hello społeczności automatyzacji. 
* [Polecenia cmdlet usługi Azure Automation](https://msdn.microsoft.com/library/mt244122.aspx) oferują informacje dotyczące automatyzacji zadań administracyjnych. Zawiera ona kont automatyzacji toomanage poleceń cmdlet, zasoby, elementy runbook, DSC.

## <a name="can-i-provide-feedback"></a>Czy mogę przekazać opinię?
**Przekaż nam swoją opinię.** Jeśli szukasz rozwiązania dotyczącego elementów Runbook usługi Azure Automation lub modułu integracji, opublikuj żądanie skryptu w Centrum skryptów. Jeśli chcesz przekazać opinię na temat żądań funkcji usługi Azure Automation, opublikuj ją w witrynie [User Voice](http://feedback.windowsazure.com/forums/34192--general-feedback). Dziękujemy. 

