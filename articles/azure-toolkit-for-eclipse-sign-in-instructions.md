---
title: "aaaSign w instrukcji dla zestawu narzędzi platformy Azure dla programu Eclipse hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosign w Microsoft Azure przy użyciu hello zestawu narzędzi platformy Azure dla programu Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a>Azure znak w instrukcji hello zestawu narzędzi platformy Azure dla programu Eclipse

zestaw narzędzi platformy Azure dla programu Eclipse Hello udostępnia dwie metody logowanie do konta platformy Azure:

  * **Interakcyjne** — gdy używana jest ta metoda będzie wprowadź swoje poświadczenia usługi Azure każdym logowaniu się do konta platformy Azure.
  * **Automatyczne** — w przypadku korzystania z tej metody spowoduje utworzenie pliku poświadczeń, który zawiera dane główne usługi, po upływie którego można użyć hello poświadczenia pliku tooautomatically logowania do konta platformy Azure.

Witaj kroki hello w następujących sekcjach opisano sposób toouse każdej metody.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Interakcyjne logowanie do konta platformy Azure

Witaj poniższe kroki przedstawiają sposób toosign na platformie Azure ręcznie wprowadzić poświadczenia platformy Azure.

1. Otwórz projekt z Eclipse.

1. Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.

   ![Menu Eclipse Azure w celu logowania się][I01]

1. Gdy hello **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **Interactive**, a następnie kliknij przycisk **logowania**.

   ![Zaloguj się okno dialogowe][I02]

1. Gdy hello **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **logowania**.

   ![Okno dialogowe logowania do platformy Azure][I03]

1. Gdy hello **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.

   ![Wybierz subskrypcje — okno dialogowe][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Podpisywanie poza konta platformy Azure po zalogowaniu trybie interakcyjnym

Po skonfigurowaniu hello kroki opisane w poprzedniej sekcji hello, zostaną automatycznie wylogowani z konta platformy Azure każdorazowo po ponownym uruchomieniu programu Eclipse. Jednak jeśli chcesz toosign poza konta platformy Azure bez ponownego uruchamiania programu Eclipse, użyj hello następujące kroki.

1. W programie Eclipse kliknij **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **Wyloguj**.

   ![Menu Eclipse Azure wylogowaniu][L01]

1. Gdy hello **Azure Wyloguj** zostanie wyświetlone okno dialogowe, kliknij przycisk **tak**.

   ![Wyloguj się okno dialogowe][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a>Automatyczne logowanie do konta platformy Azure i tworzenia poświadczeń dla plików toouse w hello przyszłych

Witaj następujące kroki przeprowadzi Cię przez proces tworzenia pliku poświadczeń, który zawiera dane główne usługi. Po wykonaniu tych kroków, Eclipse zostanie automatycznie użyj hello poświadczenia pliku tooautomatically logowania się, że możesz w każdej Azure czasu Otwórz projekt.

1. Otwórz projekt z Eclipse.

1. Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.

   ![Menu Eclipse Azure w celu logowania się][A01]

1. Gdy hello **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **automatycznego**, a następnie kliknij przycisk **nowy**.

   ![Zaloguj się okno dialogowe][A02]

1. Gdy hello **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **logowania**.

   ![Okno dialogowe logowania do platformy Azure][A03]

1. Gdy hello **tworzenia plików uwierzytelniania** zostanie wyświetlone okno dialogowe, wybierz hello subskrypcje mają toouse, wybierz katalogu docelowego, a następnie kliknij przycisk **Start**.

   ![Okno dialogowe logowania do platformy Azure][A04]

1. Witaj **stan Creatation nazwy głównej usługi** zostanie wyświetlone okno dialogowe i po Twoje pliki zostały utworzone pomyślnie, kliknij przycisk **OK**.

   ![Okno dialogowe Stan Creatation nazwy głównej usługi][A05]

1. Gdy hello **Azure logowania** zostanie wyświetlone okno dialogowe, kliknij przycisk **logowania**.

   ![Okno dialogowe logowania do platformy Azure][A06]

1. Gdy hello **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.

   ![Wybierz subskrypcje — okno dialogowe][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Podpisywanie poza konta platformy Azure po zalogowaniu automatycznie

Po skonfigurowaniu hello kroki opisane w poprzedniej sekcji hello hello Azure Toolkit spowoduje automatyczne zalogowanie do konta platformy Azure każdorazowo po ponownym uruchomieniu programu Eclipse. Jednak toosign poza konta platformy Azure i uniemożliwić hello Azure Toolkit podczas logowania automatycznie, użyj hello następujące kroki.

1. W programie Eclipse kliknij **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **Wyloguj**.

   ![Menu Eclipse Azure wylogowaniu][L01]

1. Gdy hello **Azure Wyloguj** zostanie wyświetlone okno dialogowe, kliknij przycisk **tak**.

   ![Wyloguj się okno dialogowe][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Logowanie do konta platformy Azure automatycznie przy użyciu pliku poświadczeń, które zostały już utworzone

Jeśli możesz wylogować się z platformy Azure, korzystając z programu Eclipse, konieczne będzie tooreconfigure hello Azure zestawu narzędzi dla programu Eclipse toouse pliku poświadczeń, które zostały utworzone, aby automatycznie mógł zalogować się na konto platformy Azure. Hello poniższe kroki objaśniają Konfigurowanie hello Azure Toolkit toouse istniejący plik poświadczeń.

1. Otwórz projekt z Eclipse.

1. Kliknij przycisk **narzędzia**, następnie kliknij przycisk **Azure**, a następnie kliknij przycisk **logowania**.

   ![Menu Eclipse Azure w celu logowania się][A01]

1. Gdy hello **Azure logowania** zostanie wyświetlone okno dialogowe, wybierz **automatycznego**, a następnie kliknij przycisk **Przeglądaj**.

   ![Zaloguj się okno dialogowe][A02]

1. Gdy hello **wybierz plik uwierzytelniony** zostanie wyświetlone okno dialogowe, wybierz plik poświadczeń, który został utworzony wcześniej, a następnie kliknij przycisk **wybierz**.

   ![Zaloguj się okno dialogowe][A08]

1. Gdy hello **Azure logowania** zostanie wyświetlone okno dialogowe, kliknij przycisk **logowania**.

   ![Okno dialogowe logowania do platformy Azure][A06]

1. Gdy hello **Wybierz subskrypcje** zostanie wyświetlone okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.

   ![Wybierz subskrypcje — okno dialogowe][A07]

## <a name="see-also"></a>Zobacz też
Aby uzyskać więcej informacji na temat hello narzędzi Azure dla języka Java IDEs Zobacz hello następującego łącza:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * *Zaloguj się w instrukcji hello zestawu narzędzi platformy Azure dla programu Eclipse (w tym artykule)*
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [Nowości w hello Azure Toolkit for IntelliJ]
  * [Instalowanie hello Azure Toolkit for IntelliJ]
  * [Zaloguj się w instrukcji hello Azure Toolkit for IntelliJ]
  * [Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Zaloguj się w instrukcji hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nowości w hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Nowości w hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
