---
title: "aaaTroubleshoot ról, które nie są toostart | Dokumentacja firmy Microsoft"
description: "Poniżej przedstawiono niektóre typowe przyczyny, dlaczego roli usługi w chmurze może się nie powieść toostart. Podawane są również rozwiązania toothese problemów."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a>Rozwiązywanie problemów z ról usługi w chmurze, które nie są toostart
Poniżej przedstawiono niektóre typowe problemy i rozwiązania pokrewne tooAzure usługi w chmurze ról, które się nie powieść toostart.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a>Brak biblioteki DLL lub zależności
Odpowiadać oraz ról, które są cykliczne między **inicjowanie**, **zajęty**, i **zatrzymywanie** stanów może być spowodowany brakiem biblioteki DLL lub zestawów.

Objawy Brak biblioteki DLL lub zestawy mogą być:

* Wystąpienie roli jest okrągło **inicjowanie**, **zajęty**, i **zatrzymywanie** stanów.
* Wystąpienie roli przeniósł zbyt**gotowe** , ale w przypadku przejścia aplikacji sieci web tooyour hello strona nie jest wyświetlana.

Istnieje kilka metod zalecane do badania tych problemów.

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a>Diagnozowanie Brak problemów biblioteki DLL w roli sieć web
Po przejściu tooa witryny sieci Web, które zostało wdrożone w roli sieci web, hello przeglądarka wyświetla serwera błąd podobny toohello następujące, może to oznaczać brak biblioteki DLL.

![Błąd serwera w "/" aplikacji.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a>Diagnozowanie problemów przez wyłączenie błędów niestandardowych
Bardziej szczegółowy informacje o błędzie mogą zostać przejrzane przez konfigurowanie hello web.config dla roli sieci web hello tooset tooOff tryb błędów niestandardowych hello ani ponownego wdrażania hello usługi.

tooview Wypełnij więcej błędy bez przy użyciu pulpitu zdalnego:

1. Otwórz rozwiązanie hello w programie Microsoft Visual Studio.
2. W hello **Eksploratora rozwiązań**, Znajdź plik web.config hello i otwórz go.
3. W pliku web.config hello zlokalizować sekcji system.web hello i Dodaj powitania po wierszu:

    ```xml
    <customErrors mode="Off" />
    ```
4. Zapisz plik hello.
5. Spakuj ponownie i ponownie wdrożyć usługę hello.

Gdy jest ponownie wdrożyć usługę hello, zostanie wyświetlony komunikat o błędzie, nazwą hello hello brakuje zestawu lub biblioteki DLL.

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a>Diagnozowanie problemów poprzez wyświetlenie błędu hello zdalnie
Możesz za pomocą roli hello tooaccess pulpitu zdalnego i wyświetlić więcej informacji o zdalnie. Użyj hello następujące błędy hello tooview czynności przy użyciu pulpitu zdalnego:

1. Upewnij się, że Azure SDK 1.3 lub nowszy jest zainstalowany.
2. Podczas wdrażania hello hello rozwiązania przy użyciu programu Visual Studio, wybierz za "Konfigurowanie pulpitu zdalnego połączeń...". Aby uzyskać więcej informacji na temat konfigurowania hello Podłączanie pulpitu zdalnego, zobacz [za pomocą pulpitu zdalnego z rolami Azure](../vs-azure-tools-remote-desktop-roles.md).
3. W hello Microsoft klasycznego portalu Azure, po wystąpieniu hello wskazuje stan **gotowe**, kliknij jeden z hello wystąpień roli.
4. Kliknij przycisk hello **Connect** ikonę w hello **dostępu zdalnego** obszaru hello wstążki.
5. Zaloguj przy użyciu poświadczeń hello, które zostały określone podczas konfigurowania usług pulpitu zdalnego hello toohello maszyny wirtualnej.
6. Otwórz okno poleceń.
7. Wpisz polecenie `IPconfig`.
8. Zanotuj wartość adres IPV4 hello.
9. Otwórz program Internet Explorer.
10. Wpisz adres hello i nazwa hello hello aplikacji sieci web. Na przykład `http://<IPV4 Address>/default.aspx`.

Nawigowanie po toohello witryny sieci Web zwróci teraz dokładniejsze komunikaty o błędach:

* Błąd serwera w "/" aplikacji.
* Opis: Wystąpił nieobsługiwany wyjątek podczas wykonywania bieżącego żądania sieci web hello hello. Przejrzyj ślad stosu hello, aby uzyskać więcej informacji o błędzie hello i miejscu jego występowania w kodzie hello.
* Szczegóły wyjątku: System.IO.FIleNotFoundException: nie można załadować pliku lub zestawu "Microsoft.WindowsAzure.StorageClient, wersja = 1.1.0.0, Culture = neutral, PublicKeyToken = 31bf856ad364e35" lub jednej z jego zależności. Witaj, system nie może odnaleźć określonego pliku hello.

Na przykład:

![Błąd serwera jawne w '/' aplikacji](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a>Diagnozowanie problemów przy użyciu emulatora obliczeń hello
Można użyć toodiagnose emulatora obliczeń hello w Microsoft Azure i rozwiązywanie problemów z brakujących zależności i błędy w pliku web.config.

Aby uzyskać najlepsze wyniki za pomocą tej metody diagnostyki należy używać komputer lub maszynę wirtualną, która ma czystą instalację systemu Windows. toobest symulować hello środowiska platformy Azure, należy użyć systemu Windows Server 2008 R2 x64.

1. Zainstaluj wersję autonomicznej hello hello [zestawu Azure SDK](https://azure.microsoft.com/downloads/).
2. Na komputerze deweloperskim hello kompilacji hello projekt usługi w chmurze.
3. W Eksploratorze Windows przejdź folderu bin\debug toohello hello projekt usługi w chmurze.
4. Skopiuj folder csx hello i komputera toohello pliku .cscfg używasz toodebug hello problemy.
5. Na powitania oczyszczania komputera, Otwórz okno wiersza polecenia Azure SDK i wpisz `csrun.exe /devstore:start`.
6. Wpisz w wierszu polecenia hello `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.
7. Po uruchomieniu roli hello, zobaczysz szczegółowe informacje o błędzie w programie Internet Explorer. Można również użyć standardowego systemu Windows, narzędzia do rozwiązywania problemów toofurther zdiagnozować hello problem.

## <a name="diagnose-issues-by-using-intellitrace"></a>Diagnozowanie problemów przy użyciu funkcji IntelliTrace
Dla procesu roboczego oraz role sieci web, które używają programu .NET Framework 4, możesz użyć [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), która jest dostępna w programie Microsoft Visual Studio Enterprise.

Wykonaj te kroki toodeploy hello usługi przy użyciu funkcji IntelliTrace włączone:

1. Potwierdź, że zestaw Azure SDK 1.3 lub nowszej jest zainstalowane.
2. Wdrażanie rozwiązania hello przy użyciu programu Visual Studio. Podczas wdrażania, sprawdź hello **włączenia funkcji IntelliTrace dla ról platformy .NET 4** pole wyboru.
3. Po uruchomieniu wystąpienia hello Otwórz hello **Eksploratora serwera**.
4. Rozwiń węzeł hello **Azure\\usługi w chmurze** węzła i Znajdź hello wdrożenie.
5. Rozwiń hello wdrożenia do momentu wyświetlenia hello wystąpień roli. Kliknij prawym przyciskiem myszy na jednym z wystąpień hello.
6. Wybierz **dzienniki IntelliTrace widoku**. Witaj **Podsumowanie funkcji IntelliTrace** zostanie otwarty.
7. Zlokalizuj hello wyjątki części hello podsumowania. Jeśli istnieją wyjątki, zostaną oznaczone etykietą sekcji hello **wyjątku**.
8. Rozwiń węzeł hello **wyjątku** i poszukaj **System.IO.FileNotFoundException** błędy podobne toohello poniżej:

![Dane wyjątku, Brak pliku lub zestawu](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a>Brak biblioteki dll i zestawy adresów
tooaddress Brak biblioteki DLL i zestawu błędów, wykonaj następujące kroki:

1. Otwórz rozwiązanie hello w programie Visual Studio.
2. W **Eksploratora rozwiązań**, otwórz hello **odwołania** folderu.
3. Kliknij zestaw hello objęci hello błąd.
4. W hello **właściwości** okienku Znajdź **właściwości kopii lokalnej** i ustaw wartość hello zbyt**True**.
5. Należy ponownie wdrożyć usługę w chmurze hello.

Po upewnieniu się, że wszystkie błędy zostaną naprawione, można wdrożyć usługi hello bez sprawdzania hello **włączenia funkcji IntelliTrace dla ról platformy .NET 4** pole wyboru.

## <a name="next-steps"></a>Następne kroki
Wyświetl więcej [Rozwiązywanie problemów z artykułów](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) dla usług w chmurze.

toolearn jak roli usługi w chmurze tootroubleshoot problemów przy użyciu danych diagnostycznych komputera Azure PaaS, zobacz [serii blogu Kevina Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
