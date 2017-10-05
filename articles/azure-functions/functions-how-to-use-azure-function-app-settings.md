---
title: Konfiguruj ustawienia aplikacji funkcji platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak skonfigurować ustawienia aplikacji funkcji platformy Azure."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 3b23011f66592151d517d61bf806da8743f38e03
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-manage-a-function-app-in-the-azure-portal"></a><span data-ttu-id="f4590-103">Jak zarządzać aplikacji funkcji w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f4590-103">How to manage a function app in the Azure portal</span></span> 

<span data-ttu-id="f4590-104">W środowisku Azure Functions aplikacji funkcji udostępnia kontekst wykonania dla poszczególnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="f4590-104">In Azure Functions, a function app provides the execution context for your individual functions.</span></span> <span data-ttu-id="f4590-105">Funkcja zachowania aplikacji mają zastosowanie do wszystkich funkcji obsługiwanych przez aplikację danej funkcji.</span><span class="sxs-lookup"><span data-stu-id="f4590-105">Function app behaviors apply to all functions hosted by a given function app.</span></span> <span data-ttu-id="f4590-106">W tym temacie opisano sposób konfigurowania i zarządzania aplikacjami funkcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f4590-106">This topic describes how to configure and manage your function apps in the Azure portal.</span></span>

<span data-ttu-id="f4590-107">Aby rozpocząć, przejdź do [portalu Azure](http://portal.azure.com) i zaloguj się do konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f4590-107">To begin, go to the [Azure portal](http://portal.azure.com) and sign in to your Azure account.</span></span> <span data-ttu-id="f4590-108">Na pasku wyszukiwania w górnej części portalu wpisz nazwę aplikacji funkcji i wybierz ją z listy.</span><span class="sxs-lookup"><span data-stu-id="f4590-108">In the search bar at the top of the portal, type the name of your function app and select it from the list.</span></span> <span data-ttu-id="f4590-109">Po wybraniu aplikacji funkcji, można znaleźć na następującej stronie:</span><span class="sxs-lookup"><span data-stu-id="f4590-109">After selecting your function app, you see the following page:</span></span>

![Funkcja Przegląd aplikacji w portalu Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="f4590-111"><a name="manage-app-service-settings"></a>Karta Ustawienia aplikacji — funkcja</span><span class="sxs-lookup"><span data-stu-id="f4590-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Funkcja Przegląd aplikacji w portalu Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="f4590-113">**Ustawienia** karta jest, której można zaktualizować wersji środowiska uruchomieniowego funkcje używane przez aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="f4590-113">The **Settings** tab is where you can update the Functions runtime version used by your function app.</span></span> <span data-ttu-id="f4590-114">Możliwe jest również, w których zarządzasz klucze hosta używany do ograniczania dostępu HTTP do wszystkich funkcji obsługiwanych przez aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="f4590-114">It is also where you manage the host keys used to restrict HTTP access to all functions hosted by the function app.</span></span>

<span data-ttu-id="f4590-115">Funkcje obsługuje hosting zużycia i hosting planów usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4590-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="f4590-116">Aby uzyskać więcej informacji, zobacz [wybierz plan prawidłowe usługi dla usługi Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="f4590-116">For more information, see [Choose the correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="f4590-117">Dla lepszej przewidywalności w planie zużycia funkcje umożliwia ograniczenie użycia platformy ustawiając dziennego limitu przydziału wykorzystania w gigabajtach sekund.</span><span class="sxs-lookup"><span data-stu-id="f4590-117">For better predictability in the Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="f4590-118">Po osiągnięciu dziennego limitu przydziału wykorzystania funkcji aplikacji zostanie zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="f4590-118">Once the daily usage quota is reached, the function app is stopped.</span></span> <span data-ttu-id="f4590-119">Aplikacja funkcji zatrzymana z powodu osiągnięcia limitu wydatków przydziału można ponownie włączyć w tym samym kontekście ustalaniu codziennie wydatków przydziału.</span><span class="sxs-lookup"><span data-stu-id="f4590-119">A function app stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span></span> <span data-ttu-id="f4590-120">Zobacz [usługi Azure Functions cennikiem](http://azure.microsoft.com/pricing/details/functions/) szczegółowe informacje dotyczące rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="f4590-120">See the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="f4590-121">Karta funkcje platformy</span><span class="sxs-lookup"><span data-stu-id="f4590-121">Platform features tab</span></span>

![Funkcja kartę funkcje platformy aplikacji.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="f4590-123">Funkcja aplikacje uruchomione w i są obsługiwane przez platformę Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f4590-123">Function apps run in, and are maintained, by the Azure App Service platform.</span></span> <span data-ttu-id="f4590-124">W efekcie aplikacji funkcji mają dostęp do większość funkcji hosta platformy web core platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f4590-124">As such, your function apps have access to most of the features of Azure's core web hosting platform.</span></span> <span data-ttu-id="f4590-125">**Funkcji platformy** jest karta umożliwiający dostęp do wielu funkcji używanej w aplikacjach funkcji platformy aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="f4590-125">The **Platform features** tab is where you access the many features of the App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4590-126">Nie wszystkie funkcje usługi aplikacji są dostępne, po uruchomieniu aplikacji funkcji na zużycie plan hostingu.</span><span class="sxs-lookup"><span data-stu-id="f4590-126">Not all App Service features are available when a function app runs on the Consumption hosting plan.</span></span>

<span data-ttu-id="f4590-127">Pozostała część tego tematu koncentruje się na następujące funkcje usługi App Service w portalu Azure, które są przydatne w przypadku funkcji:</span><span class="sxs-lookup"><span data-stu-id="f4590-127">The rest of this topic focuses on the following App Service features in the Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="f4590-128">Edytor usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="f4590-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="f4590-129">Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="f4590-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="f4590-130">Console</span><span class="sxs-lookup"><span data-stu-id="f4590-130">Console</span></span>](#console)
+ [<span data-ttu-id="f4590-131">Zaawansowane narzędzia (Kudu)</span><span class="sxs-lookup"><span data-stu-id="f4590-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="f4590-132">Opcje wdrażania</span><span class="sxs-lookup"><span data-stu-id="f4590-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="f4590-133">CORS</span><span class="sxs-lookup"><span data-stu-id="f4590-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="f4590-134">Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="f4590-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="f4590-135">Definicja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="f4590-135">API definition</span></span>](#swagger)

<span data-ttu-id="f4590-136">Aby uzyskać więcej informacji na temat pracy z ustawieniami usługi aplikacji, zobacz [Konfigurowanie ustawień usługi aplikacji Azure](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f4590-136">For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="f4590-137"><a name="editor"></a>Edytor usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="f4590-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Funkcja aplikacji edytora usługi aplikacji.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="f4590-139">Edytor usługi aplikacji to zaawansowany edytor w portalu można modyfikować pliki konfiguracyjne w formacie JSON i podobne plików kodu.</span><span class="sxs-lookup"><span data-stu-id="f4590-139">The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike.</span></span> <span data-ttu-id="f4590-140">Wybranie tej opcji spowoduje uruchomienie na karcie przeglądarki oddzielne za pomocą edytora podstawowego.</span><span class="sxs-lookup"><span data-stu-id="f4590-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="f4590-141">Dzięki temu można zintegrować z repozytorium Git, uruchom debugowanie kodu i modyfikowanie ustawień funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4590-141">This enables you to integrate with the Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="f4590-142">Ten edytor udostępnia środowisko ulepszone dla funkcji w porównaniu z bloku domyślnym funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4590-142">This editor provides an enhanced development environment for your functions compared with the default function app blade.</span></span>    |

![Edytor usługi aplikacji](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="f4590-144"><a name="settings"></a>Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="f4590-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Funkcja aplikacji ustawienia aplikacji.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="f4590-146">Usługi aplikacji **ustawienia aplikacji** bloku jest gdzie Konfigurowanie i zarządzanie nimi framework w wersji, debugowania zdalnego, ustawienia aplikacji i parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="f4590-146">The App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="f4590-147">Po zintegrowaniu aplikacji funkcji z innymi usługami innych firm i Azure można modyfikować tych ustawień w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="f4590-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Konfigurowanie ustawień aplikacji](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="f4590-149"><a name="console"></a>Konsoli</span><span class="sxs-lookup"><span data-stu-id="f4590-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Funkcja konsoli aplikacji w portalu Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="f4590-151">Konsoli w portalu jest narzędziem idealne developer, zamiast do interakcji z aplikacją funkcji w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="f4590-151">The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line.</span></span> <span data-ttu-id="f4590-152">Typowe polecenia obejmują katalogu i tworzenie plików i nawigacji, a także wykonywanie plików wsadowych i skryptów.</span><span class="sxs-lookup"><span data-stu-id="f4590-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Funkcja aplikacji konsoli](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="f4590-154"><a name="kudu"></a>Zaawansowane narzędzia (Kudu)</span><span class="sxs-lookup"><span data-stu-id="f4590-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Funkcja aplikacji Kudu w portalu Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="f4590-156">Zaawansowane narzędzia dla aplikacji usługi (znanej także jako Kudu) zapewniają dostęp do zaawansowanych funkcji administracyjnych funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4590-156">The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app.</span></span> <span data-ttu-id="f4590-157">Program Kudu do zarządzania informacje o systemie, ustawienia aplikacji, zmienne środowiskowe, rozszerzenia lokacji, nagłówków HTTP i zmiennych serwera.</span><span class="sxs-lookup"><span data-stu-id="f4590-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="f4590-158">Można również uruchomić **Kudu** przechodząc do punktu końcowego SCM dla funkcji aplikacji, takie jak`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="f4590-158">You can also launch **Kudu** by browsing to the SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Skonfiguruj Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="f4590-160"><a name="deployment">Opcje wdrażania</span><span class="sxs-lookup"><span data-stu-id="f4590-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Funkcja opcje wdrażania aplikacji w portalu Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="f4590-162">Funkcje pozwala tworzyć kodu funkcji na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="f4590-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="f4590-163">Następnie możesz przekazać projektu aplikacji funkcji lokalnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f4590-163">You can then upload your local function app project to Azure.</span></span> <span data-ttu-id="f4590-164">Oprócz tradycyjnego przekazywania FTP funkcje umożliwia wdrażanie aplikacji przy użyciu rozwiązań popularnych ciągłej integracji, takich jak GitHub, programu VSTS Dropbox, Bitbucket i innych funkcji.</span><span class="sxs-lookup"><span data-stu-id="f4590-164">In addition to traditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="f4590-165">Aby uzyskać więcej informacji, zobacz [ciągłego wdrażania usługi Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="f4590-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="f4590-166">Aby przekazać ręcznie przy użyciu protokołu FTP lub lokalnego Git, również należy [skonfigurować poświadczenia wdrażania](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="f4590-166">To upload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="f4590-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="f4590-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Funkcja aplikacji CORS w portalu Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="f4590-169">Aby zapobiec wykonaniu złośliwego kodu w usługach, usługa aplikacji blokuje wywołania funkcji aplikacji ze źródeł zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="f4590-169">To prevent malicious code execution in your services, App Service blocks calls to your function apps from external sources.</span></span> <span data-ttu-id="f4590-170">Funkcje obsługuje współużytkowanie zasobów między źródłami (CORS), umożliwiają definiowanie "dozwolone" dozwolonych źródeł, z których funkcji może akceptować żądań zdalnych do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="f4590-170">Functions supports cross-origin resource sharing (CORS) to let you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Konfigurowanie funkcji aplikacji CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="f4590-172"><a name="auth"></a>Uwierzytelnianie</span><span class="sxs-lookup"><span data-stu-id="f4590-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Funkcja uwierzytelniania aplikacji w portalu Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="f4590-174">Korzystając z funkcji wyzwalacz protokołu HTTP, można wymagać wywołania najpierw zostać uwierzytelnione.</span><span class="sxs-lookup"><span data-stu-id="f4590-174">When functions use an HTTP trigger, you can require calls to first be authenticated.</span></span> <span data-ttu-id="f4590-175">Usługi aplikacji obsługuje uwierzytelnianie usługi Azure Active Directory i zaloguj się przy użyciu dostawców sieci społecznościowych, takich jak Facebook, firma Microsoft i Twitter.</span><span class="sxs-lookup"><span data-stu-id="f4590-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="f4590-176">Aby uzyskać więcej informacji na temat konfigurowania uwierzytelniania określonych dostawców, zobacz [omówienie uwierzytelniania w usłudze Azure App Service](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4590-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Konfigurowanie uwierzytelniania dla aplikacji funkcja](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="f4590-178"><a name="swagger"></a>Definicja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="f4590-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![Funkcja aplikacji z interfejsu API programu swagger definicji w portalu Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="f4590-180">Funkcje obsługuje struktury Swagger, aby umożliwić klientom łatwo korzystać z funkcji wyzwalanych przez protokół HTTP.</span><span class="sxs-lookup"><span data-stu-id="f4590-180">Functions supports Swagger to allow clients to more easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="f4590-181">Aby uzyskać więcej informacji na temat tworzenia definicji interfejsu API z programu Swagger, odwiedź stronę [wprowadzenie do aplikacji interfejsu API, ASP.NET i struktury Swagger na platformie Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f4590-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="f4590-182">Umożliwia także funkcje serwera proxy do definiowania pojedynczą powierzchnię interfejsu API dla wielu funkcji.</span><span class="sxs-lookup"><span data-stu-id="f4590-182">You can also use Functions Proxies to define a single API surface for multiple functions.</span></span> <span data-ttu-id="f4590-183">Aby uzyskać więcej informacji, zobacz [Praca z serwerów proxy funkcji Azure](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="f4590-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Konfigurowanie funkcji aplikacji interfejsu API](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="f4590-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f4590-185">Next steps</span></span>

+ [<span data-ttu-id="f4590-186">Konfigurowanie ustawień usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="f4590-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="f4590-187">Ciągłe wdrażanie dla usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f4590-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



