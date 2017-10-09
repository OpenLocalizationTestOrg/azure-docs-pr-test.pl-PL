---
title: "aaaSign w instrukcje dotyczące hello Azure Toolkit for IntelliJ | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosign w tooMicrosoft Azure przy użyciu hello Azure Toolkit for IntelliJ."
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ

Hello Azure Toolkit for IntelliJ udostępnia dwie metody logowania tooyour konto platformy Azure:

  * **Interakcyjne**: Wprowadź każdym logowaniu poświadczenia platformy Azure w tooyour konto platformy Azure.
  * **Automatyczne**: Utwórz plik poświadczeń w tooyour konto platformy Azure można tooautomatically logowania.

Witaj poniższych sekcjach opisano sposób toouse każdej metody.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>Zaloguj się interaktywnie tooyour konto platformy Azure

toosign w tooAzure ręcznie wprowadzić poświadczenia platformy Azure, hello następujące:

1. Otwórz projekt z IntelliJ IDEA.

2. Kliknij przycisk **narzędzia**, punktu zbyt**Azure**, a następnie kliknij przycisk **Azure logowania**.

   ![Witaj polecenia IntelliJ Azure logowania][I01]

3. W hello **Azure logowania** wybierz **Interactive**, a następnie kliknij przycisk **Zaloguj**.

   ![Hello Azure logowania okna z Interactive wybrane][I02]

4. W hello **Azure dziennika w** zostanie wyświetlone okno dialogowe, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **Zaloguj**.

   ![okno dialogowe logowania Azure Hello][I03]

5. W hello **Wybierz subskrypcje** okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.

   ![Wybierz subskrypcje Hello — okno dialogowe][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Wylogować się z konta platformy Azure, po zarejestrowaniu trybie interakcyjnym

Po skonfigurowaniu konta przy użyciu hello w poprzednich krokach, użytkownik będzie automatyczne wylogowanie z konta platformy Azure każdorazowo po ponownym uruchomieniu IntelliJ IDEA. Jednak jeśli chcesz toosign poza konta platformy Azure *bez* ponowne uruchomienie IntelliJ IDEA hello następujące.

1. W IntelliJ IDEA, na powitania **narzędzia** menu punktu zbyt**Azure**, a następnie kliknij przycisk **Azure Wyloguj**.

   ![Witaj IntelliJ Azure Wyloguj polecenia][L01]

2. W hello **Azure Wyloguj** oknie potwierdzenia kliknij **tak**.

   ![Hello Azure Wyloguj okno potwierdzenia][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>Zaloguj się automatycznie tooyour konto platformy Azure

Ta sekcja przeprowadzi Cię przez proces tworzenia pliku poświadczeń, który zawiera dane główne usługi. Po zakończeniu tego procesu Eclipse używa hello poświadczenia pliku tooautomatically logowania się, że w każdym tooAzure czasu Otwórz projekt.

1. Otwórz projekt z IntelliJ IDEA.

2. Na powitania **narzędzia** menu punktu zbyt**Azure**, a następnie kliknij przycisk **Azure logowania**.

   ![Witaj polecenia IntelliJ Azure logowania][A01]

3. W hello **Azure logowania** wybierz **automatycznego**, a następnie kliknij przycisk **nowy**.

   ![Hello Azure logowania okna z automatycznego wybrane][A02]

4. W hello **dialogowym logowania do usługi Azure** okna, wprowadź swoje poświadczenia usługi Azure, a następnie kliknij przycisk **Zaloguj**.

   ![okno dialogowe logowania Azure Hello][A03]

5. W hello **tworzenia plików uwierzytelniania** okna, wybierz hello subskrypcje mają toouse, wybierz katalogu docelowego, a następnie kliknij przycisk **Start**.

   ![Witaj okna Tworzenie plików uwierzytelniania][A04]

6. W hello **stan tworzenia nazwy głównej usługi** okno dialogowe po Twoje pliki zostały utworzone pomyślnie, kliknij przycisk **OK**.

   ![Witaj okno dialogowe Stan tworzenia nazwy głównej usługi][A05]

7. W hello **Azure logowania** okna, kliknij przycisk **Zaloguj**.

   ![Okno dialogowe logowania do platformy Azure][A06]

8. W hello **Wybierz subskrypcje** okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.

   ![Wybierz subskrypcje Hello — okno dialogowe][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Wylogować się z konta platformy Azure po zalogowaniu się automatycznie

Po skonfigurowaniu konta przy użyciu poprzednich krokach hello, hello Azure Toolkit automatycznie loguje się użytkownik tooyour każdorazowo po ponownym uruchomieniu IntelliJ IDEA konto platformy Azure. Jednak toosign poza konta platformy Azure i zapobiec hello Azure Toolkit z automatycznego rejestrowania, hello następujące:

1. W IntelliJ IDEA, na powitania **narzędzia** menu punktu zbyt**Azure**, a następnie kliknij przycisk **Azure Wyloguj**.

   ![Witaj IntelliJ Azure Wyloguj polecenia][L01]

2. W hello **Azure Wyloguj** oknie potwierdzenia kliknij **tak**.

   ![Hello Azure Wyloguj okno potwierdzenia][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>Zaloguj się tooyour konta Azure automatycznie przy użyciu istniejącego pliku poświadczeń

Jeśli możesz wylogować się z konta platformy Azure, korzystając z IntelliJ IDEA, należy użyć znaku tooautomatically pliku istniejących poświadczeń w toohello konta. tooconfigure hello Azure zestawu narzędzi dla programu Eclipse toouse istniejący plik poświadczeń, hello następujące:

1. Otwórz projekt z IntelliJ IDEA.

2. Na powitania **narzędzia** menu punktu zbyt**Azure**, a następnie kliknij przycisk **Azure logowania**.

   ![Witaj polecenia IntelliJ Azure logowania][A01]

3. W hello **Azure logowania** wybierz **automatycznego**, a następnie kliknij przycisk **Przeglądaj**.

   ![Hello Azure logowania okna z automatycznego wybrane][A02]

4. W hello **wybierz plik Authentication** okno dialogowe, wybierz plik utworzonej wcześniej poświadczenia, a następnie kliknij **wybierz**.

   ![Wybierz plik Authentication Hello — okno dialogowe][A08]

5. W hello **Azure logowania** okna, kliknij przycisk **Zaloguj**.

   ![Hello Azure logowania okna z automatycznego wybrane][A06]

6. W hello **Wybierz subskrypcje** okno dialogowe, wybierz hello subskrypcje mają toouse, a następnie kliknij przycisk **OK**.

   ![Wybierz subskrypcje Hello — okno dialogowe][A07]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat hello narzędzi Azure dla języka Java IDEs Zobacz hello następującego łącza:

* [Azure zestawu narzędzi dla programu Eclipse]
  * [What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w programie Eclipse]
* [Azure Toolkit for IntelliJ] (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
  * [What's new in hello Azure Toolkit for IntelliJ]
  * [Instalowanie hello Azure Toolkit for IntelliJ]
  * *Logowanie instrukcje dotyczące hello Azure Toolkit for IntelliJ* (w tym artykule)
  * [Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].

<!-- URL List -->

[Azure zestawu narzędzi dla programu Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Zestaw narzędzi platformy Azure dla środowiska IntelliJ)
[Tworzenie aplikacji sieci Web Hello World na platformie Azure w programie Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Tworzenie aplikacji sieci web Hello World na platformie Azure w IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalowanie hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalowanie hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instrukcje logowania hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's new in hello zestawu narzędzi platformy Azure dla programu Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[What's new in hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
