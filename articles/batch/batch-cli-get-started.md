---
title: aaaGet uruchomiony z wiersza polecenia platformy Azure dla partii | Dokumentacja firmy Microsoft
description: "Przełącz szybkie wprowadzenie toohello pliki wsadowe wiersza polecenia platformy Azure zarządzanie zasobami usługi partia zadań Azure"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a>Zarządzanie zasobami usługi Batch przy użyciu interfejsu wiersza polecenia platformy Azure

Hello Azure CLI 2.0 jest nowe środowisko wiersza polecenia platformy Azure do zarządzania zasobami platformy Azure. Można go używać w systemach macOS, Linux i Windows. 2.0 interfejsu wiersza polecenia platformy Azure jest zoptymalizowany do zarządzania i administrowania zasobami Azure z wiersza polecenia hello. Używając hello Azure CLI toomanage Twojego konta partii zadań Azure i toomanage zasobów, takich jak pule, zadań i zadań. Z hello wiersza polecenia platformy Azure, można utworzyć skrypty wiele hello hello te same zadania wykonywane z interfejsów API partii, portalu Azure i poleceń cmdlet programu PowerShell partii.

Ten artykuł zawiera omówienie korzystania z [interfejsu wiersza polecenia platformy Azure w wersji 2.0](https://docs.microsoft.com/cli/azure/overview) z usługą Batch. Zobacz [wprowadzenie Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) omówienie przy użyciu hello interfejsu wiersza polecenia platformy Azure.

Firma Microsoft zaleca używanie najnowszej wersji hello hello Azure CLI w wersji 2.0. Aby uzyskać więcej informacji na temat wersji 2.0, zobacz [Interfejs wiersza polecenia platformy Azure 2.0 jest ogólnie dostępny](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).

## <a name="set-up-hello-azure-cli"></a>Konfigurowanie hello wiersza polecenia platformy Azure

Witaj tooinstall wiersza polecenia platformy Azure, wykonaj kroki hello opisane w [hello instalowanie interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli.md).

> [!TIP]
> Firma Microsoft zaleca się zaktualizowanie instalacji interfejsu wiersza polecenia Azure często tootake zalet usługi aktualizacji i ulepszeń.
> 
> 

## <a name="command-help"></a>Pomoc związana z poleceniami

Tekst pomocy dla każdego polecenia można wyświetlić w hello Azure CLI, dodając `-h` toohello polecenia. Pomiń wszelkie inne opcje. Na przykład:

* tooget pomocy hello `az` polecenia, wpisz:`az -h`
* tooget listę wszystkich poleceń partii w hello interfejsu wiersza polecenia, należy użyć:`az batch -h`
* tooget informacje na temat tworzenia konta usługi partia zadań, wprowadź:`az batch account create -h`

W razie wątpliwości, użyj hello `-h` opcji wiersza polecenia tooget pomocy dotyczącej polecenia wiersza polecenia platformy Azure.

> [!NOTE]
> Starsze niż hello Azure CLI używane `azure` toopreface polecenia interfejsu wiersza polecenia. W wersji 2.0 wszystkie polecenia są teraz poprzedzane opcją `az`. Można się tooupdate Twojego skrypty toouse hello nowej składni w wersji 2.0.
>
>  

Ponadto, zapoznaj się z dokumentacją odwołanie do wiersza polecenia platformy Azure toohello szczegółowe informacje o [polecenia wiersza polecenia platformy Azure dla partii](https://docs.microsoft.com/cli/azure/batch). 

## <a name="log-in-and-authenticate"></a>Logowanie i uwierzytelnianie

Witaj toouse wiersza polecenia platformy Azure z partii, należy toolog w i uwierzytelniania. Istnieją dwa toofollow prostych kroków:

1. **Zaloguj się na platformie Azure.** Logowanie do platformy Azure zapewnia dostęp tooAzure poleceń Menedżera zasobów, w tym [usługi zarządzania partii](batch-management-dotnet.md) poleceń.  
2. **Zaloguj się na koncie usługi Batch.** Logowanie do sieci zapewnia konta wsadowego dostęp do poleceń usługi tooBatch.   

### <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Istnieje kilka różnych sposobów toolog na platformie Azure, opisano szczegółowo w [Zaloguj się za pomocą usługi Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):

1. [Logowanie interakcyjne](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in). Zaloguj się interaktywnie po uruchomieniu polecenia interfejsu wiersza polecenia Azure samodzielnie hello wiersza polecenia.
2. [Logowanie za pomocą jednostki usługi](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal). Zaloguj się za pomocą jednostki usługi, gdy uruchamiasz polecenia interfejsu wiersza polecenia platformy Azure za pomocą skryptu lub aplikacji.

Dla celów hello w tym artykule, zostanie przedstawiony sposób toolog na platformie Azure interaktywnie. Typ [logowania az](https://docs.microsoft.com/cli/azure/#login) hello w wierszu polecenia:

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

Witaj `az login` polecenie zwraca token można użyć tooauthenticate, jak pokazano poniżej. Wykonaj hello instrukcjami tooopen strony sieci web i przesyłanie hello token tooAzure:

![Zaloguj się za tooAzure](./media/batch-cli-get-started/az-login.png)

Przykłady Hello na liście hello [przykładowe skrypty powłoki](#sample-shell-scripts) sekcji również Pokaż jak toostart sesję wiersza polecenia platformy Azure przez interakcyjnego logowania się do platformy Azure. Po zalogowaniu, można wywołać polecenia toowork z zasobów usługi partia zadań zarządzania, w tym konta wsadowego, kluczy, pakiety aplikacji i przydziały.  

### <a name="log-in-tooyour-batch-account"></a>Zaloguj się za tooyour konta usługi partia zadań

toouse hello Azure CLI toomanage partii zasoby, takie jak pule, zadań i zadań, należy toolog do konta partii zadań i uwierzytelniania. toolog w toohello usługa partia zadań, użyj hello [logowania konta wsadowego az](https://docs.microsoft.com/cli/azure/batch/account#login) polecenia. 

Dostępne są dwie opcje uwierzytelnienia na koncie usługi Batch:

- **Przy użyciu uwierzytelniania usługi Azure Active Directory (Azure AD).** 

    Uwierzytelniania w usłudze Azure AD jest hello domyślną, gdy użytkownik korzysta z partii hello wiersza polecenia platformy Azure i zalecane w przypadku większości scenariuszy. 
    
    Po zalogowaniu tooAzure interaktywnego, zgodnie z opisem w poprzedniej sekcji hello, poświadczenia są buforowane, dlatego hello wiersza polecenia platformy Azure można Cię zalogować w tooyour przy użyciu tych samych poświadczeń konta usługi partia zadań. Jeśli logujesz się przy użyciu nazwy głównej usługi tooAzure, te poświadczenia są również toolog używanych w tooyour konta usługi partia zadań.

    Przewagą wynikającą z korzystania z usługi Azure AD jest to, że zapewnia ona kontrolę dostępu opartą na rolach. Z RBAC dostępu użytkownika zależy od przypisanej roli, zamiast czy posiadają hello klucze konta. Zamiast zarządzać kluczami konta, można zarządzać rolami kontroli dostępu opartej na rolach oraz obsługiwać dostęp i uwierzytelnianie w usłudze Azure AD.  

    Uwierzytelnianie w usłudze Azure AD jest wymagany, jeśli utworzono kontem usługi partia zadań Azure za pomocą trybu alokacji puli ustawić too'User subskrypcji ". 

    toolog w tooyour partii konta za pomocą usługi Azure AD, należy wywołać hello [logowania konta wsadowego az](https://docs.microsoft.com/cli/azure/batch/account#login) polecenia: 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- **Przy użyciu uwierzytelniania klucza wspólnego.**

    [Uwierzytelniania klucza współużytkowanego](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) usługi partii używa polecenia interfejsu wiersza polecenia Azure tooauthenticate hello kluczy dostępu do Twojego konta.

    W przypadku tworzenia skryptów wiersza polecenia platformy Azure tooautomate wywoływania pliki wsadowe, można użyć klucza wspólnego uwierzytelniania lub nazwy głównej usługi Azure AD. W niektórych przypadkach użycie uwierzytelniania klucza wspólnego może być łatwiejsze niż tworzenie jednostki usługi.  

    toolog za pomocą uwierzytelniania klucza wspólnego obejmują hello `--shared-key-auth` opcji hello w wierszu polecenia:

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

Przykłady Hello na liście hello [przykładowe skrypty powłoki](#sample-shell-scripts) sekcja wskazuje, jak toolog do konta partii zadań z hello Azure CLI jednoczesnego używania usługi Azure AD i klucz wstępny.

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Korzystanie z szablonów interfejsu wiersza polecenia usługi Azure Batch i transferu plików (wersja zapoznawcza)

Hello Azure CLI toorun partii zadań end-to-end można użyć bez pisania kodu. Pliki szablonów partii obsługuje tworzenia pul, zadań i zadania związane z hello wiersza polecenia platformy Azure. Można również użyć plików wejściowych hello Azure CLI tooupload zadania konta usługi Azure Storage toohello skojarzonego z hello konto usługi partia zadań i pobierane pliki wyjściowe zadania. Więcej informacji można znaleźć w temacie [Use Azure Batch CLI Templates and File Transfer (Preview) (Korzystanie z szablonów interfejsu wiersza polecenia usługi Azure Batch i transferu plików (wersja zapoznawcza))](batch-cli-templates.md).

## <a name="sample-shell-scripts"></a>Przykładowe skrypty powłoki

Hello przykładowe skrypty na liście powitania po Pokaż tabeli jak polecenia toouse wiersza polecenia platformy Azure z hello usługa partia zadań i zarządzania partii usługi tooaccomplish typowych zadań. Te przykładowe skrypty obejmują wiele poleceń hello dostępne w hello wiersza polecenia platformy Azure dla partii. 

| Skrypt | Uwagi |
|---|---|
| [Tworzenie konta usługi Batch](./scripts/batch-cli-sample-create-account.md) | Tworzy konto usługi Batch i kojarzy je z kontem magazynu. |
| [Dodawanie aplikacji](./scripts/batch-cli-sample-add-application.md) | Dodaje aplikację i przekazuje spakowane dane binarne.|
| [Zarządzanie pulami usługi Batch](./scripts/batch-cli-sample-manage-pool.md) | Ilustruje tworzenie pul, zmienianie ich rozmiarów i zarządzanie nimi. |
| [Uruchamianie zadań i zadań podrzędnych za pomocą usługi Batch](./scripts/batch-cli-sample-run-job.md) | Ilustruje uruchamianie zadania i dodawanie zadania podrzędnego. |

## <a name="json-files-for-resource-creation"></a>Pliki JSON do tworzenia zasobów

Podczas tworzenia partii zasobów, takich jak pule i zadań, można określić plik JSON zawierający konfigurację hello nowy zasób zamiast przekazywanie jego parametrów jako opcje wiersza polecenia. Na przykład:

```azurecli
az batch pool create my_batch_pool.json
```

Można tworzyć najwięcej zasobów partii, używając tylko opcji wiersza polecenia, niektóre funkcje wymagają, aby określić plik w formacie JSON zawierający szczegóły zasobu hello. Należy na przykład użyć pliku JSON, pliki zasobów toospecify na zadanie uruchamiania.

Witaj toosee składni JSON wymagane toocreate zasobu, można znaleźć toohello [dokumentacji interfejsu API REST partii] [ rest_api] dokumentacji. Każdy "Dodaj *typu zasobu*" tematu w dokumentacji interfejsu API REST hello zawiera przykładowe skrypty JSON do tworzenia tego zasobu. Te przykładowe skrypty JSON można użyć jako szablon dla toouse pliki JSON z hello wiersza polecenia platformy Azure. Na przykład hello toosee składni JSON tworzenie puli, można znaleźć zbyt[dodać konto puli tooan][rest_add_pool].

Aby uzyskać przykładowy skrypt określający plik JSON, zobacz [Uruchamianie zadań i zadań podrzędnych za pomocą usługi Batch](./scripts/batch-cli-sample-run-job.md).

> [!NOTE]
> Jeśli określisz pliku JSON, podczas tworzenia zasobu, są ignorowane parametrów określone na powitania wiersza polecenia dla tego zasobu.
> 
> 

## <a name="efficient-queries-for-batch-resources"></a>Wydajne zapytania dotyczące zasobów usługi Batch

Każdy typ zasobu usługi Batch obsługuje polecenie `list`, które wysyła zapytania do konta usługi Batch i wyświetla listę zasobów tego typu. Na przykład można wyświetlić listę pul hello w zadaniach w ramach zadania konta i hello:

```azurecli
az batch pool list
az batch task list --job-id job001
```

Gdy zapytanie usługi partia zadań hello z `list` operacji można określić OData klauzuli toolimit hello ilości zwracanych danych. Ponieważ wszystkie filtrowania odbywa się po stronie serwera, hello tylko te dane, które możesz poprosić przecina hello danych przesyłanych w sieci. Użyj tych przepustowości toosave klauzule (i w związku z tym czas) po wykonaniu operacji na liście.

Witaj poniższej tabeli opisano hello klauzule OData obsługiwany przez hello usługa partia zadań:

| Klauzula | Opis |
|---|---|
| `--select-clause [select-clause]` | Zwracanie podzbioru właściwości dla każdej jednostki. |
| `--filter-clause [filter-clause]` | Zwraca tylko jednostki, które pasują hello określone wyrażenie OData. |
| `--expand-clause [expand-clause]` | Pobiera informacje jednostki hello w pojedynczym wywołaniu elementu źródłowego REST. Witaj rozwiń klauzuli aktualnie obsługuje tylko hello `stats` właściwości. |

Na przykład skryptu pokazujący toouse klauzula OData, zobacz temat [uruchomienie zadania i zadania z partii](./scripts/batch-cli-sample-run-job.md).

Aby uzyskać więcej informacji dotyczących wykonywania zapytania wydajne listy z klauzulami OData, zobacz [wydajnie zapytania usługi partia zadań Azure hello](batch-efficient-list-queries.md).

## <a name="troubleshooting-tips"></a>Wskazówki dotyczące rozwiązywania problemów

Witaj Poniższe porady mogą pomóc przy rozwiązywaniu problemów z wiersza polecenia platformy Azure:

* Użyj `-h` tooget **tekst pomocy** dla dowolnego polecenia interfejsu wiersza polecenia
* Użyj `-v` i `-vv` toodisplay **pełne** danych wyjściowych polecenia. Gdy hello `-vv` flaga jest dołączony, hello Azure CLI Wyświetla hello rzeczywiste REST żądań i odpowiedzi. Te przełączniki są przydatne do wyświetlania pełnych danych wyjściowych błędu.
* Możesz wyświetlić **polecenia danych wyjściowych w formacie JSON** z hello `--json` opcji. Przykładowo polecenie `az batch pool show pool001 --json` wyświetla właściwości puli 001 w formacie JSON. Możesz skopiować i zmodyfikuj ten toouse danych wyjściowych w `--json-file` (zobacz [pliki w formacie JSON](#json-files) wcześniej w tym artykule).
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* Witaj [forum usługi partia zadań] [ batch_forum] monitorują członkowie zespołu partii. Możesz tam zamieszczać pytania w przypadku napotkania problemów lub w sytuacji, w której potrzebujesz pomocy z konkretną operacją.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji na temat hello wiersza polecenia platformy Azure, zobacz hello [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).
* Aby uzyskać więcej informacji o zasobach usługi Batch, zobacz [Omówienie usługi Azure Batch dla deweloperów](batch-api-basics.md).
* Aby uzyskać więcej informacji o używaniu pule toocreate szablony, zadań i zadania wsadowego bez pisania kodu, zobacz [szablony interfejsu wiersza polecenia usługi partia zadań Azure Użyj i transferu plików (wersja zapoznawcza)](batch-cli-templates.md).

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
