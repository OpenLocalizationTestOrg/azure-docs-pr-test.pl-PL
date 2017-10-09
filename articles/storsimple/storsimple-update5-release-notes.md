---
title: informacje o wersji aaaStorSimple 8000 serii aktualizacji 5 | Dokumentacja firmy Microsoft
description: "Opis nowych funkcji hello, problemy i rozwiązania StorSimple 8000 serii aktualizacji 5."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: 9eb8ffb97b41ce3d4f1ffdf2975f904d0a2958e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a>Informacje o wersji StorSimple 8000 serii aktualizacji 5

## <a name="overview"></a>Omówienie

Witaj poniższych informacjach o wersji opisano nowe funkcje hello i zidentyfikować problemy krytyczne Otwórz hello StorSimple 8000 serii aktualizacji 5. Zawierają one również listę aktualizacji oprogramowania StorSimple hello zawarte w tej wersji.

Aktualizacji 5 może być zastosowane tooany StorSimple urządzenie z systemem Update 0.1 za pomocą aktualizacji w wersji 4. Wersja urządzenia Hello skojarzony z aktualizacją 5 jest 6.3.9600.17845.

Przejrzyj hello informacji zawartych w wersji hello, uwagi przed wdrożeniem hello aktualizacja w rozwiązaniu StorSimple.

> [!IMPORTANT]
> * Aktualizacja 5 ma oprogramowanie urządzenia, oprogramowania układowego dysku zabezpieczeń systemu operacyjnego i inne aktualizacje systemu operacyjnego. Trwa około 4 godziny tooinstall tej aktualizacji. Aktualizacja oprogramowania układowego dysku jest destrukcyjne aktualizacji i powoduje przestój dla danego urządzenia. Firma Microsoft zaleca zastosowanie aktualizacji 5 tookeep aktualne urządzenia.
> * Dostępność nowych wersji nie może wyświetlić aktualizacje od razu, ponieważ jak etapowego wdrażania hello aktualizacji. Poczekaj kilka dni, a następnie skanowanie w poszukiwaniu aktualizacji ponownie jako tych aktualizacji zostanie wkrótce udostępnione.

## <a name="whats-new-in-update-5"></a>Nowości w aktualizacji 5

Witaj następujące ulepszenia klucza i poprawki zostały wprowadzone w aktualizacji 5.

* **Korzystanie z usługi Azure Active Directory (AAD) tooauthenticate z usługą Menedżera urządzeń StorSimple** — tooauthenticate używane z usługą Menedżera urządzeń StorSimple hello jest z aktualizacją 5 lub nowszej, Azure Active Directory. mechanizm uwierzytelniania starego Hello zostaną wycofane przez 2017 grudnia. Wszyscy użytkownicy hello musi zawierać hello i nowego adresu URL uwierzytelniania w ich reguł zapory. Aby uzyskać więcej informacji, przejdź zbyt[uwierzytelnianie adresów URL na liście hello wymagań sieciowych dotyczących urządzenia StorSimple](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal).

    Jeśli adres URL uwierzytelniania hello nie jest uwzględniony w regułach zapory hello, hello użytkownicy będą widzieć alert krytyczny, który ich urządzenia StorSimple nie można uwierzytelnić z usługą hello. Jeśli użytkownik hello ten alert, muszą one tooinclude hello nowy adres URL uwierzytelniania. Aby uzyskać więcej informacji, przejdź zbyt[StorSimple sieci alerty](storsimple-8000-manage-alerts.md#networking-alerts).

* **Nowa wersja programu StorSimple Snapshot Manager** -wydaniu nowej wersji programu StorSimple Snapshot Manager z aktualizacją 5. Zaleca się zaktualizowanie toothis wersji. Ta wersja jest zgodne ze wszystkimi urządzeniami StorSimple hello uruchomionych aktualizacji 3 lub nowszym. Aby uzyskać więcej informacji, przejdź zbyt[wdrażanie StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).


## <a name="issues-fixed-in-update-5"></a>Problemy rozwiązane w ramach aktualizacji 5

Witaj Poniższa tabela zawiera podsumowanie problemów, które zostały usunięte w aktualizacji 5.

| Nie | Funkcja | Problem | Stosuje toophysical urządzenia | Stosuje toovirtual urządzenia |
| --- | --- | --- | --- | --- |
| 1 |Komunikacji zdalnej programu Windows PowerShell |W poprzedniej wersji hello użytkownik otrzyma błąd w trakcie tooestablish toohello połączenia zdalnego StorSimple urządzenia chmury za pomocą środowiska Windows PowerShell. Ten problem został spowodowany głównego i stałym w tej wersji. |Nie |Tak |
| 2 |Szablony przepustowości |W starszej wersji wystąpił problem z szablonami przepustowości, które spowodowało mniejszej przepustowości od jakiego urządzenia hello został skonfigurowany pod kątem. Ten problem zostanie rozwiązany w tej wersji. |Tak |Tak |
| 3 |Tryb failover |W poprzedniej wersji gdy urządzenie z dużą liczbą woluminów nie powiodło się za pośrednictwem urządzenia tooanother uruchomić aktualizację Update 4 procesu hello spowoduje niepowodzenie podczas próby rekordy kontroli dostępu hello tooapply. Tego problemu w tej wersji. |Tak |Tak |



## <a name="known-issues-in-update-5-from-previous-releases"></a>Znane problemy w aktualizacji 5 z poprzednich wersji

Nie występują nowe znane problemy w aktualizacji 5. Listę problemów przenoszone tooUpdate 5 z poprzednich wersji, przejdź zbyt[wersji Update 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a>Magistrali Serial attached SCSI (SAS) kontrolera aktualizacje w aktualizacji 5

Ta wersja zawiera kontroler SAS i LSI aktualizacje sterowników i oprogramowania układowego. Aby uzyskać więcej informacji na temat tooinstall tych aktualizacji, zobacz temat [zainstalować aktualizacji 5](storsimple-8000-install-update-5.md) na urządzeniu StorSimple.

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a>Aktualizacje urządzenia chmury StorSimple w aktualizacji 5

Ta aktualizacja nie może być zastosowane toohello urządzenia chmury StorSimple (znanej także jako hello urządzenia wirtualnego). Nowe urządzenia w chmurze muszą toobe utworzone przy użyciu obrazu hello aktualizacji 5. Aby uzyskać informacje na temat toocreate urządzenia chmury StorSimple przejść za[wdrażanie i zarządzanie nimi urządzenia chmury StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="next-step"></a>Następny krok

Dowiedz się, jak za[zainstalować aktualizacji 5](storsimple-8000-install-update-5.md) na urządzeniu StorSimple.

