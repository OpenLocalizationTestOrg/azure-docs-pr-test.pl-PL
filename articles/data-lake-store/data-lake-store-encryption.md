---
title: "aaaEncryption w usłudze Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Omówienie sposobu działania szyfrowania i wymiany kluczy w usłudze Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: yagupta
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 4/14/2017
ms.author: yagupta
ms.openlocfilehash: a9f3a2dce8232deba93005594d1e6a21e9c0cbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encryption-of-data-in-azure-data-lake-store"></a>Szyfrowanie danych w usłudze Azure Data Lake Store

Szyfrowanie w usłudze Azure Data Lake Store pomaga chronić dane, implementować zasady bezpieczeństwa w przedsiębiorstwie i spełniać prawne wymagania dotyczące zgodności. Ten artykuł zawiera omówienie projektowania hello i omówiono niektóre aspekty techniczne hello implementacji.

Usługa Data Lake Store obsługuje szyfrowanie danych zarówno magazynowanych, jak i przesyłanych. W przypadku danych magazynowanych usługa Data Lake Store obsługuje domyślnie włączone szyfrowanie przezroczyste. Poniżej przedstawiono bardziej szczegółowe wyjaśnienie tych terminów:

* **Na domyślnie**: podczas tworzenia nowego konta usługi Data Lake Store hello domyślne ustawienie włącza szyfrowanie. Później dane przechowywane w usłudze Data Lake Store jest zawsze zaszyfrowane wcześniejsze toostoring na nośniku trwałe. Jest to zachowanie hello wszystkich danych i nie można zmienić po utworzeniu konta.
* **Przezroczysty**: Data Lake Store automatycznie szyfruje toopersisting wcześniejszych danych i odszyfrowuje tooretrieval wcześniejszych danych. szyfrowanie Hello jest skonfigurowany i zarządzane na powitania poziom usługi Data Lake Store przez administratora. Nie są zmienione dane toohello dostęp do interfejsów API. W związku z tym z powodu szyfrowania nie ma konieczności wprowadzania żadnych zmian w aplikacjach i usługach, które współdziałają z usługą Data Lake Store.

Dane przesyłane (inaczej dane w ruchu) również są zawsze szyfrowane w usłudze Data Lake Store. Ponadto tooencrypting danych przed toostoring toopersistent nośnika hello zawsze ochrona danych podczas przesyłania przy użyciu protokołu HTTPS. HTTPS jest hello tylko protokół, który jest obsługiwany w przypadku powitalne interfejsy Data Lake magazynu REST. Witaj poniższym diagramie przedstawiono sposób dane szyfrowane staje się w usłudze Data Lake Store:

![Diagram szyfrowania danych w usłudze Data Lake Store](./media/data-lake-store-encryption/fig1.png)


## <a name="set-up-encryption-with-data-lake-store"></a>Konfigurowanie szyfrowania przy użyciu usługi Data Lake Store

Szyfrowanie w usłudze Data Lake Store konfiguruje się podczas tworzenia konta i zawsze jest domyślnie włączone. Możesz zarządzać kluczami hello, samodzielnie, lub zezwolić toomanage usługi Data Lake Store je automatycznie (jest to domyślny hello).

Aby uzyskać więcej informacji, zobacz [Wprowadzenie](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

## <a name="how-encryption-works-in-data-lake-store"></a>Jak działa szyfrowanie w usłudze Data Lake Store

Witaj następujące informacje dotyczą sposobu toomanage główny szyfrowania kluczy, a także opisano hello trzy różne typy klawisze, których można używać szyfrowania danych dla usługi Data Lake Store.

### <a name="master-encryption-keys"></a>Główne klucze szyfrowania

Usługa Data Lake Store udostępnia dwa tryby zarządzania głównymi kluczami szyfrowania. Teraz załóżmy, że klucz główny szyfrowania hello jest hello klucz najwyższego poziomu. Klucz główny szyfrowania toohello dostępu jest wymagany toodecrypt wszystkie dane przechowywane w usłudze Data Lake Store.

Hello dwa tryby zarządzania klucz główny szyfrowania hello są następujące:

*   Klucze zarządzane przez usługę
*   Klucze zarządzane przez klienta

W obu trybach klucz główny szyfrowania hello jest chroniona przez zapisanie go w usłudze Azure Key Vault. Key Vault jest usługą pełni zarządzany i wysokim poziomie zabezpieczeń na platformie Azure, które mogą być używane toosafeguard kluczy kryptograficznych. Aby uzyskać więcej informacji, zobacz [Key Vault](https://azure.microsoft.com/services/key-vault).

Oto krótkie porównanie możliwości oferowane przez dwa tryby hello Zarządzanie hello MEKs.

|  | Klucze zarządzane przez usługę | Klucze zarządzane przez klienta |
| --- | --- | --- |
|W jaki sposób przechowywane są dane?|Zawsze zaszyfrowane toobeing wcześniejsze przechowywane.|Zawsze zaszyfrowane toobeing wcześniejsze przechowywane.|
|Gdzie są przechowywane hello klucza szyfrowania|Usługa Key Vault|Usługa Key Vault|
|Wszystkie klucze przechowywane w hello wyczyść szyfrowania znajdują się poza Key Vault? |Nie|Nie|
|Witaj MEK można pobrać przez usługi Key Vault?|Nie. Po hello MEK jest przechowywany w magazynie kluczy można można używać tylko do szyfrowania i odszyfrowywania.|Nie. Po hello MEK jest przechowywany w magazynie kluczy można można używać tylko do szyfrowania i odszyfrowywania.|
|Kto jest właścicielem wystąpienia usługi Key Vault hello i hello MEK?|Witaj usługi Data Lake Store|Jesteś właścicielem hello wystąpienia usługi Key Vault, która należy do subskrypcji platformy Azure. Hello MEK w magazynie kluczy mogą być zarządzane przez oprogramowania lub sprzętu.|
|Możesz cofnąć dostęp toohello MEK dla hello usługi Data Lake Store|Nie|Tak. Zarządzanie listami kontroli dostępu w magazynie klucz i Usuń tożsamość usługi toohello wpisów kontroli dostępu dla hello usługi Data Lake Store.|
|Można trwale usunąć hello MEK?|Nie|Tak. Po usunięciu hello MEK z magazynu kluczy danych hello w hello konta usługi Data Lake Store nie można odszyfrować wszystkim osobom hello usługą Data Lake Store. <br><br> Jeśli jawnie kopii zapasowej poprzedniego toodeleting MEK hello go z magazynu kluczy, hello MEK można przywrócić, a następnie można odzyskać dane hello. Jednak jeśli nie kopii zapasowej poprzedniego toodeleting MEK hello go z magazynu kluczy, hello w hello konta usługi Data Lake Store może nigdy nie można odszyfrować danych później.|


Jako uzupełnienie tej różnicy, który zarządza hello MEK i hello Key Vault wystąpienia w której się znajduje, hello reszty projektu hello jest hello takie same dla obu trybów.

Po wybraniu trybu hello hello kluczy szyfrowania głównego jest ważne tooremember hello poniżej:

*   Można wybrać, czy klient toouse zarządzanych kluczy lub kluczy usługi zarządzania podczas obsługi administracyjnej konto usługi Data Lake Store.
*   Po udostępnieniu konto usługi Data Lake Store, nie można zmienić trybu hello.

### <a name="encryption-and-decryption-of-data"></a>Szyfrowanie i odszyfrowywanie danych

Istnieją trzy typy kluczy, które są używane w projekcie hello szyfrowania danych. Witaj w poniższej tabeli przedstawiono podsumowanie:

| Klucz                   | Skrót | Skojarzony z | Lokalizacja magazynu                             | Typ       | Uwagi                                                                                                   |
|-----------------------|--------------|-----------------|----------------------------------------------|------------|---------------------------------------------------------------------------------------------------------|
| Główny klucz szyfrowania | GKS          | Konto usługi Data Lake Store | Usługa Key Vault                              | Asymetryczny | Może nim zarządzać usługa Data Lake Store lub można to robić samodzielnie.                                                              |
| Klucz szyfrowania danych   | KSD          | Konto usługi Data Lake Store | Magazyn trwały zarządzany przez usługę Data Lake Store | Symetryczny  | Witaj klucza szyfrowania danych jest szyfrowany za hello MEK. Witaj, zaszyfrowanego klucza szyfrowania danych jest co to są przechowywane na nośnikach trwałych. |
| Klucz szyfrowania bloków  | KSB          | Blok danych | Brak                                         | Symetryczny  | Witaj BEK jest pochodną hello klucza szyfrowania danych i hello bloku danych.                                                      |

powitania po diagram ilustruje te pojęcia:

![Klucze używane do szyfrowania danych](./media/data-lake-store-encryption/fig2.png)

#### <a name="pseudo-algorithm-when-a-file-is-toobe-decrypted"></a>Pseudo algorytmu, gdy plik jest odszyfrowywany toobe:
1.  Sprawdź, czy hello klucza szyfrowania danych dla konta usługi Data Lake Store hello jest buforowany i gotowa do użycia.
    - Jeśli nie, odczytać hello zaszyfrowany klucz szyfrowania danych z magazynu trwałego i wysłać go odszyfrować toobe magazynu tooKey. Pamięć podręczna hello odszyfrować klucza szyfrowania danych w pamięci. Jest teraz gotowy toouse.
2.  Dla każdego bloku danych w pliku hello:
    - Odczyt hello zaszyfrowanego bloku danych z magazynu trwałego.
    - Generowanie hello BEK z hello klucza szyfrowania danych i hello zaszyfrowanego bloku danych.
    - Użyj hello BEK toodecrypt danych.


#### <a name="pseudo-algorithm-when-a-block-of-data-is-toobe-encrypted"></a>Algorytm pseudo toobe szyfrowane po bloku danych:
1.  Sprawdź, czy hello klucza szyfrowania danych dla konta usługi Data Lake Store hello jest buforowany i gotowa do użycia.
    - Jeśli nie, odczytać hello zaszyfrowany klucz szyfrowania danych z magazynu trwałego i wysłać go odszyfrować toobe magazynu tooKey. Pamięć podręczna hello odszyfrować klucza szyfrowania danych w pamięci. Jest teraz gotowy toouse.
2.  Generuj unikatowy BEK hello bloku danych z hello klucza szyfrowania danych.
3.  Szyfrowanie hello bloku danych z hello BEK, przy użyciu szyfrowania AES 256.
4.  Blok zaszyfrowanych danych hello magazynu danych na magazynu trwałego.

> [!NOTE] 
> Ze względu na wydajność wyczyść klucza szyfrowania danych w hello hello są buforowane w pamięci przez krótki czas i natychmiastowe jest później usunięte. Na nośniku trwałe zawsze znajduje się szyfrowane przez hello MEK.

## <a name="key-rotation"></a>Wymiana kluczy

Korzystając z kluczy zarządzany przez klienta, można obracać hello MEK. toolearn tooset konto usługi Data Lake Store z kluczami zarządzany przez klienta, zobacz temat [wprowadzenie](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

### <a name="prerequisites"></a>Wymagania wstępne

Po skonfigurowaniu konta usługi Data Lake Store hello wybrano toouse własnych kluczy. Nie można zmienić tej opcji, po utworzeniu konta hello. Witaj następujących krokach założono używasz klucze zarządzany przez klienta (oznacza to, że wybrano własnych kluczy z usługi Key Vault).

Należy pamiętać, że jeśli używasz hello domyślne opcje szyfrowania danych są zawsze szyfrowane przy użyciu kluczy zarządzanych przez usługi Data Lake Store. W przypadku tej opcji nie masz hello możliwości toorotate kluczy, ponieważ są one zarządzane przez usługi Data Lake Store.

### <a name="how-toorotate-hello-mek-in-data-lake-store"></a>Jak toorotate hello MEK w usłudze Data Lake Store

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Przeglądaj toohello Key Vault wystąpienie, które są przechowywane klucze skojarzone z kontem usługi Data Lake Store. Wybierz pozycję **Klucze**.

    ![Zrzut ekranu usługi Key Vault](./media/data-lake-store-encryption/keyvault.png)

3.  Wybierz klucz hello skojarzony z Twoim kontem usługi Data Lake Store i utworzyć nową wersję tego klucza. Należy pamiętać, że Data Lake Store aktualnie obsługuje tylko rotacją kluczy tooa nowa wersja klucza. Nie obsługuje on obracania tooa inny klucz.

   ![Zrzut ekranu okna Klucze z wyróżnionym przyciskiem Nowa wersja](./media/data-lake-store-encryption/keynewversion.png)

4.  Konto magazynu Data Lake Store toohello Przeglądaj i wybierz **szyfrowania**.

    ![Zrzut ekranu okna konta magazynu usługi Data Lake Store z wyróżnioną pozycją Szyfrowanie](./media/data-lake-store-encryption/select-encryption.png)

5.  Komunikat informuje, czy dostępna jest nowa wersja klucza hello klucza. Kliknij przycisk **Obróć klucza** tooupdate hello klucza toohello nowej wersji.

    ![Zrzut ekranu okna usługi Data Lake Store z komunikatem i wyróżnioną pozycją Wymień klucz](./media/data-lake-store-encryption/rotatekey.png)

Ta operacja powinno zająć mniej niż dwóch minut, i nie ma bez przestojów oczekiwanego powodu tookey obrotu. Po zakończeniu operacji hello hello nowej wersji klucza hello jest używany.
