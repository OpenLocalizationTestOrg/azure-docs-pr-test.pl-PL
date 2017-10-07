---
title: "rozwiązania aaaUse narzędzia i interfejsy API usługi partia zadań Azure toodevelop na dużą skalę przetwarzanie równoległe | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello interfejsów API i narzędzia dostępne związane z opracowywaniem rozwiązań z usługi partia zadań Azure hello."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: tamram
ms.openlocfilehash: ca75a1a63b3e7e6b0805e79a63685bc49aaaca8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-batch-apis-and-tools"></a>Omówienie narzędzi i interfejsów API usługi Batch

Przetwarzanie równoległe obciążeń z partii zadań Azure jest zazwyczaj wykonywane programowo przy użyciu jednej z hello [API partii](#batch-development-apis). Klient aplikacji lub usługi za pomocą toocommunicate API partii hello hello usługa partia zadań. Z hello interfejsów API partii, można tworzyć i Zarządzaj pulami węzłów obliczeniowych maszyn wirtualnych lub usługi w chmurze. Następnie można zaplanować toorun zadań i zadań na tych węzłach. 

Można efektywnie przetwarzania dużych obciążeń dla Twojej organizacji lub zapewnia usługi frontonu tooyour klientów, dzięki czemu mogą uruchamiać zadań i zadań, na żądanie lub według harmonogramu--na jeden, setek lub nawet tysiące węzłów. Usługę Azure Batch można także używać w ramach większego przepływu pracy zarządzanego za pomocą takich narzędzi, jak usługa [Azure Data Factory](../data-factory/data-factory-data-processing-using-batch.md?toc=%2fazure%2fbatch%2ftoc.json).

> [!TIP]
> Po zakończeniu toodig w toohello interfejsu API partii na pełniejsze zrozumienia hello ich funkcje zawiera, zapoznaj się z hello [Przegląd funkcji partii dla deweloperów](batch-api-basics.md).
> 
> 

## <a name="azure-accounts-for-batch-development"></a>Konta platformy Azure na potrzeby programowania w usłudze Batch
Podczas opracowywania rozwiązań partii użyjesz hello następującego konta na platformie Microsoft Azure.

* **Konto i subskrypcja platformy Azure** — Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN][msdn_benefits] lub utworzyć [bezpłatne konto platformy Azure][free_account]. Podczas tworzenia konta zostanie utworzona domyślna subskrypcja.
* **Konto usługi Batch** — zasoby usługi Batch, w tym pule, węzły obliczeniowe, zadania i podzadania są skojarzone z kontem usługi Azure Batch. Gdy aplikacja wysyła żądanie hello usługa partia zadań, uwierzytelnia Żądanie hello przy użyciu nazwy konta partii zadań Azure hello, adres URL hello hello konta i klucz dostępu. Możesz [Tworzenie konta usługi partia zadań](batch-account-create-portal.md) w hello portalu Azure.
* **Konto usługi Storage** — Usługa Batch obejmuje wbudowaną obsługę pracy z plikami w usłudze [Azure Storage][azure_storage]. Niemal każdego scenariusza partii korzysta z magazynu obiektów Blob platformy Azure do przemieszczania hello programy, które uruchamiania zadań i hello przetwarzania danych i do przechowywania danych wyjściowych, które generują one hello. toocreate konta magazynu, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).

## <a name="batch-service-apis"></a>Interfejsy API usługi Batch

Aplikacje i usługi można wystawianie bezpośrednie wywołania interfejsu API REST lub użyj jednej lub kilku powitania po toorun biblioteki klienta i zarządzanie obciążeń partii zadań Azure.

| Interfejs API | Dokumentacja interfejsu API | Do pobrania | Samouczek | Przykłady kodu | Więcej informacji |
| --- | --- | --- | --- | --- | --- |
| **Batch REST** |[MSDN][batch_rest] |Nie dotyczy |- |- | [Obsługiwane wersje](https://docs.microsoft.com/rest/api/batchservice/batch-service-rest-api-versioning) |
| **Batch .NET** |[docs.microsoft.com][api_net] |[NuGet ][api_net_nuget] |[Samouczek](batch-dotnet-get-started.md) |[GitHub][api_sample_net] | [Informacje o wersji](http://aka.ms/batch-net-dataplane-changelog) |
| **Batch Python** |[readthedocs.io][api_python] |[PyPI][api_python_pypi] |[Samouczek](batch-python-tutorial.md)|[GitHub][api_sample_python] | [Plik Readme](https://github.com/Azure/azure-sdk-for-python/blob/master/doc/batch.rst) |
| **Batch Node.js** |[github.io][api_nodejs] |[npm][api_nodejs_npm] |- |- | [Plik Readme](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/batch) |
| **Batch Java** |[github.io][api_java] |[Maven][api_java_jar] |- |[Plik Readme][api_sample_java] | [Plik Readme](https://github.com/Azure/azure-batch-sdk-for-java)|

## <a name="batch-management-apis"></a>Interfejsy API usługi Batch Management

Witaj interfejsów API Menedżera zasobów Azure dla partii zapewniają dostęp programistyczny tooBatch kont. Za pomocą tych interfejsów API można programowo zarządzać kontami usługi Batch, przydziałami i pakietami aplikacji.  

| Interfejs API | Dokumentacja interfejsu API | Do pobrania | Samouczek | Przykłady kodu |
| --- | --- | --- | --- | --- |
| **Interfejsy REST menedżera zasobów usługi Batch** |[docs.microsoft.com][api_rest_mgmt] |Nie dotyczy |- |[GitHub](https://github.com/Azure-Samples/batch-dotnet-manage-batch-accounts) |
| **Platforma .NET menedżera zasobów usługi Batch** |[docs.microsoft.com][api_net_mgmt] |[NuGet ][api_net_mgmt_nuget] | [Samouczek](batch-management-dotnet.md) |[GitHub][api_sample_net] |

## <a name="batch-command-line-tools"></a>Narzędzia wiersza polecenia usługi Batch

Te narzędzia wiersza polecenia zapewniają hello same funkcje jak hello usługa partia zadań i interfejsów API Management partii: 

* [Partii poleceń cmdlet programu PowerShell][batch_ps]: hello polecenia cmdlet partii zadań Azure w hello [programu Azure PowerShell](/powershell/azure/overview) modułu włączyć toomanage partii zasobów przy użyciu programu PowerShell.
* [Azure CLI](/cli/azure/overview): hello interfejsu wiersza polecenia platformy Azure (Azure CLI) to zestaw narzędzi i platform, udostępniający poleceń powłoki do interakcji z wielu usług Azure, w tym hello partii i Usługa zarządzania partii. Zobacz [Zarządzanie partii zasobów przy użyciu interfejsu wiersza polecenia Azure](batch-cli-get-started.md) Aby uzyskać więcej informacji o korzystaniu z partii hello wiersza polecenia platformy Azure.

## <a name="other-tools-for-application-development"></a>Inne narzędzia do opracowywania aplikacji

Oto niektóre dodatkowe narzędzia, które mogą być przydatne do budowania i debugowania aplikacji i usług tworzonych za pomocą usługi Batch:

* [Azure portal][portal]: tworzenie, monitorowanie i usunąć pule partii, zadań i zadań w hello Azure bloki partii portalu. Podczas uruchamiania zadań, a nawet pobierania plików z węzłami obliczeniowymi hello w Twojej puli, można wyświetlić informacje o stanie hello tych i innych zasobów. Na przykład podczas rozwiązywania problemów można pobrać plik `stderr.txt` zadania zakończonego niepowodzeniem. Możesz również pobrać pliki pulpitu zdalnego (RDP) w węzłach toocompute można toolog.
* [Eksplorator usługi partia zadań Azure][batch_explorer]: Eksplorator partii oferuje podobne funkcje zarządzania zasobami partii jako hello portalu Azure, ale w autonomicznej aplikacja kliencka Windows Presentation Foundation (WPF). Jeden z hello partiami platformy .NET przykładowe aplikacje dostępne na [GitHub][github_samples], można skompiluj go z programem Visual Studio 2015 lub nowszego i użyć go toobrowse i zarządzanie zasobami hello na koncie usługi partia zadań podczas opracowywania i debugowanie rozwiązań partii. Wyświetl zadanie, puli i szczegóły zadania pobierania plików z węzłów obliczeniowych i połączyć toonodes zdalnie przy użyciu pulpitu zdalnego (RDP) plików, które można pobrać z Eksploratora partii.
* [Eksplorator usługi Storage Azure Microsoft][storage_explorer]: podczas nie ściśle narzędzia partii zadań Azure, hello Eksploratora usługi Storage jest inny toohave przydatnym narzędziem podczas opracowywania i debugowanie rozwiązań partii.

## <a name="additional-resources"></a>Dodatkowe zasoby

- toolearn informacje rejestrowania zdarzeń z partii aplikacji, zobacz [rejestrowania zdarzeń diagnostycznych oceny i monitorowania rozwiązań partii](batch-diagnostics.md). Aby uzyskać informacje na zdarzenia generowane przez hello usługa partia zadań, zobacz [analizach wsadowych](batch-analytics.md).
- Aby uzyskać informacje o zmiennych środowiskowych dla węzłów obliczeniowych, zobacz [Zmienne środowiskowe węzła obliczeniowego usługi Azure Batch](batch-compute-node-environment-variables.md).

## <a name="next-steps"></a>Następne kroki

* Witaj odczytu [Przegląd funkcji partii dla deweloperów](batch-api-basics.md), ważne informacje dla każdego przygotowywanie toouse partii. Witaj artykuł zawiera bardziej szczegółowe informacje o partii usługi zasobów, takich jak pule, węzłów, zadań i zadań i hello wiele funkcji interfejsu API, które można używać podczas tworzenia aplikacji partii.
* [Rozpoczynanie pracy z hello biblioteki partii zadań Azure dla platformy .NET](batch-dotnet-get-started.md) toolearn jak toouse C# i hello proste obciążenia za pomocą wspólnego przepływu pracy partii tooexecute biblioteki partiami platformy .NET. W tym artykule powinien być jednym z Twojego pierwszego zatrzymuje podczas nauki jak toouse hello usługa partia zadań. Istnieje również [wersji języka Python](batch-python-tutorial.md) hello samouczka.
* Pobierz hello [przykłady w serwisie GitHub kodu] [ github_samples] toosee jak zarówno C# i Python umożliwia łączenie z obciążeń próbki tooschedule i procesu wsadowego.
* Zapoznaj się z hello [ścieżka szkoleniowa dotycząca partii] [ learning_path] tooget pomysł tooyou hello zasoby dostępne w trakcie informacje toowork z partii.


[azure_storage]: https://azure.microsoft.com/services/storage/
[api_java]: http://azure.github.io/azure-sdk-for-java/
[api_java_jar]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-batch%22
[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_nuget]: https://www.nuget.org/packages/Azure.Batch/
[api_rest_mgmt]: https://docs.microsoft.com/\rest/api/batchmanagement/
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_net_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[api_nodejs]: http://azure.github.io/azure-sdk-for-node/azure-batch/latest/
[api_nodejs_npm]: https://www.npmjs.com/package/azure-batch
[api_python]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html
[api_python_pypi]: https://pypi.python.org/pypi/azure-batch
[api_sample_net]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp
[api_sample_python]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[api_sample_java]: https://github.com/Azure/azure-batch-samples/tree/master/Java/
[batch_ps]: /powershell/resourcemanager/azurerm.batch/v2.7.0/azurerm.batch
[batch_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[free_account]: https://azure.microsoft.com/free/
[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[msdn_benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[storage_explorer]: http://storageexplorer.com/
[portal]: https://portal.azure.com
