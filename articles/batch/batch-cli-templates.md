---
title: "aaaRun partii zadań Azure zadania end-to-end bez pisania kodu (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Utwórz pliki szablonów hello Azure CLI toocreate partii pule, zadań i zadań."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Korzystanie z szablonów interfejsu wiersza polecenia usługi Azure Batch i transferu plików (wersja zapoznawcza)

Przy użyciu interfejsu wiersza polecenia Azure hello jest możliwe toorun zadań wsadowych bez pisania kodu.

Pliki szablonów można tworzyć i używać z hello interfejsu wiersza polecenia Azure, umożliwiające pule, zadań i zadań toobe utworzone partii. Pliki wejściowe zadania mogą być łatwo przekazywane hello konta magazynu skojarzone z hello konta i zadania dane wyjściowe pliki wsadowe pobrane.

## <a name="overview"></a>Omówienie

Toohello rozszerzenie interfejsu wiersza polecenia Azure umożliwia partii toobe używane na całej trasie przez użytkowników, którzy nie są deweloperów. Można utworzyć puli, przekazać dane wejściowe, zadań i skojarzonych zadań tworzenia i hello wynikowe dane wyjściowe pobrane — kod nie jest wymagany, hello interfejsu wiersza polecenia używane bezpośrednio lub zintegrowania skryptów.

Tworzenie szablonów partii na powitania [istniejących obsługę partii w hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) umożliwiająca pliki w formacie JSON wartości właściwości toospecify hello tworzenia pul, zadania, zadania i inne elementy. Z szablonami partii hello następujące funkcje są dodawane przez co to jest możliwe z plikami JSON hello:

-   Można zdefiniować parametrów. Jeśli szablon hello jest używany, tylko wartości parametrów hello są toocreate określony element hello, o wartości innych właściwości elementu określany w treści szablonu hello. Użytkownik, który rozumie, iż partii i toobe aplikacje uruchamiane przez partię można utworzyć szablony, określając puli, zadania i wartości właściwości zadania. Użytkownik mniej znanych z partii i/lub aplikacje potrzebuje tylko wartości hello toospecify hello zdefiniowanych parametrów.

-   Utworzenie zadania fabryki zadań lub więcej zadań skojarzonych z zadaniem, unikając hello konieczność dla wielu toobe definicji zadania utworzone i znacznie uproszczenie przesyłanie zadań.


Pliki danych wejściowych muszą toobe podany dla zadań i plików danych wyjściowych często są tworzone. Konto magazynu jest skojarzony domyślnie, z każdej z partii konta i pliki mogą być łatwo przekazanych tooand z tego konta magazynu przy użyciu interfejsu wiersza polecenia, z nie kodowania i wymagane nie poświadczenia magazynu.

Na przykład [ffmpeg](http://ffmpeg.org/) jest popularnych aplikacji, która przetwarza plików audio i wideo. Hello Azure partii interfejsu wiersza polecenia mogą być używane tooinvoke ffmpeg tootranscode źródła plików wideo toodifferent rozwiązania.

-   Utworzono szablon puli. Użytkownik Hello tworzenia szablonu hello zna, jak toocall hello ffmpeg aplikacji i jej wymagań; określają one hello odpowiedni system operacyjny, maszyna wirtualna rozmiar, jak ffmpeg jest zainstalowana (od pakietu aplikacji lub za pomocą Menedżera pakietów, na przykład) i innych wartości właściwości w puli. Parametry są tworzone, więc jeśli szablon hello jest używany, toobe określony wymaga tylko identyfikator puli hello i liczbę maszyn wirtualnych.

-   Utworzono szablon zadania. Tworzenie szablonu hello Hello użytkownika wie jak ffmpeg toobe musi wywołać tootranscode źródła wideo tooa inną rozdzielczość i określa wiersz polecenia zadania hello; które znają, że istnieje folder zawierający pliki wideo źródłowe hello, z zadaniem wymagane dla pliku wejściowego.

-   Użytkownik końcowy zestaw plików wideo tootranscode najpierw tworzy puli przy użyciu szablonu puli hello, określając tylko identyfikator puli hello i liczbę maszyn wirtualnych wymagana. Następnie przekazywać hello źródła plików tootranscode. Następnie można przesłać zadania przy użyciu szablonu zadania hello tylko identyfikator puli hello i lokalizację plików źródłowych hello przekazany. zadania wsadowego Hello jest tworzony z jedno zadanie na Trwa generowanie pliku wejściowego. Ponadto pliki wyjściowe przekodowane hello można pobierania.

## <a name="installation"></a>Instalacja

możliwości transferu szablonu i pliku Hello wymagają toobe rozszerzenie zainstalowane.

Aby uzyskać instrukcje dotyczące sposobu hello tooinstall wiersza polecenia platformy Azure, zobacz [zainstalować Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

Raz hello wiersza polecenia platformy Azure został zainstalowany, hello partii rozszerzenia można zainstalować przy użyciu interfejsu wiersza polecenia następujące polecenie:

```azurecli
az component update --add batch-extensions --allow-third-party
```

Aby uzyskać więcej informacji na temat hello partii rozszerzenia, zobacz [Microsoft Azure partii CLI rozszerzeń dla systemu Windows, Mac i Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).

## <a name="templates"></a>Szablony

Witaj interfejsu wiersza polecenia usługi partia zadań Azure umożliwia elementów, takich jak pule, zadania i toobe zadania utworzone przez określenie plik JSON zawierający nazwy i wartości właściwości. Na przykład:

```azurecli
az batch pool create –-json-file AppPool.json
```

Szablony usługi partia zadań Azure to podobne szablony Menedżera zasobów tooAzure, funkcje i składni. Są to pliki w formacie JSON, które zawiera element nazwy i wartości właściwości, Dodaj następujące główne pojęcia hello:

-   **Parametry**

    -   Zezwalaj na toobe wartości właściwości o tylko wartości parametrów konieczności toobe dostarczana, gdy używany jest szablon hello określone w sekcji body. Na przykład hello pełnej definicji dla puli można można umieścić w treści hello i tylko jeden parametr zdefiniowane dla Identyfikator puli; tylko ciąg identyfikatora puli w związku z tym musi toocreate toobe dostarczony puli.
        
    -   treści szablonu Hello można tworzyć przez osobę mającą wiedzę na temat partii i toobe aplikacji hello uruchamiany w partii; Jeśli szablon hello jest używany, należy podać tylko wartości parametrów zdefiniowanych przez autora hello. Użytkownik bez hello szczegółowe partii i/lub bazy wiedzy w związku z tym można używać szablonów.

-   **Zmienne**

    -   Zezwalaj na toobe wartości parametru prostymi lub złożonymi określony w jednym miejscu i używany w co najmniej jednego miejsca w treści szablonu hello. Zmienne można uprościć i zredukować rozmiar hello hello szablonu, a także była bardziej utrzymaniu przez jedną właściwości toochange lokalizacji, którego wartość może zmienić.

-   **Konstrukcji wyższego poziomu**

    -   Niektóre konstrukcji wyższego poziomu dostępnych w szablonie hello, które nie są jeszcze dostępne w hello interfejsów API partii. Na przykład można zdefiniować fabryki zadań w szablonie zadania, który tworzy wiele zadań dla zadania hello przy użyciu wspólnej definicji zadania. Te konstrukcje uniknąć toocode potrzeby hello dynamicznie utworzyć wiele plików JSON, takich jak jeden plik poszczególnych zadań, a także utworzyć skrypt aplikacji tooinstall plików za pomocą Menedżera pakietów, na przykład.

    -   W niektórych punktu, w przypadku, gdy ma to zastosowanie, tych konstrukcji mogą być dodane toothe partii usługi i jest dostępny w hello interfejsów API partii, UI itp.

### <a name="pool-templates"></a>Szablony puli

Oprócz możliwości standardowego szablonu toohello parametry i zmienne, powitania po konstrukcji wyższego poziomu są obsługiwane przez szablon puli hello:

-   **Odwołania do pakietu**

    -   Opcjonalnie umożliwia węzłów toopool toobe skopiowane oprogramowania przy użyciu pakietu menedżerów. określono Menedżera pakietów Hello i identyfikator pakietu. Trwa stanie toodeclare pozwala uniknąć jeden lub więcej pakietów hello potrzeby toocreate skrypt, który pobiera hello wymagane pakiety hello skrypt instalacji i uruchom skrypt hello w każdym węźle puli.

Hello poniżej przedstawiono przykładowy szablon, który tworzy puli maszyn wirtualnych systemu Linux z ffmpeg zainstalowana i tylko wymaga puli ciągów i hello identyfikator toouse toobe dostarczony maszyn wirtualnych:

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

Jeśli plik szablonu hello miał nazwę _ffmpeg.json puli_, a następnie hello szablon będzie można wywołać w następujący sposób:

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a>Szablony zadań

Oprócz możliwości standardowego szablonu toohello parametry i zmienne, powitania po konstrukcji wyższego poziomu są obsługiwane przez szablon zadania hello:

-   **Fabryki zadań**

    -   Tworzy wiele zadań dla zadania na podstawie definicji zadania. Trzy typy fabryki zadań są obsługiwane — parametrycznych odchylenia zadań dla każdego pliku i zadań w kolekcji.

Hello poniżej przedstawiono przykładowy szablon, który tworzy zadanie, które używa ffmpeg do tooone plików wideo MP4 transkodowanie dwa niższe rozdzielczości, z jednego zadania utworzone na źródłowy plik wideo:

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

Jeśli plik szablonu hello miał nazwę _ffmpeg.json zadania_, a następnie hello szablon będzie można wywołać w następujący sposób:

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a>Grup plików i transferu plików

Większość zadań i zadań wymagane pliki wejściowe i utworzyć pliki danych wyjściowych. Oba pliki wejściowe i pliki wyjściowe zwykle wymagają toobe przeniesione z powitania klienta toohello węzła lub z hello węzła toohello klienta. Hello rozszerzenie interfejsu wiersza polecenia Azure partii abstracts transfer plików zadań i korzysta z konta magazynu hello utworzony domyślnie dla każdego konta usługi partia zadań.

Grupa plików oznacza tooa kontener, który jest tworzony w hello kontem magazynu platformy Azure. grupy plików Hello może mieć podfoldery.

Hello rozszerzenia partii interfejsu wiersza polecenia zawiera polecenia służące do przekazywania plików z grupy określony plik tooa klientów i pobieranie plików z hello określonego pliku grupy tooa klienta.

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

Zezwalaj na pliki przechowywane w pliku grup toobe określony dla kopiowania na węzłach puli szablonów puli i zadania lub Wyłącz pulę węzłów wykonaj kopię tooa grupy plików. Na przykład w szablonie zadania poprzednio określono, hello grupy "ffmpeg — wejście" jest określony dla fabryki zadań hello jako hello lokalizację plików źródłowych hello wideo kopiowane na węzeł hello transkodowanie; Witaj grupy "ffmpeg-danych wyjściowych w pliku" jest używany jako hello lokalizacji, w którym pliki wyjściowe przekodowane hello są kopiowane węzeł hello toofrom działa każdego zadania.

## <a name="summary"></a>Podsumowanie

Obsługa transferu szablon i plik obecnie zostały dodane toohello wiersza polecenia platformy Azure. Celem Hello jest tooexpand hello odbiorców, którzy mogą używać toousers wsadowego, który nie ma potrzeby toodevelop kodu za pomocą hello interfejsów API usługi partia zadań, takich jak pracowników naukowo-badawczych, udziałem użytkowników IT i tak dalej. Bez kodowania, użytkownicy mający wiedzę na temat platformy Azure, partii i toobe aplikacji hello Uruchom przez partię można utworzyć szablony do tworzenia puli i zadania. Parametry szablonu użytkowników bez szczegółowej znajomości partii i hello aplikacji można za pomocą szablonów hello.

Wypróbowanie hello partii rozszerzenie hello wiersza polecenia platformy Azure i uzyskaliśmy wszelkie opinie i sugestie, albo w hello komentarzy tego artykułu lub za pośrednictwem hello [forum usługi partia zadań Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).

## <a name="next-steps"></a>Następne kroki

- Zobacz hello partii szablony wpisie w blogu: [za pomocą zadania uruchamiania partii zadań Azure hello Azure CLI — kod nie jest wymagany](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).
- Szczegółowa dokumentacja instalacji i użycia, przykłady i kodu źródłowego są dostępne w hello [repozytorium Azure GitHub](https://github.com/Azure/azure-batch-cli-extensions).
