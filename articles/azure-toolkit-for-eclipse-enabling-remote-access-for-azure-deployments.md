---
title: "Włączanie dostępu zdalnego dla wdrożeń platformy Azure w programie Eclipse"
description: "Dowiedz się, jak włączyć dostęp zdalny dla wdrożeń platformy Azure przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse."
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
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Włączanie dostępu zdalnego dla wdrożeń platformy Azure w programie Eclipse
Do rozwiązywania problemów wdrożeń, można włączyć i używać dostępu zdalnego do nawiązania połączenia hostowania wdrożenia maszyn wirtualnych. Funkcje dostępu zdalnego polega na protokołu RDP (Remote Desktop). Dostęp zdalny można skonfigurować dla danego wdrożenia po opublikowano na platformie Azure, lub jeśli Eclipse korzystają z systemu operacyjnego, można skonfigurować dostęp zdalny przed publikowanie na platformie Azure. Należy pamiętać, że konieczne będzie klient usług pulpitu zdalnego, który jest zgodny z systemu operacyjnego w celu nawiązania połączenia z wdrożenia maszyny wirtualnej platformy Azure.

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a>Jak włączyć dostęp zdalny, przed wdrożeniem na platformie Azure
> [!NOTE]
> Aby włączyć dostęp zdalny, przed wdrożeniem aplikacji na platformie Azure, musi działać w środowisku Eclipse w systemie Windows.
> 
> 

Poniższy obraz przedstawia **dostępu zdalnego** okna dialogowego właściwości włączania dostępu zdalnego.

![][ic719494]

Istnieją dwa sposoby wyświetlania **dostępu zdalnego** okno dialogowe właściwości:

* Kliknij przycisk **zaawansowane** łącze w **dostępu zdalnego** sekcji **publikowania na platformie Azure** okna dialogowego.

* Otwórz **właściwości** okna dialogowego projektu platformy Azure.

Podczas tworzenia nowego projektu wdrożenia usługi Azure projektu nie będzie miał dostępu zdalnego domyślnie włączone. Jednak łatwo można włączyć dostęp zdalny, określając nazwę użytkownika i hasło w **publikowania na platformie Azure** okna dialogowego. Hasła dostępu zdalnego jest szyfrowane za pomocą certyfikatów X.509. Jeśli nie używasz dostarczyć własny certyfikat szyfrowania korzysta z certyfikatu z podpisem własnym dostarczone z wtyczki Azure dla programu Eclipse. Certyfikat z podpisem własnym jest **cert** folderu projektu platformy Azure, przechowywane zarówno jako plik certyfikatu publicznego (SampleRemoteAccessPublic.cer) i jako wymiany informacji osobistych (PFX) (pliku certyfikatu SampleRemoteAccessPrivate.pfx). Zawiera klucz prywatny certyfikatu i ma domyślne hasło, **Password1**. Jednak ponieważ hasło jest publiczny wiedzy, powinien być używany certyfikat domyślny tylko w przypadku uczenia celów, nie w przypadku wdrożenia produkcyjnego. Dlatego inne niż do uczenia celów, jeśli chcesz włączyć sesji zdalnych wdrożeń, należy kliknąć opcję **zaawansowane** łącze w **publikowania na platformie Azure** okna dialogowego, aby określić własny certyfikat. Należy pamiętać, że musisz przekazać wersja PFX certyfikatu w usłudze hostowanej w portalu zarządzania Azure, tak że Azure może odszyfrować hasła użytkownika.

W pozostałej części samouczka przedstawiono sposób włączania dostępu zdalnego dla projektu wdrożenia usługi Azure, która została początkowo utworzona dostęp zdalny wyłączony. Do celów tego samouczka utworzymy nowy certyfikat z podpisem własnym, a jego plik PFX będzie miał hasła wybranych przez użytkownika. Istnieje również możliwość z użyciem certyfikatu wydanego przez urząd certyfikacji.

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a>Jak włączyć dostęp zdalny, po wdrożeniu na platformie Azure
Aby włączyć dostęp zdalny, po wdrożeniu na platformie Azure, wykonaj następujące kroki:

1. Zaloguj się do portalu zarządzania platformy Azure przy użyciu konta platformy Azure

2. Na liście **usługi w chmurze**, wybierz usługi w chmurze wdrożone

3. Na stronie sieci web usługi chmury kliknij **Konfiguruj** łącza

4. W dolnej części strony konfiguracji, kliknij polecenie **zdalnego** łącza

5. Kiedy wyświetli się okno podręczne okno dialogowe:
   
   * Określ rolę, dla której ma być włączyć dostęp zdalny

   * Kliknij, aby wybrać **Włącz pulpit zdalny** wyboru
   
   * Określ nazwę użytkownika i hasło, którego chcesz użyć dla dostępu zdalnego
   
   * Wybierz certyfikat do użycia

6. Kliknij przycisk **OK**. 

Zostanie wyświetlony komunikat informujący, że zmiany konfiguracji jest w toku, co może potrwać kilka minut. Po zmianie konfiguracji została ukończona, postępuj zgodnie z instrukcjami **zdalnego logowania** sekcji w dalszej części tego artykułu.

## <a name="how-to-enable-remote-access-in-your-package"></a>Jak włączyć dostęp zdalny do pakietu
1. W okienku Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy projekt platformy Azure, a następnie kliknij przycisk **właściwości**.

2. W **właściwości** okna dialogowego, rozwiń węzeł **Azure** w okienku po lewej stronie i kliknij przycisk **dostępu zdalnego**.

3. W **dostępu zdalnego** okna dialogowego, upewnij się, **Włącz wszystkie role do akceptowania połączeń pulpitu zdalnego przy użyciu tych poświadczeń logowania** jest zaznaczony.

4. Określ nazwę użytkownika dla połączenia pulpitu zdalnego.

5. Określ i Potwierdź hasło dla użytkownika. Wartości nazwy i hasła użytkownika w tym oknie dialogowym będą używane podczas tworzenia połączenia pulpitu zdalnego. (Należy zauważyć, że jest to oddzielnych haseł z hasła do pliku PFX).

6. Określ datę wygaśnięcia konta użytkownika.

7. Kliknij przycisk **nowy** można utworzyć nowego certyfikatu z podpisem własnym. (Można również należy wybierać certyfikat z obszaru roboczego lub pliku systemu za pośrednictwem **obszaru roboczego** lub **FileSystem** przyciski, odpowiednio, ale dla celów tego samouczka, utworzymy nową certyfikat).

   * W **nowego świadectwa** okna dialogowego, określ i Potwierdź hasło będzie używany dla pliku PFX.

   * Zaakceptuj wartość podana dla **nazwa (CN)**, lub użyj nazwy niestandardowej.

   * Określ ścieżkę i nazwę, którym zostanie zapisany nowy certyfikat w formie cer. Ten krok i następnego kroku, możesz użyć **cert** folderu projektu platformy Azure, ale jest wolny wybrać inną lokalizację. Do celów tego samouczka, użyjemy **c:\mycert\mycert.cer**. (Tworzenie **c:\mycert** folderu przed kontynuowaniem lub użyj istniejącego folderu, w razie potrzeby.)

   * Określ ścieżkę i nazwę, którym zostanie zapisany nowy certyfikat i jego klucz prywatny, w postaci pliku pfx. Do celów tego samouczka, użyjemy **c:\mycert\mycert.pfx**. Twoje **nowego świadectwa** okna dialogowego powinien wyglądać podobnie do następującego (aktualizacja ścieżki folderu, jeśli nie używasz **c:\mycert**):
     
      ![][ic712275]

   * Kliknij przycisk **OK** zamknąć **nowego świadectwa** okna dialogowego.

8. Twoje **dostępu zdalnego** okna dialogowego powinien wyglądać podobnie do następującego:</p>
   
   ![][ic719495]

9. Kliknij przycisk **OK** zamknąć **dostępu zdalnego** okna dialogowego.

Ponownie aplikacji, za pomocą kompilacji zestawu dla wdrożenia w chmurze.

## <a name="to-log-in-remotely"></a>Aby zalogować się zdalnie
Gdy wystąpienie roli jest gotowy, można zdalnie zalogować się do maszyny wirtualnej, który jest hostem aplikacji.

* Jeśli używasz programu Eclipse w systemach Windows i wybranych **wdrożyć uruchomienia pulpitu zdalnego na** opcji podczas wdrażania na platformie Azure zostaną wyświetlone Podłączanie pulpitu zdalnego ekran logowania po uruchomieniu wdrożenia. Po wyświetleniu monitu o nazwę użytkownika i hasło, wprowadź wartości określone dla użytkownika zdalnego i będą mogli się zalogować.

* Innym sposobem zdalnego logowania jest za pośrednictwem <a href="http://go.microsoft.com/fwlink/?LinkID=512959">portalu zarządzania Azure</a>:
  
  * W ramach **usługi w chmurze** widok portalu zarządzania Azure, kliknij pozycję usługi w chmurze, kliknij przycisk **wystąpień**, kliknij określonego wystąpienia, a następnie kliknij przycisk **Connect** przycisk. **Connect** przycisk pojawia się następujący na pasku poleceń:
    
      ![][ic659273]

  * Po kliknięciu przycisku **Connect** przycisku, zostanie wyświetlony monit do otwarcia pliku RDP. Otwórz plik i postępuj zgodnie z monitami. (Możesz można także zapisać ten plik na komputerze lokalnym, a następnie uruchom plik przez dwukrotne kliknięcie do zdalnego logowania się z maszyną wirtualną bez konieczności najpierw przejść do portalu zarządzania.)

  * Po wyświetleniu monitu o nazwę użytkownika i hasło, wprowadź wartości określone dla użytkownika zdalnego i będą mogli się zalogować.

> [!NOTE]
> Jeśli w systemie operacyjnym z systemem innym niż Windows, należy klienta pulpitu zdalnego, który jest zgodny z systemem operacyjnym i wykonaj kroki konfigurowania klienta przy użyciu ustawień w pliku RDP, który został pobrany.
> 
> 

## <a name="see-also"></a>Zobacz też
[Azure zestawu narzędzi dla programu Eclipse][Azure Toolkit for Eclipse]

[Tworzenie aplikacji Hello World na platformie Azure w programie Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse][Installing the Azure Toolkit for Eclipse] 

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
