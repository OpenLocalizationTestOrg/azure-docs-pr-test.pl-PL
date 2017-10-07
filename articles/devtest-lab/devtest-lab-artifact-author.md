---
title: niestandardowe artefakty aaaCreate dla maszyny Wirtualnej DevTest Labs | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooauthor własne artefaktów dla za pomocą DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>Tworzenie niestandardowych artefaktów dla maszyny Wirtualnej DevTest Labs
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>Omówienie
**Artefakty** są używane toodeploy i konfigurowania aplikacji po zainicjowaniu obsługi maszyny Wirtualnej. Artefakt składa się z plikiem definicji artefaktów i innych plików skryptów, które są przechowywane w folderze w repozytorium git. Pliki definicji artefaktów składają się z kodu JSON i wyrażeń, których można używać toospecify co chcesz tooinstall na maszynie Wirtualnej. Na przykład można zdefiniować nazwę hello artefaktu, toorun poleceń i parametrów, które są dostępne po uruchomieniu polecenia hello. Może się odwoływać tooother plików skryptów w pliku definicji artefaktów hello według nazwy.

## <a name="artifact-definition-file-format"></a>Format pliku definicji artefaktów
Witaj poniższy przykład przedstawia hello sekcje, które tworzą hello podstawowej struktury pliku definicji:

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| Nazwa elementu | Wymagana? | Opis |
| --- | --- | --- |
| $schema |Nie |Lokalizacja pliku hello schematu JSON, który ułatwia testowanie hello ważności hello pliku definicji. |
| Tytuł |Tak |Nazwa wyświetlana w laboratorium hello artefaktu hello. |
| description |Tak |Opis wyświetlany w laboratorium hello artefaktu hello. |
| Identyfikator iconUri |Nie |Identyfikator URI ikony hello wyświetlany w laboratorium hello. |
| targetOsType |Tak |System operacyjny hello zainstalowanym artefaktu maszyny Wirtualnej. Są obsługiwane opcje: systemu Windows i Linux. |
| parameters |Nie |Wartości, które znajdują się po uruchomieniu polecenia install artefaktów na maszynie. Pomaga to w Dostosowywanie Twojej artefaktu. |
| UruchomPolecenie |Tak |Artefaktu zainstalować polecenia, która jest wykonywana na maszynie Wirtualnej. |

### <a name="artifact-parameters"></a>Parametry artefaktów
W sekcji parametrów hello pliku definicji hello należy określić wartości, które użytkownik może wprowadzić podczas instalowania artefaktów. Może się odwoływać wartości toothese polecenia install hello artefaktu.

Definiuje parametry z następującej struktury hello:

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| Nazwa elementu | Wymagana? | Opis |
| --- | --- | --- |
| type |Tak |Typ wartości parametru. Zobacz hello następujące listy hello dozwolone typy: |
| Nazwa wyświetlana |Tak |Nazwa parametru hello, który jest użytkownikiem tooa wyświetlanych w laboratorium hello. | |
| description |Tak |Opis parametru hello, który jest wyświetlany w laboratorium hello. |

Witaj dozwolone typy to:

* String — dowolny prawidłowy ciąg JSON
* int — dowolną prawidłową liczbą całkowitą JSON
* bool — wszystkie prawidłowe JSON logiczna
* Array — nieprawidłowy tablicy JSON

## <a name="artifact-expressions-and-functions"></a>Artefaktu wyrażeń i funkcji
Można użyć wyrażenia i funkcje tooconstruct hello artefaktu polecenie instalacji.
Wyrażenia są ujęte w nawiasy kwadratowe ([i]) i są oceniane po zainstalowaniu hello artefaktu. Wyrażenia mogą występować w dowolnym miejscu w wartości ciągu JSON i zawsze zwracają inną wartość JSON. Jeśli potrzebujesz toouse literałem, która rozpoczyna się od nawiasu [, należy użyć dwóch nawiasy kwadratowe [[.
Zwykle używanie wyrażeń z tooconstruct funkcji wartości. Podobnie jak w języku JavaScript, wywołania funkcji są sformatowane jako functionName(arg1,arg2,arg3).

Witaj Poniższa lista zawiera typowe funkcje:

* parameters(parameterName) — zwraca wartość parametru jest dostępne po uruchomieniu polecenia artefaktu hello.
* concat (arg1, arg2, arg3,...) - łączy wiele wartości ciągu. Ta funkcja może być dowolną liczbę argumentów.

powitania po przykładzie pokazano, jak toouse wyrażeń i funkcji tooconstruct wartość:

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>Tworzenie niestandardowych artefaktów
Utwórz użytkownika niestandardowego artefaktu wykonaj następujące czynności:

1. Zainstaluj edytor JSON — należy toowork Edytor JSON z plików definicji artefaktów. Firma Microsoft zaleca używanie [Visual Studio Code](https://code.visualstudio.com/), która jest dostępna dla systemu Windows, Linux i OS X.
2. Get artifactfile.json próbki - wyewidencjonowanie artefakty hello utworzone przez zespół Azure DevTest Labs na naszych [repozytorium GitHub](https://github.com/Azure/azure-devtestlab), w którym utworzono rozbudowane biblioteki artefaktów, które ułatwiają tworzenie własnych artefaktów. Pobierz plik definicji artefaktów i upewnić toocreate tooit zmiany własne artefaktów.
3. Upewnij się, użyj IntelliSense — IntelliSense wykorzystać toosee prawidłowe elementy, które mogą być używane tooconstruct pliku definicji artefaktów. Można również sprawdzić hello różnych opcji dla wartości elementu. Na przykład Pokaż IntelliSense Witaj dwie możliwości systemu Windows lub Linux, edytując hello **targetOsType** elementu.
4. Magazyn artefaktów hello w [repozytorium git](devtest-lab-add-artifact-repo.md).
   
   1. Utwórz oddzielne katalog dla każdego artefaktu, gdzie nazwa katalogu hello jest hello takie same jak nazwa artefaktu hello.
   2. Magazyn hello artefaktu definicji (artifactfile.json) w katalogu hello utworzonego pliku.
   3. Polecenie instalacji magazynu hello skrypty, które są przywoływane z hello artefaktu.
      
      Oto przykład może wyglądać folderu artefaktu:
      
      ![Przykład repozytorium git artefaktów](./media/devtest-lab-artifact-author/git-repo.png)
5. Dodawanie laboratorium toohello repozytorium artefaktów hello — można znaleźć w artykule toohello [dodać repozytorium Git artefakty i szablony](devtest-lab-add-artifact-repo.md).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>Pokrewne artykuły:
* [Jak toodiagnose artefaktu błędów w usłudze DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Dołącz do maszyny Wirtualnej tooexisting domeny AD przy użyciu szablonu usługi resource manager w usłudze Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Dodawanie laboratorium tooa repozytorium artefaktów Git](devtest-lab-add-artifact-repo.md).

