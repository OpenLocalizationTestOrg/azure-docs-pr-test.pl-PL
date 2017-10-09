---
title: "aaaConfigure niestandardowej nazwy domeny dla punktu końcowego magazynu obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Użyj hello toomap portalu Azure własne końcowego magazynu obiektów Blob toohello nazwę kanoniczną (CNAME) dla konta usługi Azure Storage."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: 6cca6a6e1dbb69e7078df7ed11b04e8b921ec2f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a>Konfigurowanie niestandardowej nazwy domeny dla punktu końcowego usługi Blob Storage

Można skonfigurować niestandardową domenę na potrzeby uzyskiwania dostępu do danych obiektów blob na koncie magazynu Azure. Witaj domyślnego punktu końcowego magazynu obiektów Blob jest `<storage-account-name>.blob.core.windows.net`. Jeśli mapujesz niestandardowych domen i poddomen, takich jak **www.contoso.com** toohello punktu końcowego obiektu blob dla konta magazynu, użytkowników może uzyskać dostęp obiektu blob danych na koncie magazynu przy użyciu tej domeny.

> [!IMPORTANT]
> Usługa Azure Storage jeszcze natywnie obsługuje HTTPS z domen niestandardowych. Obecnie można [użyć hello Azure CDN tooaccess blob z domenami niestandardowymi za pośrednictwem protokołu HTTPS](./storage-https-custom-domain-cdn.md).
>

Witaj poniższej tabeli przedstawiono kilka przykładowych adresy URL obiektu blob danych znajdujących się na koncie magazynu o nazwie **mojekontomagazynu**. zarejestrowany Hello domeny niestandardowej dla konta magazynu hello jest **www.contoso.com**:

| Typ zasobu | Domyślny adres URL | Adres URL domeny niestandardowej |
| --- | --- | --- |
| Konto magazynu | http://mystorageaccount.blob.Core.Windows.NET | http://www.contoso.com |
| Obiekt blob |http://mystorageaccount.blob.Core.Windows.NET/mycontainer/myblob | http://www.contoso.com/mycontainer/myblob |
| Nadrzędny kontener | http://mystorageaccount.blob.Core.Windows.NET/myblob lub http://mystorageaccount.blob.core.windows.net/$ głównego/mojblob| http://www.contoso.com/myblob lub http://www.contoso.com/$ głównego/mojblob |

## <a name="direct-vs-intermediary-domain-mapping"></a>Bezpośrednie a mapowanie pośredniczące domeny

Istnieją dwa sposoby toopoint punktu końcowego obiektu blob toohello domeny niestandardowej dla konta magazynu: bezpośrednie CNAME mapping, a przy użyciu hello *asverify* pośredniczące poddomeny.

### <a name="direct-cname-mapping"></a>Bezpośrednie mapowanie CNAME

Hello pierwszy i najprostszym, metoda jest toocreate rekordu nazwę kanoniczną (CNAME), który mapuje Twoje niestandardowe domen i poddomen bezpośrednio toohello obiektu blob punktu końcowego. Rekord CNAME jest funkcją systemu (nazw domen DNS) nazwa domeny, która mapuje domeny docelowej tooa domeny źródłowej. W takim przypadku domeny źródłowej hello jest własnych niestandardowych domen i poddomen, na przykład *www.contoso.com*. domena docelowego hello jest punktu końcowego usługi Blob, na przykład  *mystorageaccount.blob.Core.Windows.NET*.

Metoda bezpośrednia Hello jest objęte [zarejestrować niestandardową domenę](#register-a-custom-domain).

### <a name="intermediary-mapping-with-asverify"></a>Mapowanie pośredniczące *asverify*

Druga metoda Hello używa również rekordy CNAME, ale najpierw wykorzystuje specjalne poddomeny rozpoznaje Azure tooavoid przestój: **asverify**.

Proces mapowania punktu końcowego obiektu blob tooa domeny niestandardowej Hello może spowodować przez krótki czas przestoju dla domeny hello podczas rejestrowania jej w hello [portalu Azure](https://portal.azure.com). Jeśli aktualnie obsługiwanych aplikacji przy użyciu umowy poziomu usług (SLA) wymaga przestojów domenę niestandardową, a następnie można użyć hello Azure *asverify* poddomeny jako etap pośredni rejestracji. Ten krok pośredniego zapewnia użytkownikom są stanie tooaccess domeny, podczas gdy hello mapowanie DNS ma miejsce.

Metoda pośredniczące Hello jest objęte [zarejestrować niestandardową domenę przy użyciu hello *asverify* poddomeny](#register-a-custom-domain-using-the-asverify-subdomain).

## <a name="register-a-custom-domain"></a>Zarejestruj domeny niestandardowej
Korzystania z niestandardowej domeny tooregister tej procedury, jeśli nie pytań dotyczących domeny hello trwa krótko niedostępny tooyour użytkowników lub domeny niestandardowej nie jest obecnie hostuje aplikację.

W przypadku domeny niestandardowej jest obecnie obsługi aplikacji, która nie może mieć żadnych przestojów, wykonaj procedurę hello opisane w temacie [zarejestrować niestandardową domenę przy użyciu hello *asverify* poddomeny](#register-a-custom-domain-using-the-asverify-subdomain).

tooconfigure niestandardowej nazwy domeny, należy utworzyć nowy rekord CNAME w systemie DNS. rekord CNAME Hello określa aliasu dla nazwy domeny. W takim przypadku mapuje hello adres Twojej domeny niestandardowej toohello obiektu Blob magazynu punktu końcowego dla konta magazynu.

Zazwyczaj można zarządzać ustawieniami DNS domeny w witrynie rejestratora domen. Każdy rejestrator ma podobne, lecz nieco inne metody określania rekord CNAME, ale koncepcji hello jest hello takie same. Niektóre pakiety rejestracji podstawowe domeny nie oferują konfiguracji DNS może więc być konieczny tooupgrade pakietu rejestracji domeny można było utworzyć rekord CNAME hello.

1. Przejdź do konta magazynu tooyour w hello [portalu Azure](https://portal.azure.com).
1. W obszarze **usługa BLOB** na powitania bloku menu, wybierz **domeny niestandardowe** tooopen hello *domeny niestandardowe* bloku.
1. Zaloguj się na rejestratora domen tooyour witryny sieci Web i przejdź do strony toohello zarządzania DNS. Może ona być zlokalizowana w sekcjach, takich jak **Domain Name** (Nazwa domeny), **DNS** (System DNS) lub **Name Server Management** (Zarządzanie serwerem nazw).
1. Znajdź sekcję hello zarządzania CNAME. Może mieć toogo tooan Zaawansowane ustawienia strony i wyszukaj słowa hello **CNAME**, **Alias**, lub **poddomen**.
1. Utwórz nowy rekord CNAME i podaj alias poddomeny, takie jak **www** lub **zdjęć**. Następnie podaj nazwę hosta, który jest punkt końcowy usługi Blob, w formacie hello **mystorageaccount.blob.core.windows.net** (gdzie *mojekontomagazynu* hello nazwa konta magazynu). toouse nazwy hosta Hello pojawia się w elemencie #1 hello *domeny niestandardowe* bloku w hello [portalu Azure](https://portal.azure.com).
1. W polu tekstowym hello na powitania *domeny niestandardowe* bloku w hello [portalu Azure](https://portal.azure.com), wprowadź nazwę domeny niestandardowej, łącznie z poddomeny hello hello. Na przykład, jeśli Twoja domena to **contoso.com** i aliasu poddomeny **www**, wprowadź **www.contoso.com**. Jeśli Twoje domeny podrzędnej jest **zdjęć**, wprowadź **photos.contoso.com**. poddomeny hello jest *wymagane*.
1. Wybierz **zapisać** na powitania *domeny niestandardowe* tooregister bloku domeny niestandardowej. Jeśli hello rejestracja zakończy się pomyślnie, zostanie wyświetlone powiadomienie portalu Twoje konto magazynu zostało pomyślnie zaktualizowane.

Po Twoje nowy rekord CNAME zakończeniem propagacji przy użyciu systemu DNS, użytkownicy mogą wyświetlać dane obiektów blob przy użyciu domenę niestandardową, tak długo, jak długo mają odpowiednie uprawnienia hello.

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a>Zarejestruj niestandardową domenę przy użyciu hello *asverify* poddomeny
Użyj tej procedury tooregister domeny niestandardowej w przypadku domeny niestandardowej jest obecnie obsługi aplikacji z umowy dotyczącej poziomu usług, które wymaga, aby nie istnieć bez przestojów. Przez utworzenie rekordu CNAME, który wskazuje z `asverify.<subdomain>.<customdomain>` zbyt`asverify.<storageaccount>.blob.core.windows.net`, można wstępnie zarejestrować domeny z platformy Azure. Następnie możesz utworzyć drugi CNAME, który wskazuje z `<subdomain>.<customdomain>` zbyt`<storageaccount>.blob.core.windows.net`, w takim przypadku domeny niestandardowej tooyour ruch będzie ukierunkowanej tooyour punkt końcowy blob.

Witaj **asverify** poddomeny jest specjalne poddomenę rozpoznawane przez platformę Azure. Przez dołączanie `asverify` tooyour własnych poddomeny, należy zezwolić na działanie Azure toorecognize domeny niestandardowej bez modyfikowania hello rekordu DNS dla domeny hello. Po zmodyfikowaniu hello rekordu DNS dla domeny hello będzie punktu końcowego obiektu blob toohello mapowane bez przestojów.

1. Przejdź do konta magazynu tooyour w hello [portalu Azure](https://portal.azure.com).
1. W obszarze **usługa BLOB** na powitania bloku menu, wybierz **domeny niestandardowe** tooopen hello *domeny niestandardowe* bloku.
1. Zaloguj się na dostawcy DNS tooyour witryny sieci Web i przejdź do strony toohello zarządzania DNS. Może ona być zlokalizowana w sekcjach, takich jak **Domain Name** (Nazwa domeny), **DNS** (System DNS) lub **Name Server Management** (Zarządzanie serwerem nazw).
1. Znajdź sekcję hello zarządzania CNAME. Może mieć toogo tooan Zaawansowane ustawienia strony i wyszukaj słowa hello **CNAME**, **Alias**, lub **poddomen**.
1. Utwórz nowy rekord CNAME i podaj alias poddomeny, która obejmuje hello *asverify* poddomeny. Na przykład **asverify.www** lub **asverify.photos**. Następnie podaj nazwę hosta, który jest punkt końcowy usługi Blob, w formacie hello **asverify.mystorageaccount.blob.core.windows.net** (gdzie **mojekontomagazynu** hello nazwa konta magazynu). toouse nazwy hosta Hello pojawia się w elemencie #2 hello *domeny niestandardowe* bloku w hello [portalu Azure](https://portal.azure.com).
1. W polu tekstowym hello na powitania *domeny niestandardowe* bloku w hello [portalu Azure](https://portal.azure.com), wprowadź nazwę domeny niestandardowej, łącznie z poddomeny hello hello. Nie dołączaj *asverify*. Na przykład, jeśli Twoja domena to **contoso.com** i aliasu poddomeny **www**, wprowadź **www.contoso.com**. Jeśli Twoje domeny podrzędnej jest **zdjęć**, wprowadź **photos.contoso.com**. poddomeny hello jest wymagana.
1. Wybierz hello **Użyj pośredniej weryfikacji CNAME** wyboru.
1. Wybierz **zapisać** na powitania *domeny niestandardowe* tooregister bloku domeny niestandardowej. Jeśli rejestracja hello zakończy się pomyślnie, zobaczysz portalu powiadomienie, że Twoje konto magazynu zostało pomyślnie zaktualizowane. W tym momencie domeny niestandardowej została zweryfikowana przez platformę Azure, ale ruch tooyour domena nie jest jeszcze rozsyłane tooyour konta magazynu.
1. Zwraca dostawcy DNS tooyour witryny sieci Web i utwórz inny rekord CNAME mapujący punktu końcowego usługi Blob tooyour poddomeny. Na przykład określić poddomeny hello jako **www** lub **zdjęć** (bez hello *asverify*), a hello hostname jako  **mystorageaccount.blob.Core.Windows.NET** (gdzie **mojekontomagazynu** hello nazwa konta magazynu). W ramach tego kroku rejestracji hello domeny niestandardowej jest ukończona.
1. Na koniec możesz usunąć rekord CNAME hello utworzone zawierającego hello **asverify** poddomeny, ponieważ było konieczne tylko jako etap pośredniczące.

Po Twoje nowy rekord CNAME zakończeniem propagacji przy użyciu systemu DNS, użytkownicy mogą wyświetlać dane obiektów blob przy użyciu domenę niestandardową, tak długo, jak długo mają odpowiednie uprawnienia hello.

## <a name="test-your-custom-domain"></a>Testowanie domenę niestandardową

tooconfirm domeny niestandardowej jest w rzeczywistości zamapowany tooyour punkt końcowy usługi Blob, Utwórz obiekt blob w kontenerze publicznym w ramach konta magazynu. Następnie w przeglądarce sieci web w hello następującego formatu tooaccess hello blob korzystania z identyfikatora URI:

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

Na przykład może użyć następującego identyfikatora URI tooaccess formularza sieci web w hello hello **myforms** kontenera w hello **photos.contoso.com** poddomeny niestandardowych:

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a>Wyrejestrowania domeny niestandardowej

tooderegister domeny niestandardowej dla punktu końcowego magazynu obiektów Blob, użyj jednej z hello zgodnie z procedurami.

### <a name="azure-portal"></a>Azure Portal

Wykonaj następujące hello w ustawieniu domena niestandardowa hello tooremove portalu Azure hello:

1. Przejdź do konta magazynu tooyour w hello [portalu Azure](https://portal.azure.com).
1. W obszarze **usługa BLOB** na powitania bloku menu, wybierz **domeny niestandardowe** tooopen hello *domeny niestandardowe* bloku.
1. Wyczyść hello zawartości pola tekstowego hello zawierający niestandardową nazwę domeny.
1. Wybierz hello **zapisać** przycisku.

Domeny niestandardowe hello został pomyślnie usunięty, zobaczysz portalu powiadomienie, że Twoje konto magazynu zostało pomyślnie zaktualizowane.

### <a name="azure-cli-20"></a>Interfejs wiersza polecenia platformy Azure 2.0

Użyj hello [aktualizacja konta magazynu az](https://docs.microsoft.com/cli/azure/storage/account#update) interfejsu wiersza polecenia polecenia i określić ciąg pusty (`""`) dla hello `--custom-domain` tooremove wartość argumentu rejestracja domeny niestandardowej.

* Format polecenia:

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* Przykład polecenia:

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a>PowerShell

Użyj hello [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) polecenia cmdlet programu PowerShell i określ pusty ciąg (`""`) dla hello `-CustomDomainName` tooremove wartość argumentu rejestracja domeny niestandardowej.

* Format polecenia:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* Przykład polecenia:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a>Następne kroki
* [Mapowanie punktu końcowego Azure sieci dostarczania zawartości (CDN) tooan domeny niestandardowej](../cdn/cdn-map-content-to-custom-domain.md)
* [Używanie hello Azure CDN tooaccess blob z domenami niestandardowymi za pośrednictwem protokołu HTTPS](./storage-https-custom-domain-cdn.md)
