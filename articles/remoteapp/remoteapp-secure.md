---
title: "aaaSecure aplikacji i zasobów w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toolock dół aplikacji i zasobów w usłudze Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7fbade87-a453-426d-bfa5-c72227ea83cd
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 26325826e92855a12a0087f19a3e32cbe1116449
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-apps-and-resources-in-azure-remoteapp"></a>Zabezpieczanie aplikacji i zasobów w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp zapewnia użytkownikom dostęp do zarządzanych toocentrally aplikacji systemu Windows pozwala kontrolować, co użytkownicy mogą i nie może wykonać.  Jest to szczególnie przydatne, gdy użytkownik hello jest łączenie z niezarządzanego urządzenia (takich jak ich osobistych Macbook), a chcesz toocontrol hello użytkownikowi dostępu lub wystąpić.

Na przykład jeśli używasz usługi Active Directory do uwierzytelniania użytkowników, i chcesz tooprevent użytkownikom kopiowania danych z aplikacji, można skonfigurować użytkowników tooblock zasad grupy usług pulpitu zdalnego z kopiowania danych.

Innym przykładem jest, jeśli mają dostęp do Internetu tooblock dla danej aplikacji w kolekcji. Można utworzyć regułę zapory systemu Windows, że bloki hello dostępu podczas tworzenia obrazu hello kolekcji.

## <a name="implementation-options"></a>Opcje wdrażania
  Oto opcje implementacji klucza hello, które mogą być używane pojedynczo lub w połączeniu w razie potrzeby:

1. Jeżeli kolekcji usługi RemoteApp jest przyłączony do domeny można wymusić żadnego [zasad grupy](https://technet.microsoft.com/library/cc725828.aspx) (z wyjątkiem hello hello bezczynny i Odłącz limitu czasu zasady opisane [tutaj](../azure-subscription-service-limits.md)).
2. Jako alternatywne tooGroup zasad (jeśli kolekcji nie jest przyłączony do domeny lub nie masz odpowiednich uprawnień dostępu hello w usłudze AD), można skonfigurować [zasady lokalne](https://technet.microsoft.com/library/cc775702.aspx) w obrazie szablonu.  Należy pamiętać, że grupy zasad atu zasady lokalne, gdy występuje konflikt.
3. Niektóre ustawienia systemu operacyjnego/aplikacji nie są konfigurowane za pomocą zasad, ale może być za pomocą klucza rejestru za pomocą hello [narzędzie RegEdit](remoteapp-hybridtrouble.md) podczas konfigurowania obrazu szablonu.
4. Można użyć [zapory systemu Windows](http://windows.microsoft.com/en-US/windows-8/Windows-Firewall-from-start-to-finish) tooand dostępu do sieci toocontrol, z którym jest uruchomiona aplikacja hello maszyny hello. Po prostu upewnij się, że nie blokuj hello adresy URL i portów zdefiniowane w tym miejscu.
5. Można użyć [zasad ograniczeń oprogramowania](https://technet.microsoft.com/library/hh831440.aspx) toocontrol, który można uruchomić aplikacji i plików użytkowników. Na przykład pomysłowy użytkownicy mogą dowiedzieć się, jak toorun aplikacji, która nie jest publikowana, ale są dostępne w hello obrazu możesz użyć toocreate hello kolekcji — Funkcja AppLocker może blokować to.

## <a name="detailed-information"></a>Szczegółowe informacje
* następujące zasady RDS Hello są prawdopodobnie toobe najbardziej przydatne:
  * [Przekierowywanie urządzeń i zasobów](https://technet.microsoft.com/library/ee791794.aspx)
  * [Przekierowanie drukarki](https://technet.microsoft.com/library/ee791784.aspx)
  * [Profile](https://technet.microsoft.com/library/ee791865.aspx).
* Należy pamiętać, że konfigurowanie przekierowań za pośrednictwem hello modułu programu PowerShell dla usługi RemoteApp (widziany [tutaj](remoteapp-redirection.md)) polega na powitania klienta tooenforce hello zasady, więc jeśli zabezpieczeń jest celem podstawowym hello tooenforce hello zasad za pośrednictwem Witaj zasad lokalnych obrazu szablonu lub za pomocą zasad grupy.
* [Zasady systemu Windows Server 2012 R2](https://technet.microsoft.com/library/hh831791.aspx).
* [Pakiet Office 2013 zasady](https://technet.microsoft.com/library/cc178969.aspx) (łącznie z [jak toocustomize hello paska narzędzi pakietu Office](https://technet.microsoft.com/library/cc179143.aspx)).

