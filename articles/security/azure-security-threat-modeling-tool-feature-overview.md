---
title: "aaaMicrosoft narzędzia do modelowania zagrożeń - Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat wszystkich hello funkcje dostępne w hello narzędzie modelowania zagrożeń"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="3ef34-103">Omówienie funkcji narzędzia do modelowania zagrożeń</span><span class="sxs-lookup"><span data-stu-id="3ef34-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="3ef34-104">Jesteśmy Cieszymy się, że wybrano hello toouse narzędzie modelowania zagrożeń dla Twojego zagrożeń modelowania musi!</span><span class="sxs-lookup"><span data-stu-id="3ef34-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="3ef34-105">Jeśli nie zostało to jeszcze zrobione, odwiedź stronę  **[wprowadzenie do narzędzia do modelowania zagrożeń hello](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn hello podstawy.</span><span class="sxs-lookup"><span data-stu-id="3ef34-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="3ef34-106">Naszego narzędzia są często aktualizowane, więc to przewodnik często toosee naszych najnowsze funkcje i ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="3ef34-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="3ef34-107">Klikając przycisk "Utwórz nowy Model" hello otwiera stronę początkową puste, podobne toohello obraz poniżej:</span><span class="sxs-lookup"><span data-stu-id="3ef34-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![Strona początkowa pusta](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="3ef34-109">Przy użyciu modelu zagrożeń hello utworzone przez nasz zespół w hello  **[wprowadzenie](./azure-security-threat-modeling-tool-getting-started.md)**  przykład, załóżmy dzisiaj wyewidencjonowania w narzędziu hello wszystkie funkcje hello.</span><span class="sxs-lookup"><span data-stu-id="3ef34-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![Podstawowe zagrożenia modelu](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="3ef34-111">Nawigacji</span><span class="sxs-lookup"><span data-stu-id="3ef34-111">Navigation</span></span>

<span data-ttu-id="3ef34-112">Przed rozpoczęciem pracy hello wbudowanych funkcji, przejdź na powitania główne składniki znaleziono w narzędziu hello</span><span class="sxs-lookup"><span data-stu-id="3ef34-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="3ef34-113">Elementy menu</span><span class="sxs-lookup"><span data-stu-id="3ef34-113">Menu items</span></span>

<span data-ttu-id="3ef34-114">środowisko Hello powinny być podobne tooother produkty firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3ef34-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="3ef34-115">Zacznijmy od zapoznania hello elementów menu najwyższego poziomu:</span><span class="sxs-lookup"><span data-stu-id="3ef34-115">Let’s begin by going through hello top-level menu items:</span></span>

![Elementy menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="3ef34-117">Etykieta</span><span class="sxs-lookup"><span data-stu-id="3ef34-117">Label</span></span>                               | <span data-ttu-id="3ef34-118">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="3ef34-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="3ef34-119">**Plik**</span><span class="sxs-lookup"><span data-stu-id="3ef34-119">**File**</span></span> | <ul><li><span data-ttu-id="3ef34-120">Otwórz, Zapisz i zamknij pliki</span><span class="sxs-lookup"><span data-stu-id="3ef34-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="3ef34-121">Konta logowania jednoportowej OneDrive</span><span class="sxs-lookup"><span data-stu-id="3ef34-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="3ef34-122">Udostępnij linki (Wyświetl i Edytuj)</span><span class="sxs-lookup"><span data-stu-id="3ef34-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="3ef34-123">Wyświetlanie informacji o pliku</span><span class="sxs-lookup"><span data-stu-id="3ef34-123">View File Information</span></span></li><li><span data-ttu-id="3ef34-124">Zastosuj nowy szablon tooExisting modeli</span><span class="sxs-lookup"><span data-stu-id="3ef34-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="3ef34-125">**Edytuj**</span><span class="sxs-lookup"><span data-stu-id="3ef34-125">**Edit**</span></span> | <span data-ttu-id="3ef34-126">Cofnij/ponów akcji, jak również kopię, paste i delete</span><span class="sxs-lookup"><span data-stu-id="3ef34-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="3ef34-127">**Widok**</span><span class="sxs-lookup"><span data-stu-id="3ef34-127">**View**</span></span> | <ul><li><span data-ttu-id="3ef34-128">Przełączanie między **analizy** i **projekt** widoków</span><span class="sxs-lookup"><span data-stu-id="3ef34-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="3ef34-129">Zamkniętego okna (e.g.stencils i właściwości elementu wiadomości)</span><span class="sxs-lookup"><span data-stu-id="3ef34-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="3ef34-130">Zresetuj ustawienia toodefault układu</span><span class="sxs-lookup"><span data-stu-id="3ef34-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="3ef34-131">**Diagram**</span><span class="sxs-lookup"><span data-stu-id="3ef34-131">**Diagram**</span></span> | <span data-ttu-id="3ef34-132">Dodaj lub usuń diagramy i nawigowania "karty" diagramów</span><span class="sxs-lookup"><span data-stu-id="3ef34-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="3ef34-133">**Raporty**</span><span class="sxs-lookup"><span data-stu-id="3ef34-133">**Reports**</span></span> | <span data-ttu-id="3ef34-134">Utwórz tooshare raporty HTML z innymi użytkownikami</span><span class="sxs-lookup"><span data-stu-id="3ef34-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="3ef34-135">**Pomoc**</span><span class="sxs-lookup"><span data-stu-id="3ef34-135">**Help**</span></span> | <span data-ttu-id="3ef34-136">Za pomocą narzędzia hello toohelp prowadnic</span><span class="sxs-lookup"><span data-stu-id="3ef34-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="3ef34-137">ikony Hello są skróty do menu najwyższego poziomu hello:</span><span class="sxs-lookup"><span data-stu-id="3ef34-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="3ef34-138">Ikona</span><span class="sxs-lookup"><span data-stu-id="3ef34-138">Icon</span></span>                               | <span data-ttu-id="3ef34-139">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="3ef34-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="3ef34-140">**Otwórz**</span><span class="sxs-lookup"><span data-stu-id="3ef34-140">**Open**</span></span> | <span data-ttu-id="3ef34-141">Zostanie otwarty nowy plik</span><span class="sxs-lookup"><span data-stu-id="3ef34-141">Opens a new file</span></span> |
| <span data-ttu-id="3ef34-142">**Zapisz**</span><span class="sxs-lookup"><span data-stu-id="3ef34-142">**Save**</span></span> | <span data-ttu-id="3ef34-143">Zapisuje bieżący plik</span><span class="sxs-lookup"><span data-stu-id="3ef34-143">Saves current file</span></span> |
| <span data-ttu-id="3ef34-144">**Projekt**</span><span class="sxs-lookup"><span data-stu-id="3ef34-144">**Design**</span></span> | <span data-ttu-id="3ef34-145">Przechodzi w widoku Projekt, w którym można utworzyć modeli</span><span class="sxs-lookup"><span data-stu-id="3ef34-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="3ef34-146">**Analiza**</span><span class="sxs-lookup"><span data-stu-id="3ef34-146">**Analyze**</span></span> | <span data-ttu-id="3ef34-147">Pokazuje wygenerowany zagrożeń i ich właściwości</span><span class="sxs-lookup"><span data-stu-id="3ef34-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="3ef34-148">**Dodawanie diagramu**</span><span class="sxs-lookup"><span data-stu-id="3ef34-148">**Add Diagram**</span></span> | <span data-ttu-id="3ef34-149">Dodaje nowy diagram (podobne toonew karty w programie Excel)</span><span class="sxs-lookup"><span data-stu-id="3ef34-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="3ef34-150">**Usuń diagramu**</span><span class="sxs-lookup"><span data-stu-id="3ef34-150">**Delete Diagram**</span></span> | <span data-ttu-id="3ef34-151">Usuwa bieżącego diagramu</span><span class="sxs-lookup"><span data-stu-id="3ef34-151">Deletes current diagram</span></span> |
| <span data-ttu-id="3ef34-152">**Wycinanie/kopiowanie/wklejanie**</span><span class="sxs-lookup"><span data-stu-id="3ef34-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="3ef34-153">Elementy kopii/części/past</span><span class="sxs-lookup"><span data-stu-id="3ef34-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="3ef34-154">**Cofnij/ponów**</span><span class="sxs-lookup"><span data-stu-id="3ef34-154">**Undo/Redo**</span></span> | <span data-ttu-id="3ef34-155">Cofa/ponowi wykonanie akcji</span><span class="sxs-lookup"><span data-stu-id="3ef34-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="3ef34-156">**Powiększ / pomniejszyć**</span><span class="sxs-lookup"><span data-stu-id="3ef34-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="3ef34-157">Zmienia powiększenie i diagram hello lepszego widoku</span><span class="sxs-lookup"><span data-stu-id="3ef34-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="3ef34-158">**Opinia**</span><span class="sxs-lookup"><span data-stu-id="3ef34-158">**Feedback**</span></span> | <span data-ttu-id="3ef34-159">Otwiera hello MSDN Forum</span><span class="sxs-lookup"><span data-stu-id="3ef34-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="3ef34-160">Kanwy</span><span class="sxs-lookup"><span data-stu-id="3ef34-160">Canvas</span></span>

<span data-ttu-id="3ef34-161">Hello miejsce gdzie przeciąganie i upuszczanie elementów do.</span><span class="sxs-lookup"><span data-stu-id="3ef34-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="3ef34-162">Przeciąganie i upuszczanie jest hello najszybsze i najbardziej efektywny sposób toobuild modeli.</span><span class="sxs-lookup"><span data-stu-id="3ef34-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="3ef34-163">Możesz również kliknij prawym przyciskiem myszy i wybierz z menu hello dodaje ogólnego wersje elementów hello, którego używasz, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="3ef34-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="3ef34-164">Porzucanie wzornika hello na powitania kanwy</span><span class="sxs-lookup"><span data-stu-id="3ef34-164">Dropping hello stencil on hello canvas</span></span>

![Upuść kanwy](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="3ef34-166">Kliknięcie wzornika hello</span><span class="sxs-lookup"><span data-stu-id="3ef34-166">Clicking on hello stencil</span></span>

![Właściwości elementu](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="3ef34-168">Wzorników</span><span class="sxs-lookup"><span data-stu-id="3ef34-168">Stencils</span></span>

<span data-ttu-id="3ef34-169">Gdzie można znaleźć wszystkie wzorników toouse dostępne na podstawie szablonu hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="3ef34-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="3ef34-170">Jeśli nie możesz znaleźć elementy prawo hello, spróbuj użyć innego szablonu, lub zmodyfikuj jeden toofit potrzeb.</span><span class="sxs-lookup"><span data-stu-id="3ef34-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="3ef34-171">Ogólnie rzecz biorąc powinien być stanie toofind kombinacją kategorii, takich jak hello widocznych poniżej:</span><span class="sxs-lookup"><span data-stu-id="3ef34-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="3ef34-172">Nazwa wzornika</span><span class="sxs-lookup"><span data-stu-id="3ef34-172">Stencil Name</span></span>                               | <span data-ttu-id="3ef34-173">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="3ef34-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="3ef34-174">**Proces**</span><span class="sxs-lookup"><span data-stu-id="3ef34-174">**Process**</span></span> | <span data-ttu-id="3ef34-175">Aplikacje, wtyczek przeglądarki wątków, maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="3ef34-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="3ef34-176">**Zewnętrzny**</span><span class="sxs-lookup"><span data-stu-id="3ef34-176">**External Interactor**</span></span> | <span data-ttu-id="3ef34-177">Dostawców uwierzytelniania, przeglądarek, użytkownicy, aplikacje sieci Web</span><span class="sxs-lookup"><span data-stu-id="3ef34-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="3ef34-178">**Magazyn danych**</span><span class="sxs-lookup"><span data-stu-id="3ef34-178">**Data Store**</span></span> | <span data-ttu-id="3ef34-179">Rejestr pliki, bazy danych, konfiguracji pamięci podręcznej, przechowywania,</span><span class="sxs-lookup"><span data-stu-id="3ef34-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="3ef34-180">**Przepływ danych**</span><span class="sxs-lookup"><span data-stu-id="3ef34-180">**Data Flow**</span></span> | <span data-ttu-id="3ef34-181">Binarny, ALPC, HTTP, HTTPS/protokoły TLS/SSL, IOCTL, IPSec, o nazwie potoku, RPC i modelu DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="3ef34-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="3ef34-182">**Obramowanie/granic zaufania**</span><span class="sxs-lookup"><span data-stu-id="3ef34-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="3ef34-183">Sieci firmowe, Internet, maszyny, piaskownicy, trybu jądra/użytkownika</span><span class="sxs-lookup"><span data-stu-id="3ef34-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="3ef34-184">Uwagi dotyczące/wiadomości</span><span class="sxs-lookup"><span data-stu-id="3ef34-184">Notes/Messages</span></span>

| <span data-ttu-id="3ef34-185">Składnik</span><span class="sxs-lookup"><span data-stu-id="3ef34-185">Component</span></span>                               | <span data-ttu-id="3ef34-186">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="3ef34-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="3ef34-187">**Komunikaty**</span><span class="sxs-lookup"><span data-stu-id="3ef34-187">**Messages**</span></span> | <span data-ttu-id="3ef34-188">Logiki wewnętrzne narzędzie, które generuje alerty dla użytkownika przy każdym wystąpieniu błędu, takie jak Brak przepływów danych między elementami</span><span class="sxs-lookup"><span data-stu-id="3ef34-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="3ef34-189">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="3ef34-189">**Notes**</span></span> | <span data-ttu-id="3ef34-190">Ręczne uwagi pliku toohello dodanych przez zespoły inżynieryjne w całości w hello projektu i przegląd procesu</span><span class="sxs-lookup"><span data-stu-id="3ef34-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="3ef34-191">Właściwości elementu</span><span class="sxs-lookup"><span data-stu-id="3ef34-191">Element properties</span></span>

<span data-ttu-id="3ef34-192">Te różnią się zależnie od elementów hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="3ef34-192">These vary by hello elements selected.</span></span> <span data-ttu-id="3ef34-193">Oprócz granice zaufania wszystkie inne elementy zawierają 3 Opcje ogólne:</span><span class="sxs-lookup"><span data-stu-id="3ef34-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="3ef34-194">Właściwości elementu</span><span class="sxs-lookup"><span data-stu-id="3ef34-194">Element Property</span></span>                               | <span data-ttu-id="3ef34-195">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="3ef34-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="3ef34-196">**Nazwa**</span><span class="sxs-lookup"><span data-stu-id="3ef34-196">**Name**</span></span> | <span data-ttu-id="3ef34-197">Przydatne w przypadku nazw toobe Twojego procesów, magazynów i obiektów interakcji przepływów czytelna</span><span class="sxs-lookup"><span data-stu-id="3ef34-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="3ef34-198">**Poza zakresem**</span><span class="sxs-lookup"><span data-stu-id="3ef34-198">**Out of Scope**</span></span> | <span data-ttu-id="3ef34-199">Jeśli zaznaczone, hello elementu jest pobierana poza macierzy generacji zagrożeń hello (niezalecane)</span><span class="sxs-lookup"><span data-stu-id="3ef34-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="3ef34-200">**Przyczyna poza zakresem**</span><span class="sxs-lookup"><span data-stu-id="3ef34-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="3ef34-201">Justowanie pola toolet użytkownicy wiedzieli, dlaczego poza zakresem wybrano</span><span class="sxs-lookup"><span data-stu-id="3ef34-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="3ef34-202">Właściwości zostały zmienione w każdej kategorii elementu.</span><span class="sxs-lookup"><span data-stu-id="3ef34-202">Properties are changed under each element category.</span></span> <span data-ttu-id="3ef34-203">Kliknij każdy element tooinspect hello dostępnych opcji lub Otwórz toolearn szablonu hello więcej.</span><span class="sxs-lookup"><span data-stu-id="3ef34-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="3ef34-204">Załóż na powitania funkcji.</span><span class="sxs-lookup"><span data-stu-id="3ef34-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="3ef34-205">Ekran powitalny</span><span class="sxs-lookup"><span data-stu-id="3ef34-205">Welcome screen</span></span>

<span data-ttu-id="3ef34-206">ekran powitalny Hello jest hello najpierw zostanie wyświetlony po otwarciu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3ef34-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="3ef34-207">Otwieranie modelu</span><span class="sxs-lookup"><span data-stu-id="3ef34-207">Open A model</span></span>

<span data-ttu-id="3ef34-208">Ustawiając kursor nad przycisk "Otwórz w modelu" zawiera opcje ukryta 2: "Otwórz w tym komputerze" i "Otwieranie z poziomu usługi OneDrive."</span><span class="sxs-lookup"><span data-stu-id="3ef34-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="3ef34-209">Hello otwierania hello Otwieranie pliku ekranu, gdy hello drugi prezentująca hello logowania procesu dla usługi OneDrive, umożliwiając toopick folderów i plików po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="3ef34-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![Otwieranie modelu](./media/azure-security-threat-modeling-tool/openmodel.png)

![Otwórz z komputera lub usługi OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="3ef34-212">Opinie i sugestie problemów</span><span class="sxs-lookup"><span data-stu-id="3ef34-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="3ef34-213">Wybranie tej opcji spowoduje przejście toohello fora MSDN dla narzędzi do tworzenia oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="3ef34-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="3ef34-214">To doskonały sposób toocheck się inne osoby mówią o narzędziu hello, w tym rozwiązania i nowe pomysły.</span><span class="sxs-lookup"><span data-stu-id="3ef34-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![Opinia](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="3ef34-216">Widok projektu</span><span class="sxs-lookup"><span data-stu-id="3ef34-216">Design view</span></span>

<span data-ttu-id="3ef34-217">Przy każdym otwarciu lub utworzyć nowy model spowoduje przekierowanie toohello widoku Projekt.</span><span class="sxs-lookup"><span data-stu-id="3ef34-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="3ef34-218">Dodawanie elementów</span><span class="sxs-lookup"><span data-stu-id="3ef34-218">Adding elements</span></span>

<span data-ttu-id="3ef34-219">Istnieją 2 metody tooadd elementów siatki hello:</span><span class="sxs-lookup"><span data-stu-id="3ef34-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="3ef34-220">**Przeciągnij i upuść** — przeciągnij hello żądany element toohello siatki, a następnie użyj hello elementu właściwości tooprovide dodatkowe informacje.</span><span class="sxs-lookup"><span data-stu-id="3ef34-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="3ef34-221">**Kliknij prawym przyciskiem myszy** — prawym przyciskiem myszy kliknij w dowolnym miejscu na powitania siatki i wybierz z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="3ef34-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="3ef34-222">Ogólny reprezentacja elementu będą wyświetlane na ekranie powitania.</span><span class="sxs-lookup"><span data-stu-id="3ef34-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="3ef34-223">Łączenie elementów</span><span class="sxs-lookup"><span data-stu-id="3ef34-223">Connecting elements</span></span>

<span data-ttu-id="3ef34-224">Istnieją 2 metody tooconnect elementów w narzędziu hello:</span><span class="sxs-lookup"><span data-stu-id="3ef34-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="3ef34-225">**Przeciągnij i upuść** — przeciągnij hello żądaną przepływu danych toohello siatki i połączyć z obu końców toohello odpowiednich elementów.</span><span class="sxs-lookup"><span data-stu-id="3ef34-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="3ef34-226">**Kliknij pozycję + Shift** — kliknięcie pierwszego elementu hello (wysyłanie danych), naciśnij i przytrzymaj klawisz Shift hello, a następnie wybierz hello drugiego elementu (odbieranie danych).</span><span class="sxs-lookup"><span data-stu-id="3ef34-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="3ef34-227">Kliknij prawym przyciskiem myszy i wybierz opcję "Połącz".</span><span class="sxs-lookup"><span data-stu-id="3ef34-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="3ef34-228">Jeśli używasz przepływu danych dwukierunkowe hello kolejność nie jest równie ważne.</span><span class="sxs-lookup"><span data-stu-id="3ef34-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="3ef34-229">Właściwości</span><span class="sxs-lookup"><span data-stu-id="3ef34-229">Properties</span></span>

<span data-ttu-id="3ef34-230">Zawiera wszystkie właściwości hello, które mogą być modyfikowane wzorników hello umieszczone na diagramie hello.</span><span class="sxs-lookup"><span data-stu-id="3ef34-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="3ef34-231">właściwości hello toosee, wystarczy kliknąć wzornika hello i hello informacje zostaną odpowiednio wypełnione.</span><span class="sxs-lookup"><span data-stu-id="3ef34-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="3ef34-232">przykład Witaj poniżej przedstawia przed i po "Bazy danych" wzornika jest przeciągnięto hello diagramu:</span><span class="sxs-lookup"><span data-stu-id="3ef34-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="3ef34-233">Przed</span><span class="sxs-lookup"><span data-stu-id="3ef34-233">Before</span></span>

![Przed](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="3ef34-235">Po</span><span class="sxs-lookup"><span data-stu-id="3ef34-235">After</span></span>

![Po](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="3ef34-237">Komunikaty</span><span class="sxs-lookup"><span data-stu-id="3ef34-237">Messages</span></span>

<span data-ttu-id="3ef34-238">Tworzenie modelu zagrożeń, pamiętaj, że dane tooconnect przepływają tooelements okna wiadomość hello powiadamia tooact.</span><span class="sxs-lookup"><span data-stu-id="3ef34-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="3ef34-239">Możesz wybrać tooignore go lub wykonaj hello instrukcje toofix hello problem.</span><span class="sxs-lookup"><span data-stu-id="3ef34-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![Komunikaty](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="3ef34-241">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3ef34-241">Notes</span></span>

<span data-ttu-id="3ef34-242">Przełączanie kart z tooNotes wiadomości umożliwia możesz tooadd uwagi tooyour diagram toocapture Twoje opinie</span><span class="sxs-lookup"><span data-stu-id="3ef34-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="3ef34-243">Analityczny</span><span class="sxs-lookup"><span data-stu-id="3ef34-243">Analysis view</span></span>

<span data-ttu-id="3ef34-244">Po zakończeniu tworzenia diagramu, przełączyć widoku tooanalysis przechodząc toohello opcji menu u góry i wybieranie hello Lupa dalej toohello paint palety.</span><span class="sxs-lookup"><span data-stu-id="3ef34-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![Analityczny](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="3ef34-246">Wybór wygenerowanego zagrożeń</span><span class="sxs-lookup"><span data-stu-id="3ef34-246">Generated threat selection</span></span>

<span data-ttu-id="3ef34-247">Po kliknięciu zagrożenia można wykorzystać trzy unikatowe funkcje:</span><span class="sxs-lookup"><span data-stu-id="3ef34-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="3ef34-248">Funkcja</span><span class="sxs-lookup"><span data-stu-id="3ef34-248">Feature</span></span>                               | <span data-ttu-id="3ef34-249">Info</span><span class="sxs-lookup"><span data-stu-id="3ef34-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="3ef34-250">**Wskaźnik do odczytu**</span><span class="sxs-lookup"><span data-stu-id="3ef34-250">**Read Indicator**</span></span> | <p><span data-ttu-id="3ef34-251">Zagrożenie jest teraz oznaczona jako odczytu, które łatwo może pomóc Ci śledzić hello elementy, które już nawiązaniem</span><span class="sxs-lookup"><span data-stu-id="3ef34-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![Odczyt/nieprzeczytana wskaźnika](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="3ef34-253">**Fokus interakcji**</span><span class="sxs-lookup"><span data-stu-id="3ef34-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="3ef34-254">Zostanie wyróżniona interakcji na diagramie hello należących toothat zagrożeń</span><span class="sxs-lookup"><span data-stu-id="3ef34-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![Fokus interakcji](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="3ef34-256">**Właściwości zagrożeń**</span><span class="sxs-lookup"><span data-stu-id="3ef34-256">**Threat Properties**</span></span> | <p><span data-ttu-id="3ef34-257">Dodatkowe informacje na temat zagrożeń hello jest wypełniana w oknie właściwości hello zagrożeń</span><span class="sxs-lookup"><span data-stu-id="3ef34-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![Właściwości zagrożeń](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="3ef34-259">Priorytet zmian</span><span class="sxs-lookup"><span data-stu-id="3ef34-259">Priority change</span></span>

<span data-ttu-id="3ef34-260">Poziom priorytetu hello każde zagrożenie wygenerowanego także zmiana ich toomake kolory go łatwo tooidentify zagrożenia wysoki, średni i niski priorytet.</span><span class="sxs-lookup"><span data-stu-id="3ef34-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![Priorytet zmian](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="3ef34-262">Pola można edytować właściwości zagrożeń</span><span class="sxs-lookup"><span data-stu-id="3ef34-262">Threat properties editable fields</span></span>

<span data-ttu-id="3ef34-263">Jak pokazano w powyższy obraz powitania, użytkownicy mogą zmieniać informacji hello wygenerowany przez narzędzie hello również dodać pola toocertain informacje, takie jak uzasadnienie.</span><span class="sxs-lookup"><span data-stu-id="3ef34-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="3ef34-264">Te pola są generowane przez szablon hello, więc jeśli potrzebujesz więcej informacji na każde zagrożenie jest zachęca toomake modyfikacje.</span><span class="sxs-lookup"><span data-stu-id="3ef34-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![Właściwości zagrożeń](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="3ef34-266">Raporty</span><span class="sxs-lookup"><span data-stu-id="3ef34-266">Reports</span></span>

<span data-ttu-id="3ef34-267">Po zakończeniu zmieniania priorytetów i aktualizowania stanu hello każdego wygenerowany zagrożeń, można zapisać plik hello lub wydrukować raport będzie zbyt "raport", a następnie "Utwórz pełny raport."</span><span class="sxs-lookup"><span data-stu-id="3ef34-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="3ef34-268">Użytkownik zostanie zapytany tooname hello raportu, a gdy to zrobisz, powinny pojawić się coś podobnego toohello obraz poniżej:</span><span class="sxs-lookup"><span data-stu-id="3ef34-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![Raport](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="3ef34-270">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3ef34-270">Next steps</span></span>

<span data-ttu-id="3ef34-271">toocontribute szablonu dla społeczności hello Przejdź tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  strony.</span><span class="sxs-lookup"><span data-stu-id="3ef34-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="3ef34-272">**[Pobierz](https://aka.ms/tmtpreview)**  tooget narzędzie hello obecnie uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="3ef34-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>
