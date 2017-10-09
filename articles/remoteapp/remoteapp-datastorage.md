---
title: "poufne dane aaaNever magazyn na niestandardowych obrazów dla usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o wytycznych hello do przechowywania danych w niestandardowych obrazów w usłudze Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a>Nigdy nie przechowują dane poufne na niestandardowych obrazów
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Kiedy host aplikacji w usłudze Azure RemoteApp, pierwszym krokiem hello jest toocreate niestandardowego obrazu. Korzystamy z tego obrazu niestandardowego wystąpień maszyn wirtualnych toocreate obsługujących aplikacje tooyour użytkowników. niestandardowy obraz powitania powinna zawierać tylko aplikacji i nigdy nie poufnych danych, które mogą zostać utracone, takie jak bazy danych SQL, pliki personelu lub plików danych specjalnych, takich jak pliki firmy QuickBooks. Wszystkie dane poufne powinien znajdować się tooAzure zewnętrznych RemoteApp na serwerze plików z innej maszyny Wirtualnej platformy Azure lub w usługach SQL Azure. Obraz powitania powinien tylko aplikacji hello hosta, która łączy toohello źródła danych i przedstawia hello danych. Przegląd [wymagania dotyczące usługi Azure RemoteApp obrazów](remoteapp-imagereqs.md) Aby uzyskać więcej informacji. 

toounderstand, dlaczego nie należy przechowywać poufnych danych, należy toounderstand sposób działania usługi Azure RemoteApp. Podczas tworzenia lub aktualizowania kolekcji tle hello wielu klony lub kopii obrazu hello są tworzone. Wszystkie wystąpienia maszyny Wirtualnej są dokładne repliki hello niestandardowego obrazu; gdy użytkownicy uruchomią aplikacji są połączone tooone tych wystąpień maszyny Wirtualnej. Jednak hello tego samego wystąpienia nie jest gwarantowana i powinien niezależnie od tego, ponieważ są one trwałe. Witaj wystąpień maszyn wirtualnych hostingu aplikacji hello są trwałe i mogą być zniszczony lub usunięty, opartych na przykład podczas aktualizowania kolekcji. 

Po zainicjowaniu obsługi zbierania hello i użytkownicy uruchamiają łączącego toohello maszyny wirtualne, dane użytkownika są trwałe i chronić, ponieważ są one zapisywane na oddzielnych magazynu w ramach dysku VHD, który nazywamy [dysku profilu użytkownika (UPD)](remoteapp-upd.md), która jest hello profilu użytkownika w c:\users\<userprofile >. Po uruchomieniu aplikacji hello UPD jest instalowana i traktowany tak samo jak lokalny profil użytkownika przez system operacyjny hello. Dowiedz się więcej o jak [usługi Azure RemoteApp zapisuje dane użytkownika i ustawienia](remoteapp-upd.md).

Przykładowe dane, który nie powinien znajdować się w obrazie hello:

* Udostępnionych danych dla użytkowników tooaccess
* Baza danych SQL lub bazy danych programu QuickBooks
* Wszystkie dane w D:\

Przykładowe dane, które mogą znajdować się w toobe profil domyślny hello są kopiowane do UPD co użytkowników:

* Pliki konfiguracji na użytkownika
* Skrypty, które użytkownicy czy muszą być zachowane w ich UPD

Kwestie kluczowe:

* Nigdy nie przechowują dane poufne, które można utracić hello obrazu podczas tworzenia niestandardowego obrazu.
* Dane poufne zawsze powinien znajdować się na oddzielnym serwerze plików, oddziel maszyny Wirtualnej platformy Azure w chmurze hello i wystąpień maszyny Wirtualnej zawsze zewnętrznych toohello hosting aplikacji w usłudze Azure RemoteApp. 
* Dane użytkownika są zapisywane i będzie się powtarzał dysku profilu użytkownika hello (UPD)

