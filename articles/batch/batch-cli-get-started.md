---
title: "Wprowadzenie do interfejsu wiersza polecenia platformy Azure dla usługi Batch | Microsoft Docs"
description: "Skorzystaj z szybkiego wprowadzenia do poleceń usługi Batch w interfejsie wiersza polecenia platformy Azure, aby zarządzać zasobami usługi Azure Batch"
services: batch
documentationcenter: 
author: v-dotren
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 09/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 68a5493282fa4a0b54ba551c48ae963a42b94dca
ms.sourcegitcommit: 51ea178c8205726e8772f8c6f53637b0d43259c6
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Zarządzanie zasobami usługi Batch przy użyciu interfejsu wiersza polecenia platformy Azure

Interfejs wiersza polecenia platformy Azure 2.0 to nowe środowisko wiersza polecenia platformy Azure do zarządzania jej zasobami. Można go używać w systemach macOS, Linux i Windows. Interfejs wiersza polecenia platformy Azure 2.0 jest zoptymalizowany do zarządzania i administrowania zasobami platformy Azure z wiersza polecenia. Interfejs wiersza polecenia platformy Azure umożliwia zarządzanie kontami usługi Azure Batch i zarządzanie zasobami, na przykład pulami, zadaniami i zadaniami podrzędnymi. Za pomocą interfejsu wiersza polecenia platformy Azure można tworzyć skrypty dla wielu tych samych zadań, które wykonuje się za pomocą interfejsów API usługi Batch, witryny Azure Portal oraz poleceń cmdlet programu PowerShell dla usługi Batch.

Ten artykuł zawiera omówienie korzystania z [interfejsu wiersza polecenia platformy Azure w wersji 2.0](https://docs.microsoft.com/cli/azure/overview) z usługą Batch. Aby zapoznać się z omówieniem korzystania z interfejsu wiersza polecenia na platformie Azure, zobacz [Rozpoczynanie pracy z interfejsem wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).

Firma Microsoft zaleca korzystanie z najnowszej wersji interfejsu wiersza polecenia na platformie Azure, czyli wersji 2.0. Aby uzyskać więcej informacji na temat wersji 2.0, zobacz [Interfejs wiersza polecenia platformy Azure 2.0 jest ogólnie dostępny](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).

## <a name="set-up-the-azure-cli"></a>Konfigurowanie interfejsu wiersza polecenia platformy Azure

Aby zainstalować interfejs wiersza polecenia platformy Azure, wykonaj czynności opisane w artykule [Instalowanie interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

> [!TIP]
> Zaleca się częstą aktualizację interfejsu wiersza polecenia platformy Azure, aby mieć możliwość korzystania z aktualizacji i rozszerzeń usługi.
> 
> 

## <a name="command-help"></a>Pomoc związana z poleceniami

Możesz wyświetlić tekst pomocy dla każdego polecenia w interfejsie wiersza polecenia platformy Azure, dodając do polecenia opcję `-h`. Pomiń wszelkie inne opcje. Na przykład:

* Aby uzyskać pomoc dotyczącą polecenia `az`, wprowadź: `az -h`
* Aby uzyskać listę wszystkich poleceń usługi Batch w interfejsie wiersza polecenia, użyj: `az batch -h`
* Aby uzyskać pomoc związaną z tworzeniem konta usługi Batch, wprowadź: `az batch account create -h`

W razie wątpliwości użyj opcji wiersza polecenia `-h`, aby uzyskać pomoc dotyczącą jakiegokolwiek polecenia interfejsu wiersza polecenia platformy Azure.

> [!NOTE]
> W wcześniejszych wersjach interfejsu wiersza polecenia platformy Azure polecenia interfejsu wiersza polecenia były poprzedzane opcją `azure`. W wersji 2.0 wszystkie polecenia są teraz poprzedzane opcją `az`. Należy zaktualizować skrypty, aby były zgodne z nową składnią wersji 2.0.
>
>  

Ponadto w dokumentacji wiersza polecenia platformy Azure można znaleźć szczegółowe informacje o [poleceniach wiersza polecenia platformy Azure dla usługi Batch](https://docs.microsoft.com/cli/azure/batch). 

## <a name="log-in-and-authenticate"></a>Logowanie i uwierzytelnianie

Aby używać interfejsu wiersza polecenia platformy Azure z usługą Batch, należy się zalogować i uwierzytelnić. Należy w tym celu wykonać dwa proste kroki:

1. **Zaloguj się na platformie Azure.** Zalogowanie się na platformie Azure zapewnia dostęp do poleceń usługi Azure Resource Manager, w tym do poleceń [usługi Batch Management](batch-management-dotnet.md).  
2. **Zaloguj się na koncie usługi Batch.** Zalogowanie się na koncie usługi Batch zapewnia dostęp do poleceń usługi Batch.   

### <a name="log-in-to-azure"></a>Zaloguj się do platformy Azure.

Istnieje kilka różnych sposobów logowania się na platformie Azure. Opisano je szczegółowo w artykule [Logowanie się za pomocą interfejsu wiersza polecenia platformy Azure 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [Logowanie interakcyjne](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#az_authenticate_azure_cli_interactive_log_in). Zaloguj się interakcyjnie, gdy samodzielnie uruchamiasz polecenia interfejsu wiersza polecenia platformy Azure w wierszu polecenia.
2. [Logowanie za pomocą jednostki usługi](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#az_authenticate_azure_cli_logging_in_with_a_service_principal). Zaloguj się za pomocą jednostki usługi, gdy uruchamiasz polecenia interfejsu wiersza polecenia platformy Azure za pomocą skryptu lub aplikacji.

Na potrzeby tego artykułu wyjaśnimy, jak zalogować się interakcyjnie. W wierszu polecenia wpisz [az login](https://docs.microsoft.com/cli/azure/#login):

```azurecli
# Log in to Azure and authenticate interactively.
az login
```

Polecenie `az login` zwraca token używany do uwierzytelniania, jak to tutaj pokazano. Postępuj zgodnie z instrukcjami, aby otworzyć stronę internetową i przesłać token do platformy Azure:

![Zaloguj się do platformy Azure.](./media/batch-cli-get-started/az-login.png)

W przykładach wymienionych w sekcji [Przykładowe skrypty powłoki](#sample-shell-scripts) również pokazano, jak uruchomić sesję interfejsu wiersza polecenia platformy Azure przez zalogowanie się interakcyjne na platformie Azure. Po zalogowaniu się można wywoływać polecenia do pracy z zasobami usługi Batch Management, w tym z kluczami, pakietami aplikacji, przydziałami i kontami usługi Batch.  

### <a name="log-in-to-your-batch-account"></a>Logowanie się na koncie usługi Batch

Aby za pomocą interfejsu wiersza polecenia platformy Azure zarządzać zasobami usługi Batch, na przykład pulami, zadaniami i zadaniami podrzędnymi, należy zalogować się na koncie usługi Batch i dokonać uwierzytelnienia. Aby zalogować się do usługi Batch, użyj polecenia [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#az_batch_account_login). 

Dostępne są dwie opcje uwierzytelnienia na koncie usługi Batch:

- **Przy użyciu uwierzytelniania usługi Azure Active Directory (Azure AD).** 

    Uwierzytelnianie przy użyciu usługi Azure AD jest ustawieniem domyślnym w przypadku używania interfejsu wiersza polecenia platformy Azure z usługą Batch i jest zalecane w większości przypadków. 
    
    W razie logowania się interakcyjnego na platformie Azure, zgodnie z opisem w poprzedniej sekcji, poświadczenia są buforowane, dzięki czemu interfejs wiersza polecenia platformy Azure może zalogować użytkownika na koncie usługi Batch za ich pomocą. W razie logowania się na platformie Azure za pomocą jednostki usługi te poświadczenia także są używane do zalogowania się na koncie usługi Batch.

    Przewagą wynikającą z korzystania z usługi Azure AD jest to, że zapewnia ona kontrolę dostępu opartą na rolach. W przypadku kontroli dostępu opartej na rolach poziom dostępu użytkownika zależy od przypisanej mu roli, a nie od tego, czy posiada on klucze konta. Zamiast zarządzać kluczami konta, można zarządzać rolami kontroli dostępu opartej na rolach oraz obsługiwać dostęp i uwierzytelnianie w usłudze Azure AD.  

        To log in to your Batch account using Azure AD, call the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#az_batch_account_login) command: 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **Przy użyciu uwierzytelniania klucza wspólnego.**

    [Uwierzytelnianie klucza wspólnego](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) polega na uwierzytelnianiu poleceń interfejsu wiersza polecenia platformy Azure dla usługi Batch za pomocą kluczy dostępu konta.

    W przypadku tworzenia skryptów interfejsu wiersza polecenia platformy Azure w celu zautomatyzowania wywoływania poleceń usługi Batch można użyć uwierzytelniania klucza wspólnego lub jednostki usługi w usłudze Azure AD. W niektórych przypadkach użycie uwierzytelniania klucza wspólnego może być łatwiejsze niż tworzenie jednostki usługi.  

    Aby zalogować się przy użyciu uwierzytelniania klucza wspólnego, dodaj w wierszu polecenia opcję `--shared-key-auth`:

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

W przykładach wymienionych w sekcji [Przykładowe skrypty powłoki](#sample-shell-scripts) pokazano, jak zalogować się na koncie usługi Batch za pomocą interfejsu wiersza polecenia platformy Azure przy użyciu zarówno usługi Azure AD, jak i klucza wspólnego.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Korzystanie z szablonów interfejsu wiersza polecenia usługi Azure Batch i transferu plików (wersja zapoznawcza)

Interfejsu wiersza polecenia platformy Azure można używać do kompleksowej obsługi zadań usługi Batch bez konieczności pisania kodu. Pliki szablonów usługi Batch obsługują tworzenie pul, zadań i zadań podrzędnych przy użyciu interfejsu wiersza polecenia platformy Azure. Interfejs wiersza polecenia platformy Azure umożliwia także przekazywanie plików wejściowych zadania do konta usługi Azure Storage skojarzonego z kontem usługi Batch oraz pobieranie z niego plików wyjściowych zadania. Więcej informacji można znaleźć w temacie [Use Azure Batch CLI Templates and File Transfer (Preview) (Korzystanie z szablonów interfejsu wiersza polecenia usługi Azure Batch i transferu plików (wersja zapoznawcza))](batch-cli-templates.md).

## <a name="sample-shell-scripts"></a>Przykładowe skrypty powłoki

W przykładowych skryptach wymienionych w poniższej tabeli pokazano, jak za pomocą poleceń interfejsu wiersza polecenia platformy Azure z usługami Batch i Batch Management wykonywać typowe zadania. Te przykładowe skrypty obejmują wiele poleceń dostępnych w interfejsie wiersza polecenia platformy Azure dla usługi Batch. 

| Skrypt | Uwagi |
|---|---|
| [Tworzenie konta usługi Batch](./scripts/batch-cli-sample-create-account.md) | Tworzy konto usługi Batch i kojarzy je z kontem magazynu. |
| [Dodawanie aplikacji](./scripts/batch-cli-sample-add-application.md) | Dodaje aplikację i przekazuje spakowane dane binarne.|
| [Zarządzanie pulami usługi Batch](./scripts/batch-cli-sample-manage-pool.md) | Ilustruje tworzenie pul, zmienianie ich rozmiarów i zarządzanie nimi. |
| [Uruchamianie zadań i zadań podrzędnych za pomocą usługi Batch](./scripts/batch-cli-sample-run-job.md) | Ilustruje uruchamianie zadania i dodawanie zadania podrzędnego. |

## <a name="json-files-for-resource-creation"></a>Pliki JSON do tworzenia zasobów

Podczas tworzenia zasobów usługi Batch, np. puli i zadań, możesz określić plik JSON zawierający konfiguracje nowego zasobu, zamiast przekazywać parametry zasobu w opcjach wiersza polecenia. Na przykład:

```azurecli
az batch pool create my_batch_pool.json
```

Możesz wykonać większość operacji tworzenia zasobów usługi Batch, korzystając wyłącznie z opcji wiersza polecenia, niemniej niektóre funkcje wymagają określenia pliku w formacie JSON zawierającego szczegółowe informacje o zasobie. Przykładowo musisz użyć pliku JSON, jeśli chcesz określić pliki zasobu dla zadania rozpoczęcia.

Aby zapoznać się ze składnią pliku JSON wymaganego do utworzenia zasobu, skorzystaj z dokumentacji [interfejsu API REST usługi Batch][rest_api]. Każdy temat „Dodawanie *typu zasobu*” w dokumentacji interfejsu API REST zawiera przykładowe skrypty JSON do tworzenia zasobu. Tych przykładowych skryptów JSON można używać jako szablonów dla plików JSON do użytku z interfejsem wiersza polecenia platformy Azure. Aby na przykład zapoznać się ze składnią pliku JSON do tworzenia puli, zobacz [Dodawanie puli do konta][rest_add_pool].

Aby uzyskać przykładowy skrypt określający plik JSON, zobacz [Uruchamianie zadań i zadań podrzędnych za pomocą usługi Batch](./scripts/batch-cli-sample-run-job.md).

> [!NOTE]
> Jeśli określisz plik JSON podczas tworzenia zasobu, wszystkie inne parametry określone dla tego zasobu w wierszu polecenia zostaną zignorowane.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Wydajne zapytania dotyczące zasobów usługi Batch

Każdy typ zasobu usługi Batch obsługuje polecenie `list`, które wysyła zapytania do konta usługi Batch i wyświetla listę zasobów tego typu. Przykładowo możesz wyświetlić listę puli na koncie i zadań w ramach zadania:

```azurecli
az batch pool list
az batch task list --job-id job001
```

Podczas wysyłania zapytania do usługi Batch z operacją `list` można określić klauzulę OData, aby ograniczyć ilość zwracanych danych. Ponieważ całe filtrowanie odbywa się po stronie serwera, tylko dane, których zażądasz, zostają przekazane podczas transmisji. Użyj tych klauzul, aby oszczędzić przepustowość (i czas) podczas wykonywania operacji związanych z wyświetlaniem listy.

W poniższej tabeli opisano klauzule OData obsługiwane przez usługę Batch:

| Klauzula | Opis |
|---|---|
| `--select-clause [select-clause]` | Zwracanie podzbioru właściwości dla każdej jednostki. |
| `--filter-clause [filter-clause]` | Zwracanie tylko jednostek, które pasują do określonego wyrażenia OData. |
| `--expand-clause [expand-clause]` | Uzyskiwanie informacji dotyczących jednostki w pojedynczym, podstawowym wywołaniu REST. Klauzula expand obsługuje obecnie tylko właściwość `stats`. |

Aby uzyskać przykładowy skrypt ilustrujący używanie klauzuli OData, zobacz [Uruchamianie zadań i zadań podrzędnych za pomocą usługi Batch](./scripts/batch-cli-sample-run-job.md).

Aby uzyskać więcej informacji o wykonywaniu wydajnych zapytań listy przy użyciu klauzul OData, zobacz [Efektywne wysyłanie zapytań do usługi Azure Batch](batch-efficient-list-queries.md).

## <a name="troubleshooting-tips"></a>Wskazówki dotyczące rozwiązywania problemów

Poniższe porady mogą być pomocne w przypadku rozwiązywania problemów związanych z interfejsem wiersza polecenia platformy Azure:

* Użyj polecenia `-h`, aby uzyskać **tekst pomocy** dla dowolnego polecenia interfejsu wiersza polecenia
* Użyj opcji `-v` i `-vv`, aby wyświetlić **pełne** dane wyjściowe polecenia. Gdy jest dołączona flaga `-vv`, w interfejsie wiersza polecenia platformy Azure wyświetlane są faktyczne żądania i odpowiedzi REST. Te przełączniki są przydatne do wyświetlania pełnych danych wyjściowych błędu.
* Możesz wyświetlić **dane wyjściowe polecenia w formie pliku JSON** przy użyciu opcji `--json`. Przykładowo polecenie `az batch pool show pool001 --json` wyświetla właściwości puli 001 w formacie JSON. Następnie możesz skopiować i zmodyfikować te dane wyjściowe, aby użyć ich w pliku `--json-file` (zobacz sekcję [Pliki JSON](#json-files) wcześniej w tym artykule).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting to any location.--->
* [Forum usługi Batch][batch_forum] jest monitorowane przez członków zespołu usługi Batch. Możesz tam zamieszczać pytania w przypadku napotkania problemów lub w sytuacji, w której potrzebujesz pomocy z konkretną operacją.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji na temat interfejsu wiersza polecenia platformy Azure, zobacz [dokumentację interfejsu wiersza polecenia platformy Azure](https://docs.microsoft.com/cli/azure/overview).
* Aby uzyskać więcej informacji o zasobach usługi Batch, zobacz [Omówienie usługi Azure Batch dla deweloperów](batch-api-basics.md).
* Aby uzyskać więcej informacji o tworzeniu pul, zadań i zadań podrzędnych przy użyciu szablonów usługi Batch i bez konieczności pisania kodu, zobacz [Use Azure Batch CLI Templates and File Transfer (Preview) (Korzystanie z szablonów interfejsu wiersza polecenia usługi Azure Batch i transferu plików (wersja zapoznawcza))](batch-cli-templates.md).

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
