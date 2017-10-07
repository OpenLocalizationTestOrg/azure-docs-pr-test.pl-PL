---
title: "Moduł aaaPowerShell dla usługi Machine Learning | Dokumentacja firmy Microsoft"
description: "Witaj modułu programu PowerShell dla usługi Azure Machine Learning jest dostępna w trybie publicznej wersji zapoznawczej. Użyj programu PowerShell toocreate i zarządzaj nimi obszarów roboczych, eksperymentów, usług sieci web i."
keywords: experiment,linear regression,machine learning algorithms,machine learning tutorial,predictive modeling techniques,data science experiment
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 59362027356b86bf286b7c07380db677ae1d71c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a>Moduł programu PowerShell dla usługi Azure Machine Learning
Witaj modułu programu PowerShell dla usługi Azure Machine Learning jest zaawansowane narzędzie, które pozwala obszarów roboczych toomanage środowiska Windows PowerShell toouse, eksperymentów, zestawy danych i usług sieci web klasycznego.

Można wyświetlić dokumentację hello i pobrać moduł hello, wraz z hello pełny kod źródłowy, na [https://aka.ms/amlps](https://aka.ms/amlps). 

> [!NOTE]
> Moduł programu PowerShell usługi Azure Machine Learning Hello jest obecnie w wersji zapoznawczej. Moduł Hello będzie toobe ulepszone i rozwinięty w tym okresie podglądu. Śledzić na powitania [Cortana Intelligence i Machine Learning blogu](https://blogs.technet.microsoft.com/machinelearning/) wiadomości lub informacji.

## <a name="what-is-hello-machine-learning-powershell-module"></a>Co to jest moduł PowerShell Learning maszyny hello?
Moduł PowerShell Learning maszyny Hello. Na podstawie NET modułu DLL umożliwiający toofully Zarządzanie obszarów roboczych usługi Azure Machine Learning, eksperymenty zestawów danych, usługi sieci web klasycznego i punktów końcowych usługi sieci web klasycznego z programu Windows PowerShell. 

Wraz z modułu hello, możesz pobrać hello pełny kod źródłowy w tym prawidłowo rozdzielonych [warstwę interfejsu API języka C#](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs). Możesz odwoływać się do tej biblioteki DLL z projektu platformy .NET i zarządzać uczenia maszynowego Azure za pomocą kodu platformy .NET. Ponadto hello biblioteki DLL jest zależna od podstawowych interfejsów API REST używaną bezpośrednio z ulubionych klienta.

## <a name="what-can-i-do-with-hello-powershell-module"></a>Co można zrobić z modułu PowerShell hello?
Poniżej przedstawiono niektóre hello zadań, które można wykonywać za pomocą ten moduł programu PowerShell. Zapoznaj się z hello [pełna dokumentacja](https://aka.ms/amlps) te i wiele więcej funkcji.

* Aprowizacja nowego obszaru roboczego za pomocą certyfikatu zarządzania ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))
* Eksportowanie i importowanie pliku JSON reprezentującego wykres eksperymentu ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) i [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))
* Uruchamianie eksperymentu ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))
* Tworzenie usługi sieci Web na podstawie eksperymentu predykcyjnego ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))
* Tworzenie punktu końcowego w usłudze opublikowanych w sieci web ([AmlWebServiceEndpoint Dodaj](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))
* Wywoływanie punktu końcowego usługi sieci Web RRS i/lub BES ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) i [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))

Poniżej przedstawiono prosty przykład za pomocą środowiska PowerShell toorun eksperymentu istniejących:

        #Find hello first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run hello Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

Aby uzyskać więcej informacji na temat przypadek użycia, zobacz w tym artykule przy użyciu tooautomate modułu programu PowerShell hello często żądanego zadania: [utworzyć wiele modeli uczenia maszynowego i sieci web punktów końcowych usługi z doświadczenia przy użyciu programu PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).

## <a name="how-do-i-get-started"></a>Jak rozpocząć?
tooget wprowadzenie Machine Learning PowerShell, Pobierz hello [wersji pakietu](https://github.com/hning86/azuremlps/releases) z serwisu GitHub i wykonaj hello [instrukcje dotyczące instalacji](https://github.com/hning86/azuremlps/blob/master/README.md). Hello instrukcje wyjaśniają sposób toounblock hello pobrane/rozpakowane biblioteki DLL, a następnie zaimportuj go do środowiska PowerShell. Większość powitalne poleceń cmdlet muszą podać identyfikator obszaru roboczego hello, hello token autoryzacji obszaru roboczego, a następnie hello region platformy Azure, która hello obszaru roboczego jest. Hello najprostszy sposób tooprovide hello wartości jest użycie domyślnego pliku config.json. instrukcje Hello również wyjaśniają sposób tooconfigure tego pliku. 

A jeśli chcesz, można sklonować hello git drzewa, zmodyfikuj kod hello i skompiluj go lokalnie za pomocą programu Visual Studio.

## <a name="next-steps"></a>Następne kroki
Hello pełną dokumentację dla hello modułu programu PowerShell można znaleźć [https://aka.ms/amlps](https://aka.ms/amlps). 

Rozszerzone przykład sposobu toouse hello modułu w rzeczywistych scenariuszy, wyewidencjonowanie hello szczegółowe użycia, [utworzyć wiele modeli uczenia maszynowego i sieci web punktów końcowych usługi z doświadczenia przy użyciu programu PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).
