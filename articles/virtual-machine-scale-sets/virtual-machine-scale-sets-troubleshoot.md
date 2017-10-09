---
title: "aaaTroubleshoot automatycznie skalowana za pomocą zestawów skali maszyny wirtualnej | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z automatycznie skalowana za pomocą zestawów skali maszyny wirtualnej. Zrozumienie typowych problemów i w jaki sposób tooresolve je."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
ms.openlocfilehash: 4c9a70992348d87fb43646421a90a027bf400a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>Rozwiązywanie problemów z automatycznie skalowana za pomocą zestawów skali maszyny wirtualnej
**Problem** — po utworzeniu Skalowanie automatyczne infrastruktury w usłudze Azure Resource Manager przy użyciu zestawy skalowania maszyny Wirtualnej — na przykład, przez wdrożenie szablonu następująco: https://github.com/Azure/azure-quickstart-templates/tree/master/201- vmss-bottle — funkcja automatycznego skalowania — masz zdefiniowanych reguł skalowania i działa ona ponosić, z tą różnicą, że niezależnie od tego, ile obciążenia zostanie umieszczony na powitania maszyn wirtualnych, nie będzie skalowania automatycznego.

## <a name="troubleshooting-steps"></a>Kroki rozwiązywania problemów
Niektóre elementy tooconsider obejmują:

* Liczby rdzeni każda maszyna wirtualna ma i czy ładowanie każdego rdzenia? Szablon Szybki Start Azure przykład Hello powyżej ma do_work.php skrypt, który jest ładowany przez pojedynczy rdzeń. Jeśli używasz większy niż pojedynczego rdzenia rozmiar maszyny Wirtualnej maszyny Wirtualnej, tak jak Standard_A1 lub D1 następnie wymagałoby toorun obciążenie wiele razy. Sprawdź, ile rdzenie maszyn wirtualnych, przeglądając [rozmiary dla systemu Windows maszyny wirtualne na platformie Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Jak wiele maszyn wirtualnych w hello zestawu skali maszyny Wirtualnej można operacji pracy na każdej z nich?
  
    Skalowania zdarzeń ma miejsce tylko po hello średni procesora CPU przez **wszystkie** hello wartości progowej, wraz z upływem czasu hello wewnętrzny zdefiniowane w regułach skalowania automatycznego hello przekracza hello maszyn wirtualnych w zestawie skalowania.
* Czy zapomniano wszelkie zdarzenia skalowania?
  
    Przejrzyj dzienniki inspekcji hello w hello portalu Azure zdarzeń skali. Może być wystąpił skali górę i skalowania w dół, która została pominięta. Można filtrować według "Skala"...
  
    ![Dzienniki inspekcji][audit]
* Wartości progowe w skali i skalowalnego w poziomie są różni się wystarczająco?
  
    Załóżmy, że ustawić reguły tooscale się, gdy średnie wykorzystanie Procesora jest większa niż 50% ponad 5 minut, a tooscale w przypadku średnie wykorzystanie Procesora na mniej niż 50%. To spowodowałoby problem "flapping" gdy wykorzystanie Procesora jest próg Zamknij toothis akcji skalowania hello stale zwiększania i zmniejszania rozmiaru hello zestawu. W związku z tym hello automatycznego skalowania usługi próbuje tooprevent "niestabilny", który można manifestu jako skalowania nie. W związku z tym upewnij się, że wartości progowe skalowalnego w poziomie i w skali są różni się wystarczająco tooallow Zwolnij miejsce Between skalowania.
* Czy pisania szablonu JSON?
  
    Jest łatwe toomake błędów, więc uruchomić przy użyciu szablonu, takie jak hello jest jeden nad którym sprawdzone toowork i małych zmiany przyrostowe. 
* Można ręcznie skalowanie przychodzący lub wychodzący?
  
    Spróbuj ręcznie hello ponownego wdrożenia zasobów zestawu skali maszyny Wirtualnej z różnych "pojemność" ustawienie toochange hello wiele maszyn wirtualnych. Przykład toodo szablonu jest tutaj: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing — może być konieczne tooedit hello szablonu toomake się, że ma ona hello sam rozmiar komputera jest korzystania z zestawu skalowania. Czy można pomyślnie ręcznie zmienić hello liczbę maszyn wirtualnych, następnie wiadomo, że hello problem jest tooautoscale izolowanym.
* Sprawdź Twojej Microsoft.Compute/virtualMachineScaleSet i zasoby elemencie Microsoft.Insights hello [Eksploratora zasobów Azure](https://resources.azure.com/)
  
    Jest to nieodzowne Rozwiązywanie problemów z narzędzia, które pokazuje hello stanu zasobów usługi Azure Resource Manager. Kliknij subskrypcję i przyjrzyj się hello są Rozwiązywanie problemów z grupy zasobów. W obszarze dostawcy zasobów obliczeniowych hello przyjrzeć się hello tworzenia zestawu skali maszyny Wirtualnej i sprawdź hello wystąpienia widoku, który pokazuje hello stanu wdrożenia. Sprawdź również hello widok wystąpienia maszyny wirtualnej w hello zestawu skali maszyny Wirtualnej. Następnie przejdź do dostawcy zasobów w elemencie Microsoft.Insights hello i sprawdź, czy wygląd hello reguł skalowania automatycznego.
* Jest hello diagnostycznych rozszerzenia pracy i wysyłających dane dotyczące wydajności?
  
    **Aktualizacja:** Azure automatycznego skalowania zostało ulepszone toouse hosta na podstawie metryk potoku, który nie wymaga już toobe rozszerzenia diagnostyki, zainstalowane. Oznacza to, że hello kilku następnych akapitów nie mają już zastosowania w przypadku utworzenia aplikacji Skalowanie automatyczne przy użyciu hello nowy potok. Na przykład szablonów platformy Azure, które zostały przekonwertowane toouse hello hosta potoku: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale. 
  
    Przy użyciu hosta na podstawie metryki skalowania automatycznego jest lepszym rozwiązaniem dla hello z następujących powodów:
  
  * Mniej części ruchome jako rozszerzenia nie diagnostyki muszą toobe zainstalowane.
  * Szablony prostsze. Wystarczy dodać insights skalowania automatycznego reguły tooan istniejącego zestawu skalowania maszyny wirtualnej szablonu.
  * Bardziej niezawodne, raportowanie i szybsze uruchamianie nowych maszyn wirtualnych.
    
    Hello tylko przyczyn może być tookeep przy użyciu rozszerzenia diagnostycznych może być konieczne będzie pamięci diagnostyki raportowania/skalowania. Host, na podstawie metryk nie raportują pamięci.
    
    Z tym pamiętać tylko wykonaj hello dalszej części tego artykułu, nadal używasz rozszerzenia diagnostycznych dla Twojego Skalowanie automatyczne.
    
    Funkcja automatycznego skalowania usługi Azure Resource Manager można pracować (ale nie ma już do) za pomocą rozszerzenia maszyny Wirtualnej o nazwie hello rozszerzenia diagnostyki. Konto magazynu tooa danych wydajności, zdefiniowanych w szablonie hello go emituje. Te dane są agregowane przez usługę Azure Monitor hello.
    
    Jeśli hello usługa szczegółowych informacji nie można odczytać danych z hello maszyn wirtualnych, powinien toosend Ci wiadomość e-mail — na przykład jeśli zostały hello maszyn wirtualnych, więc Sprawdź pocztę (hello określona podczas tworzenia hello konto platformy Azure).
    
    Można również przejść i wyglądać na powitania danych. Spójrz na powitania kontem magazynu platformy Azure przy użyciu Eksplorator chmury. Na przykład za pomocą hello [programu Visual Studio Cloud Explorer](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2), zaloguj się za wybierz hello używasz subskrypcji platformy Azure i hello nazwa odwołuje hello definicji rozszerzenia diagnostyki w danym wdrożeniu konto magazynu diagnostyki szablon...
    
    ![Eksplorator chmury][explorer]
    
    W tym miejscu zobaczysz grupy tabel, gdzie są przechowywane dane hello z każdej maszyny Wirtualnej. Biorąc systemu Linux i hello Metryka procesora CPU, na przykład, przyjrzeć się hello najnowszych wierszy. Hello Visual Studio cloud explorer obsługuje język zapytań, więc można uruchomić zapytania, takie jak "datetime gt sygnatura czasowa" 2016-02-02T21:20:00Z "" toomake się pobrać najnowszych zdarzeń hello (przyjmowane jest czas jest w formacie UTC). Witaj dane, które widać w odpowiada toohello skalowany reguł skonfigurowanych? W poniższym przykładzie hello hello Procesora dla maszyny 20 uruchomiona zwiększyć too100% hello ostatnich 5 minut.
    
    ![Magazyn tabel][tables]
    
    W przypadku hello danych nie istnieje, następnie zakłada się, że hello problem jest rozszerzeniem diagnostycznych hello uruchomionych w hello maszyn wirtualnych. Jeśli istnieje już hello danych, oznacza to, brak problemami z reguł skalowania lub usłudze Insights hello. Sprawdź [Azure stan](https://azure.microsoft.com/status/).
    
    Po już został tych kroków, jeśli nadal występują problemy z automatycznego skalowania można wypróbować fora hello na [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp), lub [przepełnienie stosu](http://stackoverflow.com/questions/tagged/azure), lub pomocy technicznej. Można przygotować tooshare hello szablon i widoku hello danych dotyczących wydajności.

[audit]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png
