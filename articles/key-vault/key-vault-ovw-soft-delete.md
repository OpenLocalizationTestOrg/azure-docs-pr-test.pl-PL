---
ms.assetid: 
title: "usuwania nietrwałego aaaAzure Key Vault | Dokumentacja firmy Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a>Omówienie usługi Azure Key Vault soft-delete

Funkcja usuwania nietrwałego Key Vault umożliwia odzyskiwanie hello usunięte magazynów i magazynu obiektów, znany jako usuwania nietrwałego. W szczególności można rozwiązać hello następujące scenariusze:

- Obsługa możliwych do odzyskania usuwanie magazynu kluczy
- Obsługa możliwych do odzyskania usuwanie magazynu kluczy obiektów (np. klucze, klucze tajne certyfikatów)

## <a name="supporting-interfaces"></a>Obsługa interfejsów

Witaj funkcji usuwania nietrwałego jest początkowo dostępna za pośrednictwem hello REST, .NET / interfejsy C# i programu PowerShell. Odnoszą się odwołania toohello tych więcej szczegółów, [z informacjami o kluczach magazynu](https://docs.microsoft.com/azure/key-vault/).

## <a name="scenarios"></a>Scenariusze

Azure magazynów kluczy są śledzone zasoby zarządzanym przez Menedżera zasobów Azure. Usługa Azure Resource Manager określa również dobrze zdefiniowanego zachowania do usunięcia, co wymaga czy powodzenie operacji DELETE muszą dawać w wyniku tego zasobu nie nie jest już dostępny. adresy funkcji usuwania nietrwałego Hello hello odzyskiwania hello usunięty obiekt, czy usunięcie hello było przypadkowym lub zamierzone.

1. W hello typowy scenariusz użytkownik może przypadkowo usunięto magazyn kluczy lub obiekt magazynu kluczy; Jeśli tego klucza lub klucza magazynie magazyn obiektu zostały toobe możliwych do odzyskania przez okres ustalonej, hello użytkownika może cofnąć usunięcia hello i odzyskiwanie ich danych.

2. W przypadku różnych złośliwy użytkownik może podejmować toodelete magazynu kluczy lub obiektu magazynu kluczy, na przykład klucz w magazynie toocause zakłóceń biznesowych. Oddzielanie hello usuwanie magazynu kluczy hello lub obiekt magazynu kluczy z hello rzeczywiste usunięcie hello bazowy danych może służyć jako zabezpieczeniem, na przykład ograniczenie uprawnień na tooa usunięcia danych jest inny, Zaufane roli. Takie podejście efektywnie wymaga kworum dla danej operacji, które w przeciwnym razie może spowodować utratę danych bezpośrednim.

### <a name="soft-delete-behavior"></a>Zachowanie soft-delete

Przy użyciu tej funkcji hello operacji usuwania w magazynie kluczy lub obiekt magazynu kluczy jest soft-delete, efektywnie przytrzymując hello zasobów w danym okresie przechowywania danego nadanie hello wygląd obiektu hello jest usuwany. Dodatkowo usługa Hello udostępnia mechanizm odzyskiwanie hello usunięty obiekt zasadniczo cofanie usuwania hello. 

Usuwania nietrwałego jest opcjonalne zachowanie magazyn kluczy i **nie jest włączone domyślnie** w tej wersji. Szczegółowe informacje na temat włączania soft-delete dla magazynu kluczy, można znaleźć hello dokładne wskazówki w odwołaniu hello interfejsu hello wybranych [z informacjami o kluczach magazynu](https://docs.microsoft.com/azure/key-vault/).

### <a name="key-vault-recovery"></a>Magazyn kluczy odzyskiwania

Podczas usuwania magazynu kluczy, usługa hello tworzy zasób serwera proxy w ramach subskrypcji hello, dodawanie metadanych wystarczające do odzyskania. zasób proxy Hello jest przechowywane obiektu dostępne w hello tej samej lokalizacji co magazyn kluczy hello usunięte. 

### <a name="key-vault-object-recovery"></a>Odzyskiwanie obiektów magazynu kluczy

Podczas usuwania obiektu magazynu kluczy, na przykład klucz usługi hello umieści obiektu hello w stanie usunięty, co w związku z tym operacjami pobierania tooany niedostępny. W tym stanie obiektu magazynu kluczy hello może wystąpić tylko, odzyskana lub wymuszone/trwale usunięte. 

Na powitania sam czasie, klucza magazynu zaplanowane usunięcie hello hello bazowy toohello odpowiednich danych usunąć magazyn kluczy lub obiekt magazynu kluczy do wykonania po upływie czasu przechowywania wcześniej. Witaj DNS rekordów odpowiedni toohello magazyn także jest przechowywany dla długości hello okresu przechowywania hello.

### <a name="soft-delete-retention-period"></a>Okres przechowywania soft-delete

Elastyczne zasoby usunięte zostaną zachowane na wybrany okres czasu, w ciągu 90 dni. Przedział czasu przechowywania usuwania nietrwałego hello Zastosuj następujące hello:

- Może listę wszystkich magazynów kluczy hello i obiektów magazynu kluczy w stanie usuwania nietrwałego powitania dla Twojej subskrypcji, a także dostęp do usunięcia i odzyskiwania informacji o nich.
    - Tylko użytkownicy z uprawnieniami specjalne można wyświetlić listę usuniętych magazynów. Zaleca się naszych użytkowników utworzenie niestandardowej roli zabezpieczeń z odpowiednimi uprawnieniami specjalne magazynów Obsługa usunięta.
- Magazyn kluczy o tej samej nazwie, nie można utworzyć w hello hello tej samej lokalizacji. odpowiednio magazynu kluczy nie można utworzyć obiektu w danym magazynie Jeśli tego magazynu kluczy zawiera obiekt z hello tej samej nazwy i która jest w stanie usunięty 
- W szczególności uprzywilejowanych użytkownik może przywrócić magazynu kluczy lub obiekt magazynu kluczy wydając polecenie Odzyskaj na powitania odpowiadający jej zasób serwera proxy.
    - Użytkownik Hello członka hello niestandardową rolę, który ma toocreate uprawnień hello magazynu kluczy w grupie zasobów hello można przywrócić hello magazynu.
- Tylko użytkownik, w szczególności uprzywilejowanych może wymusić usuwanie magazynu kluczy lub obiektu magazynu kluczy wydając polecenie delete na powitania odpowiadający jej zasób serwera proxy.

Chyba, że magazyn kluczy lub obiekt magazynu kluczy zostanie przywrócona, koniec usługi hello interwał przechowywania hello na powitania wykonuje przeczyszczanie magazynu kluczy hello wszystkie usunięte nietrwale lub obiektu magazynu kluczy i jego zawartości. Nie może być zmienił jego usunięcia zasobu.

### <a name="permitted-purge"></a>Przeczyszczanie dozwolone

Trwałe usuwanie, usuwanie, magazyn kluczy jest możliwe za pośrednictwem operację POST na powitania serwera proxy zasobów i wymaga specjalnych uprawnień. Ogólnie rzecz biorąc tylko właściciel subskrypcji hello będą mogli toopurge magazynu kluczy. Wyzwalacze operacji POST Hello hello usunięcia natychmiastowe i nie można odzyskać tego magazynu. 

Wyjątek toothis sytuacja hello hello subskrypcji platformy Azure została oznaczona jako *nieusuwalnej*. W takim przypadku tylko hello usługa może następnie wykonaj rzeczywiste usunięcie hello i wykonuje zaplanowane proces. 



