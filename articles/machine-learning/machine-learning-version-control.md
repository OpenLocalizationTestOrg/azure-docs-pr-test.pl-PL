---
title: "aaaALM w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Zastosuj najlepsze rozwiązania dotyczące zarządzania cyklem życia aplikacji w usłudze Azure Machine Learning Studio"
keywords: "Kontrola wersji ALM, AML, Azure ML, Zarządzanie cyklem życia aplikacji,"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1be6577d-f2c7-425b-b6b9-d5038e52b395
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: haining
ms.openlocfilehash: 99470ff72fea7ab59d9d44f3fded7b9dd49a38c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-lifecycle-management-in-azure-machine-learning-studio"></a>Zarządzanie cyklem życia aplikacji w usłudze Azure Machine Learning Studio
Azure Machine Learning Studio to narzędzie do tworzenia eksperymenty uczenia maszynowego, które są operationalized na platformie Azure cloud hello. Jest tak jak hello programu Visual Studio IDE i usługą w chmurze skalowalne scalone z pojedynczą platformę. Standardowe rozwiązania zarządzania cyklem życia aplikacji (ALM), z wersji można zastosować różne zasoby tooautomated wykonywania i wdrażania w Azure Machine Learning Studio. W tym artykule omówiono niektóre opcje hello i metod.

## <a name="versioning-experiment"></a>Przechowywanie wersji eksperymentu
Istnieją dwa sposoby zalecane tooversion eksperymentów. Można zależne od wbudowanej Historia uruchomień, lub wyeksportować hello eksperymentu w formacie JavaScript Object Notation (JSON) i zarządzać nią zewnętrznie. Każde podejście jest dostarczany z jej zalet i wad.

### <a name="experiment-snapshots-using-run-history"></a>Za pomocą historii Uruchom migawki eksperymentu
Modelu wykonywania hello hello Azure Machine Learning Studio uczenia eksperymentu, każdym kliknięciu hello **Uruchom** przycisk w edytorze eksperymentu hello niezmienne migawki eksperymentu hello jest przesłanych toohello harmonogramu zadań. Ta lista migawek można wyświetlić, klikając hello **Uruchom historii** przycisk na pasku poleceń hello w widoku edytora hello eksperymentu.

![Przycisk historii wykonywania](media/machine-learning-version-control/runhistory.png)

Można następnie migawki hello otwarte w trybie zablokowany, klikając nazwę hello doświadczenia hello na powitania czasu hello eksperymentu został przesłany toorun i hello migawki. Należy zauważyć, że tylko hello pierwszego elementu z listy hello reprezentuje hello bieżącego eksperymentu, jest w stanie edycji. Również należy zauważyć, że każdy migawki mogą znajdować się w różnych stan stany również tym Zakończono (Uruchom), częściowego nie powiodła się i nie powiodło się (Uruchom), częściowego lub projekt.

![Listy historii wykonywania](media/machine-learning-version-control/runhistorylist.png)

Po otwarciu, można zapisać jako nowy eksperyment hello migawki eksperymentu, a następnie zmodyfikować go. Jeśli migawki eksperymentu zawiera zasobów takich jak trenowanego modelu, przekształcania i zestawu danych, które zostały zaktualizowane wersje, hello migawki zachowuje hello odwołuje się do toohello oryginalnej wersji podczas hello migawki. Jeśli zapiszesz hello zablokowany migawki jako nowy eksperyment, Azure Machine Learning Studio wykrywa hello istnienie nowszej wersji tych zasobów i automatycznie aktualizuje je w hello nowy eksperyment.

Jeśli usuniesz eksperymentu hello, są usuwane wszystkie migawki tego eksperymentu.

### <a name="exportimport-experiment-in-json-format"></a>Eksperymentu eksportu/importu w formacie JSON
migawki historii Hello Uruchom zachować niezmienne wersję hello eksperymentu w usłudze Azure Machine Learning Studio za każdym razem, gdy jest toorun przesłane. Można także zapisać lokalną kopię eksperymentu hello i zaewidencjonować tooyour systemu kontroli źródła Ulubione, takich jak Team Foundation Server i później ponownie utworzyć eksperyment z tym plikiem lokalnym. Można użyć hello [programu PowerShell usługi Azure Machine Learning](http://aka.ms/amlps) polecenia cmdlet [ *AmlExperimentGraph eksportu* ](https://github.com/hning86/azuremlps#export-amlexperimentgraph) i [  *Import-AmlExperimentGraph* ](https://github.com/hning86/azuremlps#import-amlexperimentgraph) tooaccomplish który.

Plik JSON Hello jest tekstową reprezentację wartości hello eksperymentu wykresu, która może obejmować tooassets odwołania w obszarze roboczym hello, takie jak element dataset lub uczonego modelu. Nie zawiera on serializacji wersji hello zasobów. Przy próbie dokumentu JSON hello tooimport do obszaru roboczego hello hello odwołuje się do zasobów musi już istnieć z hello sam identyfikatorów, które są przywoływane w eksperymencie hello zasobów. W przeciwnym razie nie będzie tooaccess stanie hello zaimportowane eksperymentu.

## <a name="versioning-trained-model"></a>Przechowywanie wersji uczonego modelu
Uczonego modelu w usłudze Azure Machine Learning jest serializowany w formacie znane jako plik .iLearner i znajduje się na koncie magazynu obiektów Blob platformy Azure hello skojarzonych z obszarem roboczym hello. Jednym ze sposobów tooget kopię pliku .iLearner hello jest hello ponownego trenowania interfejsu API. [W tym artykule](machine-learning-retrain-models-programmatically.md) wyjaśniono sposób działania hello ponownego trenowania interfejsu API. Witaj ogólne kroki:

1. Konfigurowanie eksperymentu szkolenia.
2. Dodawanie modułu Train Model toohello portu wyjście usługi sieci web lub hello moduł, który tworzy hello uczonego modelu, takie jak dostosować Hyperparameter modelu lub utworzyć Model R.
3. Uruchamianie eksperymentu uczenia, a następnie wdrożyć go jako usługi sieci web szkolenia modelu.
4. Wywołaj hello BES punkt końcowy usługi sieci web szkolenia hello i określ nazwy pliku żądanego .iLearner hello i lokalizacja konta magazynu obiektów Blob którym będzie przechowywany.
5. Zakończy zbiorów hello wyprodukowanych .iLearner pliku po hello BES wywołania.

Inny sposób tooretrieve hello .iLearner plik jest za pomocą polecenia programu PowerShell hello [ *AmlExperimentNodeOutput pobierania*](https://github.com/hning86/azuremlps#download-amlexperimentnodeoutput). Może to być łatwiejsze, jeśli chcesz tooget kopię hello .iLearner pliku bez modelu hello tooretrain potrzeby hello programowo.

Po hello .iLearner plik zawierający hello trenowanego modelu, można następnie wdrożyć strategii przechowywania wersji. strategii Hello może być tak proste, jak stosowanie sprzed/przyrostek jako konwencji nazewnictwa i pozostawienie hello .iLearner pliku w magazynie obiektów Blob lub kopiowania/importowania go do systemu kontroli wersji.

następnie można Hello .iLearner zapisany plik wyników za pośrednictwem usług sieci web wdrożone.

## <a name="versioning-web-service"></a>Przechowywanie wersji usługi sieci web
Można wdrożyć dwa typy usług sieci web z eksperymentu uczenia maszynowego Azure. Usługa sieci web klasycznego Hello jest ściśle powiązane ze hello eksperymentu, a także hello obszaru roboczego. Hello nową usługę sieci web używa hello Azure Resource Manager framework i nie jest już połączone z oryginalnego eksperymentu hello lub hello obszaru roboczego.

### <a name="classic-web-service"></a>Usługa sieci web klasycznego
usługi sieci web klasycznego tooversion, można korzystać konstrukcji punkt końcowy usługi sieci web hello. Oto typowy przepływ:

1. Z predykcyjnej eksperymentu możesz wdrożyć nowe klasycznego usługi sieci web, który zawiera domyślny punkt końcowy.
2. Możesz utworzyć nowy punkt końcowy o nazwie ep2, który udostępnia hello bieżącej wersji hello eksperymentu/uczenia modelu.
3. Przejdź wstecz i aktualizowanie eksperyment predykcyjny i trenowanego modelu.
4. Należy ponownie wdrożyć eksperyment predykcyjny hello, który zostanie następnie zaktualizuj hello domyślnego punktu końcowego. Ale nie zmieni ep2.
5. Możesz utworzyć dodatkowe punktu końcowego o nazwie ep3, który udostępnia nową wersję hello eksperymentu hello i uczonego modelu.
6. Wróć toostep 3 w razie potrzeby.

W czasie, może mieć wiele punktów końcowych utworzone w hello sama usługa sieci web. Każdy punkt końcowy reprezentuje kopię w momencie eksperymentu hello zawierającą wersję w momencie hello hello trenowanego modelu. Następnie można użyć toodetermine logiki zewnętrznych, które toocall punktu końcowego, który oznacza wybranie wersji hello uczony model dla wykonywania oceniania hello.

Można również tworzyć wiele punktów końcowych usługi sieci web identyczne i zastosować poprawki różne wersje hello .iLearner pliku toohello punktu końcowego tooachieve podobny efekt. [W tym artykule](machine-learning-create-models-and-endpoints-with-powershell.md) opisano szczegółowo w sposób tooaccomplish który.

### <a name="new-web-service"></a>Nowa usługa sieci web
Jeśli utworzysz nową usługę sieci web opartej na usłudze Azure Resource Manager hello punktu końcowego konstrukcja nie jest już dostępny. Zamiast tego można wygenerować plików definicji (WSD) usługi sieci web w formacie JSON z predykcyjnej eksperymentu przy użyciu hello [AmlWebServiceDefinitionFromExperiment eksportu](https://github.com/hning86/azuremlps#export-amlwebservicedefinitionfromexperiment) polecenia programu PowerShell lub przy użyciu hello [ *AzureRmMlWebservice eksportu* ](https://msdn.microsoft.com/library/azure/mt767935.aspx) polecenia programu PowerShell z usługi sieci web na podstawie Resource Manager wdrożone.

Po utworzeniu hello wyeksportowany i wersja pliku WSD sterować nim, hello WSD można wdrożyć jako nową usługę sieci web, w planie usługi innej witryny sieci web w innym regionie Azure. Po prostu upewnij się, że Podaj konto magazynu odpowiednie hello się, że konfiguracja, a także hello nowych sieci web identyfikator planu usługi. toopatch w różnych .iLearner pliki, można zmodyfikować pliku WSD hello i aktualizacji hello lokalizacji odwołania hello uczenia modelu i wdróż je jako nową usługę sieci web.

## <a name="automate-experiment-execution-and-deployment"></a>Automatyzacja wdrażania i wykonywania eksperymentu
Ważnym aspektem ALM jest wykonanie hello stanie tooautomate toobe i proces wdrażania aplikacji hello. W usłudze Azure Machine Learning, można to zrobić za pomocą hello [modułu PowerShell](http://aka.ms/amlps). Oto przykład end-to-end kroków, które są odpowiednie tooa standardowe ALM automatycznego wdrożenia/wykonywania procesu przy użyciu hello [modułu programu PowerShell usługi Azure Machine Learning Studio](http://aka.ms/amlps). Każdy krok jest połączony tooone lub więcej apletów poleceń programu PowerShell pomocne tooaccomplish który krok.

1. [Przekaż zestawu danych](https://github.com/hning86/azuremlps#upload-amldataset).
2. Skopiuj eksperyment uczenia do obszaru roboczego hello z [obszaru roboczego](https://github.com/hning86/azuremlps#copy-amlexperiment) lub [galerii](https://github.com/hning86/azuremlps#copy-amlexperimentfromgallery), lub [zaimportować](https://github.com/hning86/azuremlps#import-amlexperimentgraph) [wyeksportowane](https://github.com/hning86/azuremlps#export-amlexperimentgraph) Poeksperymentuj z dysk lokalny.
3. [Aktualizowanie zestawu danych hello](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) w eksperyment uczenia hello.
4. [Uruchom eksperyment uczenia hello](https://github.com/hning86/azuremlps#start-amlexperiment).
5. [Podwyższ poziom hello uczonego modelu](https://github.com/hning86/azuremlps#promote-amltrainedmodel).
6. [Skopiuj eksperyment predykcyjny](https://github.com/hning86/azuremlps#copy-amlexperiment) hello obszaru roboczego.
7. [Aktualizacja hello uczonego modelu](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) w eksperyment predykcyjny hello.
8. [Uruchom eksperyment predykcyjny hello](https://github.com/hning86/azuremlps#start-amlexperiment).
9. [Wdrażanie usługi sieci web](https://github.com/hning86/azuremlps#new-amlwebservice) z eksperyment predykcyjny hello.
10. Testowanie usługi sieci web hello [RRS](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) lub [BES](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint) punktu końcowego.

## <a name="next-steps"></a>Następne kroki
* Pobierz hello [programu PowerShell usługi Azure Machine Learning Studio](http://aka.ms/amlps) tooautomate modułu, a następnie Rozpocznij zadania ALM.
* Dowiedz się, jak za[tworzenie i zarządzanie dużą liczbą modeli uczenia Maszynowego przy użyciu tylko jednego eksperymentu](machine-learning-create-models-and-endpoints-with-powershell.md) za pośrednictwem programu PowerShell i ponownego trenowania interfejsu API.
* Dowiedz się więcej o [wdrażanie usług sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
