---
title: "toodo aaaWhat w przypadku hello Azure zakłócenia, który ma wpływ na usługi Azure Key Vault | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie toodo w przypadku hello Azure zakłócenia, który ma wpływ na usługi Azure Key Vault."
services: key-vault
documentationcenter: 
author: adamglick
manager: mbaldwin
editor: 
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 88eec82ada401a28323b3eea126168185ba4cdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-availability-and-redundancy"></a>Usługa Azure Key Vault dostępność i nadmiarowość
Usługa Azure Key Vault funkcjami wielu warstw nadmiarowość toomake się, że Twoje klucze i klucze tajne nadal dostępne tooyour aplikacji, nawet jeśli pojedynczych składników hello usług kończyć się niepowodzeniem.

Witaj zawartość magazynu kluczy są replikowane w obrębie regionu hello i region pomocniczy tooa co najmniej 150 mil optymalizacji, ale w hello tej samej lokalizacji geograficznej. Zapewnia to dostępność wysoką trwałością kluczy i kluczy tajnych. Zobacz hello [Azure łączyć regionów](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) dokumentu szczegółowe informacje dotyczące konkretnego regionu pary.

Jeśli pojedynczych składników w ramach usługi Magazyn kluczy hello zakończą się niepowodzeniem, alternatywne składniki w obrębie regionu hello kroku w tooserve Twojego żądania toomake się, że nie jest bez spadku funkcji. Nie trzeba tootake tootrigger żadnych akcji to. On odbywa się automatycznie i będzie tooyou przezroczysty.

W przypadku rzadkich hello niedostępności całego regionu Azure, żądania hello, wprowadzone z usługi Azure Key Vault w tym regionie automatycznie są kierowane (*przejścia w tryb failover*) tooa regionie pomocniczym. Gdy regionu podstawowego hello jest ponownie dostępny, żądania są kierowane Wstecz (*nie powiodło się wstecz*) toohello regionu podstawowego. Ponownie nie trzeba tootake żadnych akcji, ponieważ jest to wykonywane automatycznie.

Znane są kilka toobe ostrzeżenia:

* W przypadku hello Failover region może potrwać kilka minut, aż hello toofail usługi za pośrednictwem. Żądania, które zostały wprowadzone w tym czasie może zakończyć się niepowodzeniem, dopóki nie zakończy pracy awaryjnej hello.
* Po zakończeniu pracy w trybie failover magazynu kluczy jest w trybie tylko do odczytu. Żądania, które są obsługiwane w tym trybie są:
  * Lista magazynów kluczy
  * Pobierz właściwości magazynów kluczy
  * Utwórz listę kluczy tajnych
  * Pobierz kluczy tajnych
  * Lista kluczy
  * Pobieranie kluczy (właściwości)
  * Szyfrowanie
  * Odszyfrowywanie
  * Zawijaj
  * Dekodowanie
  * Weryfikuj
  * Zaloguj się
  * Tworzenie kopii zapasowych
* Po przejściu w tryb failover nie jest ponownie, wszystkie żądania typy (w tym odczytu *i* żądań zapisu) są dostępne.

