---
title: "wyniki aaaPersist lub dzienniki ukończone zadań i zadań, danych tooa store - partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o różnych opcjach trwałych danych wyjściowych z zadań i zadań wsadowych. Można ją utrwalić danych tooAzure magazynu lub tooanother przechowywania."
services: batch
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0b11e387f1694e1ce3e9573db7f6013f0154cad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-output"></a>Utrwalanie danych wyjściowych zadań i zadań podrzędnych

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Typowe przykłady dane wyjściowe zadania obejmują:

- Pliki utworzone podczas procesów zadań hello dane wejściowe.
- Pliki dziennika związane z wykonywania zadania. 

W tym artykule opisano różne opcje utrwalanie zadań dane wyjściowe hello scenariuszy i dla których jest najbardziej odpowiednia każdej opcji.   

## <a name="about-hello-batch-file-conventions-standard"></a>Temat hello standardowych konwencji pliku wsadowego

Wsadowe definiuje opcjonalny zestaw konwencji nazewnictwa plików dane wyjściowe zadania w usłudze Azure Storage. Witaj [standard konwencje pliku wsadowego](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) zawiera opis tych konwencji. standard konwencje plików Hello określa nazwy hello hello i kontener obiektów blob ścieżkę docelową w usłudze Azure Storage dla pliku wyjściowego danego na podstawie nazw hello hello zadań i zadań.

Jest zapasowej tooyou czy zdecydujesz hello toouse konwencje plików standard nazewnictwa plików danych wyjściowych. Jednak chcesz, można nazwać hello docelowy kontener i obiektów blob. Jeśli należy używać hello konwencje plików standard nazewnictwa plików wyjściowych, a następnie Twoje pliki wyjściowe są dostępne do wyświetlenia w hello [portalu Azure][portal].

Istnieje kilka sposobów użyć standardowego pliku konwencje hello:

- Jeśli używane są pliki wyjściowe toopersist hello partii usługi interfejsu API, można wybrać tooname docelowego kontenerów i obiektów blob, zgodnie z toohello konwencje plików standardowych. Hello interfejsu API usługi partii pozwala toopersist pliki wyjściowe z kodu klienta bez modyfikowania aplikacji zadań.
- Jeśli tworzysz .NET, możesz użyć hello [biblioteki konwencje plików usługi partia zadań Azure dla platformy .NET][nuget_package]. Zaletą tej biblioteki jest on obsługuje badania plików wyjściowych według Identyfikatora tootheir lub cel. wbudowanej funkcji podczas badania Hello umożliwia łatwe tooaccess pliki wyjściowe z aplikacji klienckiej lub innych zadań. Jednak zadanie aplikacji musi być toocall zmodyfikowanego pliku konwencje biblioteki. Aby uzyskać więcej informacji, zobacz hello odwołania dla hello [konwencje plików biblioteki dla platformy .NET](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.aspx).
- Jeśli tworzysz języka innego niż .NET, można zaimplementować hello konwencje plików standardowe w aplikacji.

## <a name="design-considerations-for-persisting-output"></a>Zagadnienia dotyczące projektowania dla trwałych danych wyjściowych 

Podczas projektowania rozwiązania partii, należy wziąć pod uwagę hello następujące czynniki pokrewne toojob oraz wyniki zadań.

* **Okres istnienia węzła obliczeniowe**: obliczeniowe są często przejściowe, szczególnie w pule włączona funkcja automatycznego skalowania. Dane wyjściowe zadania w węźle jest dostępna tylko wtedy, gdy węzeł hello istnieje, i tylko w okresie przechowywania pliku hello ustawiono hello zadania. Jeśli zadanie generuje dane wyjściowe, które mogą być wymagane po ukończeniu zadania hello, hello zadań należy przesłać jego dane wyjściowe pliki tooa trwałego magazynu takie jak magazyn Azure.

* **Dane wyjściowe magazynu**: Magazyn Azure jest zalecane jako dane wyjściowe zadania w magazynie danych, ale można użyć dowolnego magazynu trwałego. Zapisywanie tooAzure dane wyjściowe zadania magazynu jest zintegrowany hello interfejsu API usługi partii. Jeśli używasz innej formy trwałego magazynu, musisz toowrite hello aplikacji logiki toopersist danych wyjściowych zadania w sobie.   

* **Dane wyjściowe pobierania**: Jeśli utrwalonych danych wyjściowych zadania można pobrać dane wyjściowe zadania bezpośrednio z hello węzłów obliczeniowych w puli lub usługi Azure Storage lub innym magazynie danych. tooretrieve zadania wyjściowy bezpośrednio w węźle obliczeń, potrzebujesz hello nazwę pliku i jego lokalizacji danych wyjściowych w węźle hello. Jeśli będzie się powtarzać tooAzure dane wyjściowe zadania magazynu, należy hello Pełna ścieżka toohello pliku w pliki wyjściowe hello toodownload usługi Azure Storage z hello zestawu SDK usługi Magazyn Azure.

* **Wyświetlanie danych wyjściowych**: po przejściu tooa zadanie wsadowe w hello Azure portalu i wybierz pozycję **pliki w węźle**, wyświetlane są wszystkie pliki skojarzone z zadaniem hello, nie tylko hello interesuje Cię plików wyjściowych. Ponownie plików w węzłach obliczeniowych są dostępne tylko wtedy, gdy istnieje węzeł hello i tylko w obrębie czas przechowywania pliku hello ustawiono hello zadania. zadanie tooview danych wyjściowych, że zostały utrwalone tooAzure magazynu, możesz użyć hello portalu Azure lub aplikację klienta usługi Azure Storage, takich jak hello [Eksploratora usługi Storage Azure][storage_explorer]. tooview output danych w usłudze Azure Storage za pomocą portalu hello lub innego narzędzia, należy znać lokalizacji pliku hello i przejść bezpośrednio tooit.

## <a name="options-for-persisting-output"></a>Opcje dla trwałych danych wyjściowych

W zależności od scenariusza istnieje kilka różne podejścia może zająć toopersist dane wyjściowe z zadania:

- Użyj interfejsu API usługi partii hello.  
- Użyj hello konwencje pliku wsadowego biblioteki dla platformy .NET.  
- Implementuje hello konwencje pliku wsadowego standardowe w aplikacji.
- Implementacji niestandardowego pliku rozwiązania przepływu.

Witaj następujące sekcje opisują każde podejście bardziej szczegółowo.

### <a name="use-hello-batch-service-api"></a>Za pomocą interfejsu API usługi partii hello

Wersją 2017-05-01 hello usługa partia zadań dodaje obsługę określanie plików wyjściowych w usłudze Azure Storage dla danych zadań podczas możesz [dodać zadania tooa zadań](https://docs.microsoft.com/rest/api/batchservice/add-a-task-to-a-job) lub [dodania kolekcji zadań tooa zadania](https://docs.microsoft.com/rest/api/batchservice/add-a-collection-of-tasks-to-a-job).

Witaj interfejsu API partii usługi obsługuje trwałych tooan danych zadania konta magazynu Azure z zestawów utworzonych za pomocą hello konfiguracji maszyny wirtualnej. Z hello interfejsu API usługi partii można ją utrwalić danych zadania bez modyfikowania aplikacji hello, która uruchamia zadania. Można opcjonalnie stosować toohello [standard konwencje pliku wsadowego](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) nazewnictwa plików hello, który można utrwalić tooAzure magazynu. 

Użyj hello interfejsu API usługi partii zadań toopersist dane wyjściowe po:

- Chcesz, aby dane toopersist z partii zadań i zadania Menedżer zadania w pulach utworzone za pomocą hello konfiguracji maszyny wirtualnej.
- Chcesz kontenera magazynu Azure tooan toopersist danych za pomocą dowolnego nazwy.
- Ma toopersist danych tooan kontenera magazynu Azure o nazwie zgodnie z toohello [standard konwencje pliku wsadowego](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

> [!NOTE]
> Hello interfejsu API usługi partii nie obsługuje trwałych danych z zadań uruchomionych w pulach utworzone z konfiguracją usługi w chmurze hello. Dla informacji o zadaniu utrwalanie dane wyjściowe z systemem konfiguracji usługi w chmurze hello pule, zobacz [utrwalić i zadań tooAzure danych magazynu z biblioteki konwencje pliku wsadowego hello .NET toopersist](batch-task-output-file-conventions.md)
> 
> 

Aby uzyskać więcej informacji na trwałych danych wyjściowych zadania z hello interfejsu API partii usługi, zobacz [utrwalić tooAzure danych zadań magazynu z hello interfejsu API usługi partii](batch-task-output-files.md). Zobacz też hello [PersistOutputs] [github_persistoutputs] przykładowy projekt w witrynie GitHub, który demonstruje sposób biblioteki klienta toouse hello partii zadań dla zadania toopersist .NET output toodurable magazynu.

### <a name="use-hello-batch-file-conventions-library-for-net"></a>Użyj hello konwencje pliku wsadowego biblioteki dla platformy .NET

Deweloperzy tworzenia rozwiązań partii z C# i .NET mogą używać hello [konwencje plików biblioteki dla platformy .NET] [ nuget_package] tooan danych zadań toopersist konta magazynu Azure, zgodnie z toohello [pliku wsadowego Konwencje standardowych](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Biblioteka konwencje plików Hello obsługuje przenoszenie danych wyjściowych tooAzure pliki magazynu i nazewnictwa docelowego kontenerów i obiektów blob w dobrze znanego sposób.

je bez konieczności hello Hello badania plików wyjściowych według Identyfikatora lub cel obsługuje biblioteki konwencje plików, dzięki czemu można łatwo toolocate zakończenie pliku identyfikatorów URI. 

Użyj biblioteki konwencje pliku wsadowego hello zadania toopersist .NET dane wyjściowe po:

- Podczas zadania hello jest nadal uruchomiona, które mają toostream tooAzure danych magazynu.
- Chcesz, aby dane toopersist z zestawów utworzonych za pomocą konfiguracji usługi w chmurze hello lub hello konfiguracji maszyny wirtualnej.
- Aplikacja kliencka lub innych zadań w hello zadania toolocate potrzeb, a pliki wyjściowe zadań za pomocą Identyfikatora lub w celu pobrania. 
- Ma tooperform wskazanie wyboru lub wczesne przekazywania początkowe wyniki.
- Ma tooview dane wyjściowe zadania w hello portalu Azure.

Aby uzyskać więcej informacji na trwałych danych wyjściowych zadania z hello konwencje plików biblioteki dla platformy .NET, zobacz [utrwalić i zadań tooAzure danych magazynu z biblioteki konwencje pliku wsadowego hello .NET toopersist ](batch-task-output-file-conventions.md). Zobacz też hello [PersistOutputs] [github_persistoutputs] przykładowy projekt w witrynie GitHub, który demonstruje sposób toouse hello konwencje plików biblioteki .NET toopersist zadania output toodurable magazynu.

Witaj [PersistOutputs] [github_persistoutputs] przykładowy projekt w witrynie GitHub pokazuje, jak biblioteki klienta toouse hello partii zadań dla zadania toopersist .NET output toodurable magazynu.

### <a name="implement-hello-batch-file-conventions-standard"></a>Implementowanie hello standardowych konwencji pliku wsadowego

Jeśli używasz języka innego niż .NET można zaimplementować hello [standard konwencje pliku wsadowego](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) w swojej aplikacji. 

Możesz hello tooimplement pliku konwencje nazewnictwa samodzielnie ma sprawdzonych schemat nazewnictwa, lub utworzyć tooview dane wyjściowe zadania w hello portalu Azure.

### <a name="implement-a-custom-file-movement-solution"></a>Implementacji niestandardowego pliku rozwiązania przepływu

Można też wdrożyć własne rozwiązania przeniesienia całego pliku. Użyj tego podejścia, gdy:

- Ma toopersist zadań danych tooa magazynu danych innego niż Azure Storage. tooupload pliki tooa magazyn danych Azure SQL lub danych Azure, można utworzyć niestandardowego skryptu lub pliku wykonywalnego tooupload toothat lokalizacji. Można następnie wywołać ją w wierszu polecenia powitania po uruchomieniu podstawowego pliku wykonywalnego. Na przykład w węźle systemu Windows, należy wywołać następujące dwa polecenia:`doMyWork.exe && uploadMyFilesToSql.exe`
- Ma tooperform wskazanie wyboru lub wczesne przekazywania początkowe wyniki.
- Ma toomaintain szczegółową kontrolę nad obsługi błędów. Na przykład można tooimplement własne rozwiązania, jeśli chcesz toouse zadań zależności akcje tootake niektórych Przekaż akcji na podstawie kodów zakończenia określonego zadania. Aby uzyskać więcej informacji na akcje zależności zadań, zobacz [utworzyć zależności zadań toorun zadania, które są zależne od innych zadań](batch-task-dependencies.md). 

## <a name="next-steps"></a>Następne kroki

- Eksplorowania przy użyciu nowych funkcji hello w danych zadań toopersist hello interfejsu API usługi partii w [utrwalić tooAzure danych zadań magazynu z hello interfejsu API usługi partii](batch-task-output-files.md).
- Informacje o używaniu biblioteki konwencje pliku wsadowego powitania dla platformy .NET w [utrwalić i zadań tooAzure danych magazynu z biblioteki konwencje pliku wsadowego hello .NET toopersist ](batch-task-output-file-conventions.md).
- Zobacz hello [PersistOutputs] [github_persistoutputs] przykładowy projekt w witrynie GitHub, który demonstruje sposób toouse zarówno hello biblioteki klienta usługi partia zadań dla platformy .NET i hello konwencje plików biblioteki .NET toopersist zadania output toodurable magazynu.

[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/
