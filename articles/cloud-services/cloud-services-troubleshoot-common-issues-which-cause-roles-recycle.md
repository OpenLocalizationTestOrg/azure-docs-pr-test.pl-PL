---
title: "aaaCommon powoduje, że odtwarzanie ról usługi w chmurze | Dokumentacja firmy Microsoft"
description: "Rola usługi chmury, która nagle odtwarzana może spowodować znaczne przestoju. Poniżej przedstawiono typowe problemy, które powodują toobe ról poddanych recyklingowi, które mogą pomóc w zmniejszeniu przestoju."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 8fa152b33d2b22a8a02f834d4bc38519b4272f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="common-issues-that-cause-roles-toorecycle"></a>Typowe problemy powodujące toorecycle ról
W tym artykule omówiono niektóre typowe przyczyny problemów z wdrażaniem hello i rozwiązywanie problemów z toohelp: porady dotyczące rozwiązywania tych problemów. Wskazanie, że istnieje problem z aplikacją jest wystąpienia roli hello toostart nie powiedzie się lub jego przełączanie między Stanami inicjowania zajęty i zatrzymywanie hello.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a>Brak zależności środowiska uruchomieniowego
Jeśli rola w aplikacji zależy od zestawu, który nie jest częścią hello biblioteki zarządzanej .NET Framework lub hello Azure, należy jawnie przypisać w pakiecie aplikacji hello tego zestawu. Należy pamiętać, że innych platform firmy Microsoft, nie są dostępne na platformie Azure domyślnie. Jeśli rola użytkownika opiera się na takie struktury, należy dodać pakiet aplikacji toohello tych zestawów.

Przed kompilacji i pakiet aplikacji, należy sprawdzić następujące hello:

* Jeśli przy użyciu programu Visual studio, upewnij się, że hello **Kopiuj lokalnie** właściwość jest ustawiona zbyt**True** dla każdego odwołania do zestawu w projekcie, który nie jest częścią hello Azure SDK lub hello .NET Framework.
* Upewnij się, że plik web.config hello nie odwołuje się do żadnych zestawów nieużywane w elemencie kompilacji hello.
* Witaj **Akcja kompilacji** .cshtml co plik został ustawiony zbyt**zawartości**. Dzięki temu, że hello pliki będą wyświetlane poprawnie w pakiecie hello i umożliwia tooappear innych plików w pakiecie hello.

## <a name="assembly-targets-wrong-platform"></a>Zestaw obiektów docelowych nieprawidłowej platformie
Platforma Azure jest 64-bitowego środowiska. W związku z tym skompilowany dla elementu docelowego 32-bitowych zestawów platformy .NET nie będzie działać na platformie Azure.

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a>Rola zgłasza nieobsługiwanych wyjątków podczas inicjowania lub zatrzymywanie
Wszystkie wyjątki, które są zgłaszane przez metody hello hello [RoleEntryPoint] klasy, która obejmuje hello [OnStart], [OnStop], i [Uruchom]metody, są nieobsługiwane wyjątki. Jeśli wystąpi nieobsługiwany wyjątek w jednej z tych metod, odtwarzana hello roli. Jeśli rola hello jest odtwarzanie wielokrotnie, może być zgłaszanie nieobsługiwany wyjątek zawsze próbuje toostart.

## <a name="role-returns-from-run-method"></a>Zwraca roli z metoda Run
Witaj [Uruchom] metoda jest zamierzone toorun przez nieograniczony czas. Jeśli kod zastępuje hello [Uruchom] metody go uśpienia przez nieograniczony czas. Jeśli hello [Uruchom] metoda zwróci wartość, odtwarzana hello roli.

## <a name="incorrect-diagnosticsconnectionstring-setting"></a>Nieprawidłowe ustawienie DiagnosticsConnectionString
Jeśli aplikacja używa diagnostyki Azure, w pliku konfiguracji usługi należy określić hello `DiagnosticsConnectionString` ustawienia konfiguracji. To ustawienie należy określić konto magazynu tooyour połączenia HTTPS na platformie Azure.

tooensure który Twojej `DiagnosticsConnectionString` ustawienia są poprawne, przed wdrożeniem programu tooAzure pakietu aplikacji, sprawdź następujące hello:  

* Witaj `DiagnosticsConnectionString` ustawienia punktów tooa prawidłowe konto magazynu na platformie Azure.  
  Domyślnie to ustawienie punktów toohello emulowane konta magazynu, dlatego należy jawnie zmienić to ustawienie przed wdrożeniem pakietu aplikacji. Jeśli nie należy zmieniać tego ustawienia, wyjątku monitora diagnostycznego hello toostart próbujący hello wystąpienia roli. Może to spowodować toorecycle wystąpienia roli hello nieskończoność.
* Witaj ciągu połączenia jest określona w następujących hello [format](../storage/common/storage-configure-connection-string.md). (hello protokołu, muszą być określone jako HTTPS). Zastąp *MyAccountName* hello nazwą konta magazynu i *MyAccountKey* kluczem dostępu:    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  Jeśli tworzysz aplikację za pomocą narzędzia Azure dla programu Microsoft Visual Studio, możesz użyć tooset stron właściwości hello tej wartości.

## <a name="exported-certificate-does-not-include-private-key"></a>Wyeksportowany certyfikat nie zawiera klucza prywatnego
toorun rolę sieci web w ramach protokołu SSL, pamiętaj, że zarządzania wyeksportowany certyfikat zawiera klucz prywatny hello. Jeśli używasz hello *Menedżera certyfikatów systemu Windows* tooexport hello certyfikatu, można tooselect się, że **tak** dla hello **klucza prywatnego hello eksportu** opcji. Witaj, certyfikat musi być eksportowany w formacie PFX hello, który jest tylko format hello obecnie obsługiwane.

## <a name="next-steps"></a>Następne kroki
Wyświetl więcej [Rozwiązywanie problemów z artykułów](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) dla usług w chmurze.

Wyświetl więcej roli odtwarzania scenariusze, w [serii blogu Kevina Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[Uruchom]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
