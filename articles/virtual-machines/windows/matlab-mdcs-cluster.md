---
title: "aaaMATLAB klastrów na maszynach wirtualnych | Dokumentacja firmy Microsoft"
description: "Użyj toocreate maszyny wirtualne Microsoft Azure toorun klastrów serwera przetwarzania danych rozproszonych MATLAB obciążeń obliczeniowych równoległych MATLAB"
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>Tworzenie klastrów serwera przetwarzania danych rozproszonych MATLAB na maszynach wirtualnych Azure
Użyj wirtualnych Microsoft Azure maszyn toocreate jedną lub klastry serwerów obliczeniowych więcej rozproszonych MATLAB toorun obciążeń obliczeniowych równoległych MATLAB. Zainstaluj oprogramowanie serwera przetwarzania danych rozproszonych MATLAB na toouse maszyny Wirtualnej, jako obrazu podstawowego i przy użyciu szablonu Azure szybkiego startu skryptu programu Azure PowerShell (dostępne na [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy hello klaster i nim zarządzać. Po wdrożeniu połączyć toorun klastra toohello obciążeń.

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>Temat MATLAB i MATLAB rozproszonego przetwarzania danych serwera
Witaj [MATLAB](http://www.mathworks.com/products/matlab/) platformy jest zoptymalizowany do rozwiązywania problemów inżynieryjne i naukowe. MATLAB symulacje na dużą skalę i zadań przetwarzania danych Umożliwia równoległe MathWorks obliczeniowych toospeed produktów zapasowej ich obciążeń obliczeniowych dzięki wykorzystaniu klastrów obliczeniowych oraz usług siatki. [Równoległe przetwarzanie przybornika](http://www.mathworks.com/products/parallel-computing/) umożliwia użytkownikom MATLAB parallelize aplikacji i skorzystać z wielordzeniowych procesorów GPU i klastrów obliczeniowych. [Serwer przetwarzania danych rozproszonych MATLAB](http://www.mathworks.com/products/distriben/) umożliwia MATLAB tooutilize użytkowników z wielu komputerów w klastrze obliczeniowym.

Przy użyciu maszyn wirtualnych platformy Azure, można utworzyć klastry serwerów rozproszonych obliczeniowych MATLAB, których wszystkie hello mechanizmów dostępne toosubmit równoległych służbowe jako klastry lokalnych, takich jak interakcyjne zadania, zadania wsadowe, niezależnie od zadania i Komunikacja zadania. Za pomocą platformy Azure w połączeniu z platformą MATLAB hello ma wiele zalet w porównaniu tooprovisioning i przy użyciu tradycyjnych lokalnymi sprzętu: rozmiary zakres maszyny wirtualnej, tworzenie klastrów na żądanie, więc płacisz tylko za zasoby obliczeniowe hello używasz, i modele tootest możliwości Hello na dużą skalę.  

## <a name="prerequisites"></a>Wymagania wstępne
* **Komputer kliencki** — po wdrożeniu należy toocommunicate komputerów klienckich z systemem Windows, z platformy Azure i hello MATLAB rozproszonego przetwarzania danych klastra.
* **Program Azure PowerShell** — zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) tooinstall go na komputerze klienckim.
* **Subskrypcja platformy Azure** — Jeśli nie masz subskrypcji, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut. W przypadku dużych klastrów rozważ z subskrypcji lub inne opcje zakupu.
* **Limit przydziału rdzeni** — może być konieczne toodeploy przydziału rdzeni hello tooincrease dużych klastra lub więcej niż jednym klastrze MATLAB rozproszonego przetwarzania danych serwera. limit przydziału, tooincrease [otwarcia żądania pomocy technicznej online klienta](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) bez dodatkowych opłat.
* **Licencje MATLAB, przybornika przetwarzanie równoległe i serwera przetwarzania danych rozproszonych MATLAB** — skrypty hello założono, że hello [MathWorks hostowanej License Manager](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) jest używany dla wszystkich licencji.  
* **Oprogramowanie serwera przetwarzania rozproszonego MATLAB** — zostanie zainstalowana na maszynie Wirtualnej, która będzie służyć jako podstawowy obraz maszyny Wirtualnej hello hello klastrowania maszyn wirtualnych.

## <a name="high-level-steps"></a>Wysokiego poziomu kroków
toouse wirtualnej Azure maszyny dla klastrów serwerów rozproszonych obliczeniowych MATLAB hello następujące ogólne kroki są wymagane. Szczegółowe instrukcje znajdują się w dokumentacji hello towarzyszące hello szybkiego startu szablon oraz skrypty na [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster).

1. **Tworzenie obrazu maszyny Wirtualnej**  

   * Pobierz i zainstaluj oprogramowanie serwera przetwarzania danych rozproszonych MATLAB na tej maszyny Wirtualnej.

     > [!NOTE]
     > Ten proces może potrwać kilka godzin, ale masz tylko toodo go po dla każdej wersji MATLAB używasz.   
     >
     >
2. **Utwórz co najmniej jeden klaster**  

   * Użyj skryptu PowerShell dostarczane hello lub toocreate szablon szybkiego startu hello klastra z hello podstawowy obraz maszyny Wirtualnej.   
   * Zarządzanie klastrami hello za pomocą skryptu PowerShell hello dostarczane, co pozwala toolist, wstrzymywanie, wznawianie i usuwania klastrów.

## <a name="cluster-configurations"></a>Konfiguracje klastrów
Obecnie skryptu tworzenia klastra hello i szablon pozwalają toocreate pojedynczego topologii MATLAB rozproszonego przetwarzania danych serwera. Należy utworzyć co najmniej jeden klaster dodatkowe z każdym klastrze mających różne liczby procesu roboczego maszyny wirtualne, przy użyciu różnych rozmiarów maszyn wirtualnych i tak dalej.

### <a name="matlab-client-and-cluster-in-azure"></a>MATLAB klienta i klaster na platformie Azure
Rysunek Hello MATLAB klienta węzła, węzeł MATLAB harmonogramu zadań i MATLAB komputerowe serwera rozproszonych "pracownik" węzły są wszystkie skonfigurowane jako maszynach wirtualnych platformy Azure w sieci wirtualnej, jak pokazano poniżej hello.


* Witaj toouse klastra, Połącz przez węzeł klienta toohello pulpitu zdalnego. Węzeł Klient Hello uruchamia hello MATLAB klienta.
* powitania klienta węzeł ma udziału plików, które są dostępne dla wszystkich pracowników.
* Menedżer licencji hostowanej MathWorks służy do hello kontroli licencji oprogramowania MATLAB.
* Domyślnie jednego serwera przetwarzania danych rozproszonych MATLAB procesu roboczego na podstawowe zostało utworzone w wątku roboczym hello maszyn wirtualnych, ale można określić dowolną liczbę.

## <a name="use-an-azure-based-cluster"></a>Używanie klastra bazujących na platformie Azure
Podobnie jak w przypadku innych typów klastrów serwerów rozproszonych obliczeniowych MATLAB należy toouse hello menedżera profilu klastra w hello MATLAB klienta (na powitania klienta maszyny Wirtualnej) toocreate profilu klastra MATLAB harmonogramu zadań.

![Menedżer profilu klastra](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać szczegółowe instrukcje toodeploy i zarządzania klastrami serwerów rozproszonych obliczeniowych MATLAB na platformie Azure, zobacz hello [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) repozytorium zawierający szablony hello i skryptów.
* Przejdź toohello [lokacji MathWorks](http://www.mathworks.com/) szczegółowa dokumentacja MATLAB i MATLAB rozproszonego przetwarzania danych serwera.
