---
title: "Omówienie powłoki chmury (wersja zapoznawcza) aaaAzure | Dokumentacja firmy Microsoft"
description: "Przegląd hello powłoki chmury Azure."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: 45c6c85b167a90947a333f44a9186e2c01b4fa7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-cloud-shell-preview"></a>Omówienie powłoki chmury Azure (wersja zapoznawcza)
Powłoki chmury Azure jest interaktywny, dostępny w przeglądarce powłoki zarządzania zasobami platformy Azure.

![](media/overview-pic.png)

## <a name="features"></a>Funkcje
### <a name="browser-based-shell-experience"></a>Środowisko powłoki przeglądarki
Chmury powłoki umożliwia dostęp tooa wiersza polecenia w przeglądarce skompilowanej za pomocą zadań zarządzania platformy Azure na uwadze. Korzystaj z powłoki chmury toowork autonomiczne z komputera lokalnego w sposób, który można podać tylko hello chmury.

### <a name="pre-configured-azure-workstation"></a>Wstępnie skonfigurowane Azure stacji roboczej
Powłoki chmury jest wstępnie zainstalowane z popularnych narzędzi wiersza polecenia i język obsługuje, dzięki czemu można pracować szybciej.

[Wyświetl hello narzędzi pełną listę dla powłoki chmury Azure tutaj.](features.md#tools)

### <a name="automatic-authentication"></a>Automatyczne uwierzytelnianie
W każdej sesji dla zasobów tooyour natychmiastowy dostęp za pośrednictwem hello Azure CLI 2.0 powłoki chmury bezpiecznie uwierzytelnia automatycznie.

### <a name="connect-your-azure-file-storage"></a>Łączenie z magazynem plików Azure
Maszyny powłoki chmury są tymczasowe i w związku z tym wymagają toobe udziału plików na platformę Azure zainstalowany jako `clouddrive` toopersist $Home katalogu.
Przy pierwszym uruchomieniu chmury powłoka wyświetli monit toocreate, które grupy zasobów, konta magazynu i udziału plików w Twoim imieniu. To jest jednorazowe kroku i być automatycznie dołączane do wszystkich sesji. 

#### <a name="create-new-storage"></a>Tworzenie nowego magazynu
![](media/basic-storage.png)

Konto magazyn lokalnie nadmiarowy (LRS) można utworzyć w Twoim imieniu z udziału plików na platformę Azure zawierającego domyślny obraz dysku 5 GB. Instaluje Hello udziału plików jako `clouddrive` dla pliku udziału interakcji z obrazu dysku hello są używane toosync i utrwala $Home katalogu. Koszty przechowywania regularne mają zastosowanie.

Trzy zasoby zostaną utworzone w Twoim imieniu:
1. Grupa zasobów o nazwie:`cloud-shell-storage-<region>`
2. Konto magazynu o nazwie:`cs<uniqueGuid>`
3. Udział plików o nazwie:`cs-<user>-<domain>-com-uniqueGuid`

> [!Note]
> Wszystkie pliki w katalogu $Home, takie jak klucze SSH są trwale przechowywane w udziale zainstalowanego pliku obrazu dysku użytkownika. Zastosowanie najlepszych rozwiązań podczas zapisywania plików w katalogu $Home i udziału zainstalowanego pliku.

#### <a name="use-existing-resources"></a>Korzystać z istniejących zasobów
![](media/advanced-storage.png)

Zaawansowana opcja dostępne są również zezwolenie na obecność możesz tooassociate istniejących zasobów tooCloud powłoki. Po prezentowany hello magazynu Instalatora wiersza, kliknij przycisk "Pokaż zaawansowane ustawienia" tooselect dodatkowe opcje. Listę rozwijaną są filtrowane przypisany region powłoki w chmurze i kont/globalnie — magazyn lokalnie nadmiarowy.

[Więcej informacji na temat magazynu powłoki chmury aktualizowanie udziałów plików i przekazywanie pobierania plików.] (utrwalanie shell-storage.md)

## <a name="concepts"></a>Pojęcia
* Powłoka działa na tymczasowej maszyny na sesji, poszczególnych użytkowników w chmurze
* Chmura powłoki upłynie limit czasu po upływie 20 minut bez interaktywnego działania
* Powłoka chmury można uzyskać tylko z udziałem plików dołączone
* Chmura powłoki przypisano na jednym komputerze na konto użytkownika
* Uprawnienia zostały ustawione jako zwykłych użytkowników systemu Linux

[Dowiedz się więcej o wszystkich funkcji powłoki chmury.](features.md)

## <a name="examples"></a>Przykłady
* Utwórz lub Edytuj tooautomate skryptów zarządzania platformy Azure
* Jednoczesne zarządzanie zasobami za pośrednictwem portalu Azure i 2.0 interfejsu wiersza polecenia platformy Azure
* Test-Drive Azure CLI 2.0

[Wypróbuj te przykłady na powitania powłoki chmury — Szybki Start.](quickstart.md)

## <a name="pricing"></a>Cennik
Hello komputerem obsługującym powłoki chmury jest wolne, wymaga wstępnie posiadania zainstalowanego pliku Azure udział toopersist $Home katalogu. Koszty przechowywania regularne mają zastosowanie.

## <a name="supported-browsers"></a>Obsługiwane przeglądarki
Powłoka w chmurze jest zalecane Chrome, Edge i przeglądarki Safari. Powłoka chmury jest obsługiwana dla programu Chrome, Firefox Safari, IE i krawędzi, powłoki chmury jest ustawienia przeglądarki toospecific podmiotu.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
1. Podczas korzystania z subskrypcji usługi Azure Active Directory, nie można utworzyć magazynu z powodu tooError: 400 DisallowedOperation. tooresolve, użyj subskrypcji platformy Azure umożliwia tworzenie zasobów magazynu. Subskrypcje AD są toocreate nie jest w stanie zasobów platformy Azure.

Dla określonego znane ograniczenia, odwiedź stronę [ograniczenia powłoki chmury](limitations.md).
