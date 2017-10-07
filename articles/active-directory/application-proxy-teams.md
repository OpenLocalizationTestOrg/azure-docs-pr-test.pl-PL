---
title: "aplikacje serwera Proxy aplikacji usługi Azure AD w zespołach aaaAccess | Dokumentacja firmy Microsoft"
description: "Za pomocą serwera Proxy aplikacji usługi Azure AD tooaccess aplikacji lokalnej za pośrednictwem Teams firmy Microsoft."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="2f0d2-103">Dostęp do aplikacji lokalnych poprzez Teams firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="2f0d2-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="2f0d2-104">Azure Active Directory serwera Proxy aplikacji daje pojedynczy znak tooon lokalnych aplikacji niezależnie od tego, gdzie się znajdujesz i Teams firmy Microsoft upraszcza współpracy wysiłków w jednym miejscu.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-104">Azure Active Directory Application Proxy gives you single sign-on tooon-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="2f0d2-105">Integrowanie hello dwa razem oznacza, że użytkownicy mogą produktywność z ich członków zespołu w każdej sytuacji.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-105">Integrating hello two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="2f0d2-106">Użytkownicy mogą dodawać chmury aplikacji tootheir zespołów kanałów [przy użyciu karty](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), ale co się stanie, jeśli jest w tej witrynie programu SharePoint lub narzędzie do planowania wszyscy korzystają z obsługiwanego lokalnie?</span><span class="sxs-lookup"><span data-stu-id="2f0d2-106">Your users can add cloud apps tootheir Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="2f0d2-107">Serwer Proxy aplikacji jest hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-107">Application Proxy is hello solution.</span></span> <span data-ttu-id="2f0d2-108">Można dodać aplikacji opublikowanych przy użyciu serwera Proxy aplikacji tootheir kanałów przy użyciu hello tego samego zewnętrzne adresy URL zawsze korzystają z tooaccess swoje aplikacje zdalnie.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-108">They can add apps published through Application Proxy tootheir channels using hello same external URLs they always use tooaccess their apps remotely.</span></span> <span data-ttu-id="2f0d2-109">I ponieważ uwierzytelnia serwer Proxy aplikacji za pomocą usługi Azure Active Directory, hello tego samego posiada środowisko rejestracji jednokrotnej za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-109">And because Application Proxy authenticates through Azure Active Directory, hello same single sign-on experience carries through.</span></span>


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="2f0d2-110">Instalowanie łącznika serwera Proxy aplikacji hello i publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="2f0d2-110">Install hello Application Proxy connector and publish your app</span></span>

<span data-ttu-id="2f0d2-111">Jeśli nie jest jeszcze, [skonfigurować serwer Proxy aplikacji dzierżawy i zainstalować łącznik hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="2f0d2-111">If you haven't already, [configure Application Proxy for your tenant and install hello connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="2f0d2-112">Następnie [opublikować aplikację lokalną](application-proxy-publish-azure-portal.md) dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="2f0d2-113">W przypadku publikowania aplikacji hello, zwróć uwagę na powitania zewnętrznego adresu URL, ponieważ użytkownicy końcowi muszą tych informacji podczas dodawania tooTeams aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-113">When you're publishing hello app, make note of hello external URL because your end users need that information when they add hello app tooTeams.</span></span>

<span data-ttu-id="2f0d2-114">Jeśli już masz aplikacje opublikowane, ale nie zapamiętuj ich zewnętrzne adresy URL, wyszukaj je hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f0d2-114">If you already have your apps published but don't remember their external URLs, look them up in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2f0d2-115">Zaloguj się, a następnie przejdź zbyt**usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje** > Wybierz aplikacji > **Serwera proxy aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-115">Sign in, then navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-tooteams"></a><span data-ttu-id="2f0d2-116">Dodaj tooTeams Twojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="2f0d2-116">Add your app tooTeams</span></span>

<span data-ttu-id="2f0d2-117">Po opublikowaniu aplikacji hello za pośrednictwem serwera Proxy aplikacji, należy poinformować użytkowników, że ich go dodać na karcie bezpośrednio w ich kanały zespołów.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-117">Once you publish hello app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="2f0d2-118">Niech wykonaj następujące trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="2f0d2-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="2f0d2-119">Przejdź toohello zespołów kanału miejscu tooadd tej aplikacji i wybierz  **+**  tooadd karty.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-119">Navigate toohello Teams channel where you want tooadd this app and select **+** tooadd a tab.</span></span>

   ![Wybierz opcję Dodaj kartę](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="2f0d2-121">Wybierz **witryny sieci Web** hello kartę Opcje.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-121">Select **Website** from hello tab options.</span></span>

   ![Dodaj witrynę sieci Web](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="2f0d2-123">Nadaj nazwę hello kartę i ustawić hello adresu URL toohello serwera Proxy aplikacji zewnętrznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-123">Give hello tab a name and set hello URL toohello Application Proxy external URL.</span></span> 

   ![Skonfiguruj kartę nazwy i adresu URL](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="2f0d2-125">Po jednego członka do zespołu dodaje kartę hello, jest wyświetlane dla wszystkich użytkowników w kanale hello.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-125">Once one member of a team adds hello tab, it shows up for everyone in hello channel.</span></span> <span data-ttu-id="2f0d2-126">Wszyscy użytkownicy, którzy mają dostęp do aplikacji toohello korzystać pojedynczego logowania jednokrotnego przy użyciu poświadczeń hello, używanego dla Teams firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-126">Any users who have access toohello app get single sign-on access with hello credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="2f0d2-127">Wszyscy użytkownicy, którzy nie mają dostępu do aplikacji toohello zostanie wyświetlony na karcie hello w zespołach, ale dopóki przysługujące im uprawnienia toohello lokalnej aplikacji i hello Azure portalu opublikowanej wersji aplikacji hello są blokowane.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-127">Any users who don't have access toohello app will see hello tab in Teams, but are blocked until you give them permissions toohello on-premises app and hello Azure portal published version of hello app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2f0d2-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2f0d2-128">Next steps</span></span>

- <span data-ttu-id="2f0d2-129">Dowiedz się, jak za[publikowanie witryn programu SharePoint lokalnymi](application-proxy-enable-remote-access-sharepoint.md) z serwerem Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-129">Learn how too[publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="2f0d2-130">Skonfiguruj toouse Twoje aplikacje [domen niestandardowych](active-directory-application-proxy-custom-domains.md) dla ich zewnętrznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="2f0d2-130">Configure your apps toouse [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
