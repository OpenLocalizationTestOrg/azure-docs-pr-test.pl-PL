---
title: aaaAzure zestawu SDK dla platformy .NET 3.0 informacje o wersji | Dokumentacja firmy Microsoft
description: Informacje o wersji zestawu Azure SDK dla platformy .NET 3.0
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a>Informacje o wersji zestawu Azure SDK for .NET 3.0

Ten temat zawiera informacje o wersji dla wersji 3.0 hello Azure SDK dla platformy .NET.

##<a name="azure-sdk-for-net-30-release-summary"></a>Zestaw Azure SDK dla wersji .NET 3.0 podsumowania

Data wydania: 2017-03/07
 
Nie podziału zmiany toohello Azure SDK 3.0 zostały wprowadzone w tej wersji. Nie jest również nie tooleverage procesu uaktualniania wymagane tego zestawu SDK z istniejącymi projektami usługi w chmurze. Użycie tooallow hello Azure SDK 3.0 bez konieczności procesu uaktualniania, Azure SDK 3.0 instaluje toohello samych katalogach jako zestaw Azure SDK 2.9. Większość składników hello wersji głównej hello nie została zmieniona z 2.9, ale zamiast tego po zaktualizowaniu hello numer kompilacji.

## <a name="visual-studio-2017-rtw"></a>Visual Studio 2017 RTW

- W programie Visual Studio 2017 r. tej wersji programu hello Azure SDK dla platformy .NET jest wbudowany toohello obciążenia Azure. Wszystkie narzędzia hello należy toodo rozwoju platformy Azure będzie częścią Visual Studio 2017 r idąc dalej. Dla programu Visual Studio 2015 hello zestawu SDK będą nadal dostępne za pośrednictwem WebPI. Firma Microsoft ma przerywane zestawu Azure SDK dla wersji platformy .NET dla programu Visual Studio 2013 teraz, Visual Studio 2017 został zwolniony.

### <a name="azure-diagnostics"></a>Diagnostyka Azure

- Zmienione hello zachowanie tooonly przechowywać parametry połączenia z częściowa kluczem hello zastępuje token dla parametrów połączenia magazynu diagnostyki usługi w chmurze. Klucz magazynu rzeczywista Hello są obecnie przechowywane w folderze profilu użytkownika hello, można kontrolować dostęp do niej. Visual Studio odczyta hello klucza magazynu z folderu profilu użytkownika dla debugowania lokalnego i proces publikowania. 
- W przypadku zmiany toohello odpowiedzi opisane powyżej Visual Studio Online zespołu rozszerzone hello szablon zadania wdrożenia usługi w chmurze Azure, użytkownicy można określić klucz magazynu hello do ustawiania rozszerzenia diagnostyki podczas publikowania tooAzure w ciągłej integracji i wdrażania.
- Ułatwiliśmy ciągu bezpiecznego połączenia możliwe toostore i tokenizacji dla Azure Diagnostics (WAD), toohelp rozwiązuje problemy związane z konfiguracją w environements.
 
### <a name="windows-server-2016-virtual-machines"></a>Maszyny wirtualne systemu Windows Server 2016

- Program Visual Studio teraz obsługuje wdrażanie usługi w chmurze tooOS rodziny 5 (z systemem Windows Server 2016), maszynach wirtualnych. Istniejące usługi w chmurze, można zmienić Twojego tootarget ustawienia hello nowej rodziny systemów operacyjnych. Podczas tworzenia nowych usług w chmurze, jeśli wybierzesz toocreate hello usługi przy użyciu platformy .net 4.6 lub nowszej, będzie on domyślnej hello usługi toouse 5 rodziny systemu operacyjnego.  Aby uzyskać więcej informacji, możesz przejrzeć hello [rodziny systemów operacyjnych gościa obsługuje tabeli](../cloud-services/cloud-services-guestos-update-matrix.md).

### <a name="known-issues"></a>Znane problemy

- Azure .NET SDK 3.0 wprowadzono wystąpił problem podczas usuwania programu Visual Studio 2017 w konfiguracji obok siebie z programem Visual Studio 2015.  Jeśli masz hello zainstalowane dla programu Visual Studio 2015 SDK Azure hello emulatora magazynu Microsoft Azure i emulatora obliczeniowe programu Microsoft Azure zostaną usunięte, po odinstalowaniu programu Visual Studio 2017 r.  Spowoduje to utworzenie wystąpił błąd podczas tworzenia i debugowanie nowe projekty usługi w chmurze w programie Visual Studio 2015. W kolejności toofix ten problem, zainstaluj ponownie hello Azure SDK z hello Instalatora platformy sieci Web.  Witaj problem zostanie rozwiązany w przyszłej aktualizacji programu Visual Studio 2017 r.  .

 
### <a name="azure-in-role-cache"></a>Pamięć podręczna na roli Azure 

- Obsługę pamięci podręcznej na roli Azure została zakończona w dniu 30 listopada 2016 r. Aby uzyskać więcej informacji, kliknij przycisk [tutaj](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).




