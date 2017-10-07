---
title: "aaaEnabling dostępu zdalnego we wdrożeniach Azure w programie Eclipse"
description: "Dowiedz się, jak dostęp zdalny tooenable wdrożeń platformy Azure przy użyciu hello Azure zestawu narzędzi dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Włączanie dostępu zdalnego dla wdrożeń platformy Azure w programie Eclipse
toohelp Rozwiązywanie problemów z wdrożeń, można włączyć i używać dostępu zdalnego tooconnect toohello hostowania maszyn wirtualnych wdrożenia. Witaj funkcje dostępu zdalnego zależy od hello protokołu RDP (Remote Desktop). Po opublikowaniu go tooAzure lub jeśli Eclipse korzystają z systemu operacyjnego, można skonfigurować dostęp zdalny, przed opublikowaniem tooAzure, można skonfigurować dostęp zdalny dla danego wdrożenia. Należy pamiętać, że konieczne będzie klient usług pulpitu zdalnego, który jest zgodny z systemem operacyjnym w wdrożenia kolejności tooconnect tooyour maszyny wirtualnej platformy Azure.

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a>Jak tooenable dostępu zdalnego, aby wdrożyć tooAzure
> [!NOTE]
> tooenable dostępu zdalnego przed wdrożeniem programu tooAzure aplikacji należy toobe uruchamianie Eclipse w systemie Windows.
> 
> 

Witaj poniższy obraz przedstawia hello **dostępu zdalnego** okna dialogowego właściwości używany tooenable dostępu zdalnego.

![][ic719494]

Istnieją dwa sposoby toodisplay hello **dostępu zdalnego** okno dialogowe właściwości:

* Kliknij przycisk hello **zaawansowane** łącze w hello **dostępu zdalnego** sekcji hello **publikowania tooAzure** okna dialogowego.

* Otwórz hello **właściwości** okna dialogowego projektu platformy Azure.

Podczas tworzenia nowego projektu wdrożenia usługi Azure hello projektu nie będzie miał dostępu zdalnego domyślnie włączone. Jednak łatwo można włączyć dostęp zdalny, określając hello nazwy użytkownika i hasła w hello **publikowania tooAzure** okna dialogowego. Hello hasła dostępu zdalnego jest szyfrowane za pomocą certyfikatów X.509. Jeśli nie używasz dostarczyć własny certyfikat szyfrowania hello korzysta z certyfikatu z podpisem własnym dostarczone z hello Azure dodatek dla programu Eclipse. Certyfikat z podpisem własnym jest hello **cert** folderu projektu platformy Azure, przechowywane zarówno jako plik certyfikatu publicznego (SampleRemoteAccessPublic.cer) i jako wymiany informacji osobistych (PFX) (pliku certyfikatu SampleRemoteAccessPrivate.pfx). ostatnie Hello zawiera hello klucza prywatnego dla certyfikatu hello i ma domyślne hasło, **Password1**. Jednak ponieważ hasło jest publiczny wiedzy, powinien być używany certyfikat domyślny hello tylko w przypadku uczenia celów, nie w przypadku wdrożenia produkcyjnego. Tak innych niż do uczenia celów, jeśli chcesz tooenabled sesji zdalnych wdrożeń, należy kliknąć opcję hello **zaawansowane** łącze w hello **publikowania tooAzure** toospecify okna dialogowego własne certyfikat. Należy pamiętać, że musisz mieć wersję PFX hello tooupload hello certyfikatu tooyour hostowanej usługi w ramach hello portalu zarządzania Azure, tak że Azure może odszyfrować hasła użytkownika hello.

Witaj pozostałej części samouczka hello pokazuje, jak dostęp zdalny tooenable dla projektu wdrożenia usługi Azure, która została początkowo utworzona dostęp zdalny wyłączony. Do celów tego samouczka utworzymy nowy certyfikat z podpisem własnym, a jego plik PFX będzie miał hasła wybranych przez użytkownika. Istnieje również opcja hello przy użyciu certyfikatu wystawionego przez urząd certyfikacji.

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a>Jak tooenable dostępu zdalnego po wdrożeniu tooAzure
dostęp zdalny tooenable po wdrożeniu tooAzure, użyj hello następujące kroki:

1. Zaloguj się do portalu zarządzania Azure hello przy użyciu konta platformy Azure

2. Na liście **usługi w chmurze**, wybierz usługi w chmurze wdrożone

3. Na stronie sieci web usługi chmury hello, kliknij przycisk hello **Konfiguruj** łącza

4. Na dole hello hello na stronie konfiguracji, kliknij przycisk hello **zdalnego** łącza

5. Kiedy wyświetli się okno podręczne okno dialogowe hello:
   
   * Określ hello rolę dla której ma zostać tooenable dostępu zdalnego

   * Kliknij przycisk tooselect hello **Włącz pulpit zdalny** wyboru
   
   * Określ nazwę użytkownika i hasło mają toouse dla dostępu zdalnego
   
   * Wybierz hello toouse certyfikatu

6. Kliknij przycisk **OK**. 

Zostanie wyświetlony komunikat informujący, że zmiany konfiguracji jest w toku, co może potrwać kilka minut toocomplete. Po zakończeniu hello zmianę konfiguracji, wykonaj kroki hello hello **toolog w zdalnie** sekcji w dalszej części tego artykułu.

## <a name="how-tooenable-remote-access-in-your-package"></a>W jaki sposób tooenable zdalnego dostępu do pakietu
1. W okienku Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy projekt platformy Azure, a następnie kliknij przycisk **właściwości**.

2. W hello **właściwości** okna dialogowego, rozwiń węzeł **Azure** w okienku po lewej stronie powitania i kliknij przycisk **dostępu zdalnego**.

3. W hello **dostępu zdalnego** okna dialogowego, upewnij się, **Włącz wszystkie role tooaccept połączeń pulpitu zdalnego przy użyciu tych poświadczeń logowania** jest zaznaczony.

4. Określ nazwę użytkownika dla hello Podłączanie pulpitu zdalnego.

5. Określ i Potwierdź hasło hello hello użytkownika. Witaj użytkownika nazwę i hasło wartości w tym oknie dialogowym będą używane podczas tworzenia połączenia pulpitu zdalnego. (Należy zauważyć, że jest to oddzielnych haseł z hasła do pliku PFX).

6. Określ datę wygaśnięcia hello hello konta użytkownika.

7. Kliknij przycisk **nowy** toocreate nowego certyfikatu z podpisem własnym. (Można również należy wybierać certyfikat z obszaru roboczego lub pliku systemu za pośrednictwem hello **obszaru roboczego** lub **FileSystem** przyciski, odpowiednio, ale dla celów tego samouczka, utworzymy nową certyfikat).

   * W hello **nowego świadectwa** okna dialogowego, określ i Potwierdź hasło hello użyjesz dla pliku PFX.

   * Zaakceptuj wartość hello **nazwa (CN)**, lub użyj nazwy niestandardowej.

   * Określ hello ścieżka i nazwa pliku którym zostanie zapisany nowy certyfikat hello w postaci cer. Dla tego kroku i hello następnego kroku, możesz użyć hello **cert** folderu projektu platformy Azure, ale w przypadku wolnego toochoose innej lokalizacji. Do celów tego samouczka, użyjemy **c:\mycert\mycert.cer**. (Tworzenie hello **c:\mycert** tooproceeding poprzedniego folderu lub użyj istniejącego folderu, w razie potrzeby.)

   * Określ hello ścieżka i nazwa pliku którym zostanie zapisany hello nowego certyfikatu i klucza prywatnego, w postaci pliku pfx. Do celów tego samouczka, użyjemy **c:\mycert\mycert.pfx**. Twoje **nowego świadectwa** okna dialogowego powinna wyglądać podobnie następujące toohello (Zaktualizuj hello ścieżki folderu, jeśli nie używasz **c:\mycert**):
     
      ![][ic712275]

   * Kliknij przycisk **OK** tooclose hello **nowego świadectwa** okna dialogowego.

8. Twoje **dostępu zdalnego** okna dialogowego powinna wyglądać podobnie toohello następujące:</p>
   
   ![][ic719495]

9. Kliknij przycisk **OK** tooclose hello **dostępu zdalnego** okna dialogowego.

Aplikacja jest ponownie kompilowana, hello kompilacji zestawu dla wdrożenia toocloud.

## <a name="toolog-in-remotely"></a>toolog w zdalnie
Gdy wystąpienie roli jest gotowy, może zdalnie zalogować toohello maszyny wirtualnej, który jest hostem aplikacji.

* Jeśli używasz programu Eclipse w systemach Windows i wybranych hello **wdrożyć uruchomienia pulpitu zdalnego na** opcja podczas tooAzure Twojego wdrożenia, zostanie wyświetlona Podłączanie pulpitu zdalnego ekran logowania po uruchomieniu wdrożenia. Po wyświetleniu monitu o hello nazwy użytkownika i hasła, wprowadź wartości hello, określone dla użytkownika zdalnego hello i będą mogli toolog w.

* Inny sposób toolog w zdalnie odbywa się za pośrednictwem hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">portalu zarządzania Azure</a>:
  
  * W ramach hello **usługi w chmurze** widok hello portalu zarządzania Azure, kliknij pozycję usługi w chmurze, kliknij przycisk **wystąpień**, kliknij przycisk określonego wystąpienia, a następnie kliknij przycisk hello **Connect**przycisku. Witaj **Connect** przycisk pojawia się następujący hello na pasku poleceń hello:
    
      ![][ic659273]

  * Po kliknięciu przycisku hello **Connect** przycisku będzie tooopen zostanie wyświetlony monit o plik RDP. Otwórz plik hello i postępuj zgodnie z monitami hello. (Możesz można także zapisać komputera lokalnego tooyour pliku, a następnie uruchom plik hello przez dwukrotne kliknięcie dziennika tooremote w tooyour maszyny wirtualnej bez konieczności toofirst Przejdź w portalu zarządzania hello.)

  * Po wyświetleniu monitu o hello nazwy użytkownika i hasła, wprowadź wartości hello, określone dla użytkownika zdalnego hello i będą mogli toolog w.

> [!NOTE]
> Jeśli w systemie operacyjnym z systemem innym niż Windows, należy toouse klienta pulpitu zdalnego, który jest zgodny z systemem operacyjnym i wykonaj tooconfigure kroki powitania klienta z ustawieniami hello w pliku RDP hello.
> 
> 

## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse][Installing hello Azure Toolkit for Eclipse] 

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
