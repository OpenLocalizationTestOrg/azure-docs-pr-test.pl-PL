---
title: "aaaAzure szyfrowanie usługi Magazyn przy użyciu klienta zarządzane klucze w usłudze Azure Key Vault | Dokumentacja firmy Microsoft"
description: "Użyj usługi magazynu obiektów Blob Azure tooencrypt funkcji szyfrowanie usługi Magazyn Azure powitania po stronie usługi hello podczas zapisywania danych hello i go odszyfrować podczas pobierania danych hello przy użyciu klienta zarządzanych kluczy."
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: 870cae2f258b356aa234f8bba65a023ac389be10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Szyfrowanie usługi Magazyn przy użyciu klienta zarządzane klucze w usłudze Azure Key Vault

Microsoft Azure jest silnie zatwierdzone toohelping ochrony i chronić Twoje toomeet danych organizacji bezpieczeństwa i zgodności zobowiązań.  Jednym ze sposobów może chronić dane w stanie spoczynku jest toouse magazynu usługi szyfrowania (SSE), które automatycznie szyfruje dane podczas jej pisania toostorage i odszyfrowuje dane podczas pobierania go. Witaj szyfrowania i odszyfrowywania jest automatyczne i całkowicie niewidoczne i używa 256-bitowego [szyfrowania AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), jednego bloku najwyższy hello szyfrów dostępne.

Klucze szyfrowania zarządzany przez firmę Microsoft można używać z SSE lub skorzystać z kluczy szyfrowania. W tym artykule zostaną omówione hello później. Aby uzyskać więcej informacji o korzystaniu z kluczy zarządzany przez firmę Microsoft, lub SSE ogólnie, zobacz [szyfrowanie usługi Magazyn danych magazynowanych](storage-service-encryption.md).

toouse możliwości hello tooprovide własnych kluczy szyfrowania SSE dla magazynu obiektów Blob jest zintegrowany z magazynu kluczy Azure (AKV). Można utworzyć kluczy szyfrowania i przechowywać je w AKV lub za pomocą kluczy szyfrowania toogenerate interfejsów API firmy AKV. Nie tylko AKV pozwalają toomanage i kontrolować klucze, umożliwia również należy tooaudit użycie klucza. 

Dlaczego chcesz toocreate własne klucze? Zapewnia większą elastyczność, w tym toocreate możliwości hello, obracanie, wyłącz i zdefiniować kontroli dostępu i tooaudit hello szyfrowania kluczy używanych tooprotect dane.

## <a name="sse-with-customer-managed-keys-preview"></a>SSE z customer preview zarządzanych kluczy

Ta funkcja jest obecnie dostępna w wersji zapoznawczej. toouse tej funkcji, należy toocreate nowe konto magazynu. Możesz utworzyć nowego magazynu kluczy oraz klucz lub użyć istniejącego magazynu kluczy oraz klucz. Konto magazynu Hello i hello magazynu kluczy musi należeć do hello tego samego regionu, ale może znajdować się w różnych subskrypcji.

Skontaktuj się z pomocą tooparticipate w wersji zapoznawczej hello [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com). Firma Microsoft udostępni tooparticipate linku w wersji zapoznawczej hello.

toolearn więcej, zobacz toohello [— często zadawane pytania](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).

> [!IMPORTANT]
> Możesz zarejestrować się, aby hello Podgląd wcześniejsze toofollowing hello opisanych w tym artykule. Bez dostępu do wersji zapoznawczej, nie będzie można tooenable stanie tej funkcji w portalu hello.

## <a name="getting-started"></a>Wprowadzenie
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Krok 1: [Utwórz nowe konto magazynu](storage-create-storage-account.md)

## <a name="step-2-enable-encryption"></a>Krok 2: Włączanie szyfrowania
Można włączyć SSE hello konto magazynu przy użyciu hello [portalu Azure](https://portal.azure.com). W bloku ustawienia hello hello konta magazynu Wyszukaj hello sekcji usługi obiektów Blob, jak pokazano na rysunku poniżej, a następnie kliknij przycisk szyfrowania.

![Opcja szyfrowania portalu zrzut ekranu przedstawiający](./media/storage-service-encryption/image1.png)
<br/>*Włącz SSE dla usługi Blob*

Jeśli chcesz tooprogrammatically Włącz lub wyłącz hello szyfrowanie usługi Magazyn na koncie magazynu, można użyć hello [interfejsu API REST dostawcy zasobów magazynu Azure](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), hello [biblioteki klienta dostawcy zasobów magazynu dla platformy .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [programu Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), lub hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).

Na tym ekranie Jeśli nie jest widoczne pole wyboru "Użyj własnego klucza" hello, możesz nie zostały zatwierdzone hello podglądu. Wyślij wiadomość e-mail jest zbyt[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) i zażądać zatwierdzenia.

![Portal zrzut ekranu przedstawiający podgląd szyfrowania](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

Domyślnie SSE użyje klucze zarządzany przez firmę Microsoft. toouse własne klucze hello pole wyboru. Następnie można określić klucz identyfikatora URI, lub wybierać selektora hello klucza i magazyn kluczy.

## <a name="step-3-select-your-key"></a>Krok 3: Wybierz klucz

![Portal zrzut ekranu przedstawiający szyfrowania opcja własnego klucza](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![Portalu zrzut ekranu przedstawiający szyfrowania z wprowadź identyfikator uri klucza opcji](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

Hello konta magazynu nie ma dostępu toohello Key Vault, można uruchomić hello następujące polecenie, używając programu Azure Powershell toogrant dostępu toohello magazynu kont toohello wymagane magazynu kluczy.

![Portal zrzut ekranu przedstawiający odmowa dostępu do magazynu kluczy](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

Można również przyznać dostęp za pośrednictwem portalu Azure hello przechodząc toohello usługi Azure Key Vault w portalu Azure hello i udzielanie dostępu toohello magazynu konta.

## <a name="step-4-copy-data-toostorage-account"></a>Krok 4: Skopiowanie danych toostorage konta
Jeśli chcesz tootransfer danych do nowego konta magazynu, dzięki czemu jest on zaszyfrowany, można znaleźć zbyt[krok 3 z wprowadzenie w szyfrowanie usługi Magazyn danych magazynowanych](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a>Krok 5: Hello kwerenda o stan hello zaszyfrowanych danych
Stan hello tooquery hello zaszyfrowanych danych można znaleźć zbyt[kroku 4 z wprowadzenie w szyfrowanie usługi Magazyn danych magazynowanych](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Często zadawane pytania dotyczące szyfrowanie usługi Magazyn danych w stanie spoczynku
**Pytanie: czy używany Magazyn w warstwie Premium; z kluczami zarządzanego klienta można używać SSE?**

A: tak, SSE z zarządzanego przez firmę Microsoft i klientów zarządzanych kluczy jest obsługiwany w standardowych magazynu i Magazyn w warstwie Premium. 

**Pytanie: czy można utworzyć nowego konta magazynu z SSE z kluczami klientów zarządzanych włączyć za pomocą programu Azure PowerShell i interfejsu wiersza polecenia Azure?**

Odpowiedź: tak.

**Pytanie: jak dużo więcej pojawia się koszt usługi Azure Storage SSE klientowi zarządzanych kluczy jest włączone?**

Odpowiedź: Brak koszt skojarzony przy użyciu usługi Azure Key Vault. Więcej informacji można znaleźć [klucza magazynu cennik](https://azure.microsoft.com/en-us/pricing/details/key-vault/). Nie ma żadnych dodatkowych kosztów stosowania SSE.

**Pytanie: czy mogę Odwołaj klucze szyfrowania toohello dostępu?**

Odpowiedź: tak, w dowolnym momencie można odwołać dostęp. Istnieje kilka sposobów toorevoke dostępu tooyour kluczy. Zobacz zbyt[PowerShell magazynu kluczy Azure](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) i [interfejsu wiersza polecenia Azure Key Vault](https://docs.microsoft.com/en-us/cli/azure/keyvault) więcej szczegółów. Odbieranie prawa dostępu skutecznie blokuje dostęp do obiektów blob tooall na koncie magazynu hello hello konta klucz szyfrowania jest niedostępne dla magazynu Azure.

**Pytanie: czy można utworzyć konta magazynu i klucza w innym regionie?**

Odpowiedź: nie hello konto magazynu i klucza/magazynu kluczy muszą toobe w hello tego samego regionu. 

**Pytanie: czy można włączyć SSE z klientów zarządzanych kluczy podczas tworzenia konta magazynu hello?**

Odpowiedź: nie. Po włączeniu SSE podczas tworzenia konta magazynu hello można używać tylko klucze zarządzany przez firmę Microsoft. Jeśli chcesz toouse klienta zarządzania kluczami należy właściwości konta magazynu hello tooupdate. Można użyć REST lub jeden z tooprogrammatically biblioteki klienta magazynu hello zaktualizować konta magazynu lub właściwości konta magazynu hello przy użyciu portalu Azure hello po utworzeniu konta hello.

**Pytanie: czy szyfrowanie można wyłączyć podczas z klienta przy użyciu SSE zarządzane klucze?**

A: nie, nie można wyłączyć szyfrowania, gdy z klienta przy użyciu SSE zarządzanych kluczy. szyfrowanie toodisable, konieczne będzie tooswitch toousing zarządzany przez firmę Microsoft kluczy. Można to zrobić za pomocą hello portalu Azure lub programu PowerShell.

**Pytanie: jest SSE domyślnie włączona, tworząc nowe konto magazynu?**

Odpowiedź: SSE nie jest włączona domyślnie; Witaj tooenable portalu Azure można użyć go. Można również programowo włączyć tę funkcję za pomocą interfejsu API REST dostawcy zasobów magazynu hello. 

**Pytanie: nie można włączyć szyfrowanie na moim koncie magazynu.**

A: to konto magazynu Resource Manager? Klasycznych kont magazynu nie są obsługiwane. SSE z kluczami klientów zarządzanych także można włączyć tylko na nowo utworzonych kont magazynu Menedżera zasobów.

**Pytanie: SSE jest klientowi zarządzane klucze dozwolone tylko w określonych regionach?**

Odpowiedź: SSE jest dostępny w tylko niektóre regiony dla magazynu obiektów Blob dla tej wersji zapoznawczej. Wyślij wiadomość e-mail [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck dostępności i szczegółowe informacje o wersji zapoznawczej. 

**Pytanie: jak można skontaktować się z osobą czy wystąpienia jakichkolwiek problemów lub mają tooprovide opinii?**

Odpowiedź: Skontaktuj się z pomocą [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) problemów związanych z tooStorage usługi szyfrowania. 

## <a name="next-steps"></a>Następne kroki

*   Aby uzyskać więcej informacji na powitania rozbudowany zestaw zabezpieczeń możliwości, które ułatwiają deweloperom tworzenie bezpiecznych aplikacji, zobacz hello [przewodnik zabezpieczeń magazynu](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).
*   Aby uzyskać przegląd informacji dotyczących usługi Azure Key Vault, zobacz [co to jest usługa Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)?
*   W ramach wprowadzenia usługi Azure Key Vault, zobacz [wprowadzenie do korzystania z usługi Azure Key Vault](../key-vault/key-vault-get-started.md).
