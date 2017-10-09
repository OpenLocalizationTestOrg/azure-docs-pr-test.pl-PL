---
title: "Omówienie tworzenia aplikacji aaaDatabase bazy danych Azure dla programu MySQL | Dokumentacja firmy Microsoft"
description: "Wprowadza zagadnienia dotyczące projektowania, które dewelopera należy stosować podczas pisania aplikacji kod tooconnect tooAzure bazy danych dla programu MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: f08df605eba21b4ba4b43565c0a7ded95779a171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-development-overview-for-azure-database-for-mysql"></a><span data-ttu-id="a059a-103">Omówienie tworzenia aplikacji dla bazy danych Azure dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="a059a-103">Application development overview for Azure Database for MySQL</span></span> 
<span data-ttu-id="a059a-104">W tym artykule omówiono zagadnienia dotyczące projektowania, które dewelopera należy stosować podczas pisania aplikacji kod tooconnect tooAzure bazy danych dla programu MySQL</span><span class="sxs-lookup"><span data-stu-id="a059a-104">This article discusses design considerations that a developer should follow when writing application code tooconnect tooAzure Database for MySQL</span></span> 

> [!TIP]
> <span data-ttu-id="a059a-105">Samouczek przedstawiający sposób toocreate serwera, utworzenie zapory na serwerze, wyświetlić właściwości serwera, Utwórz bazę danych, Połącz i zapytań przy użyciu narzędzia workbench i mysql.exe, można zobaczyć [projektowania pierwszą bazę danych MySQL na platformie Azure](tutorial-design-database-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a059a-105">For a tutorial showing you how toocreate a server, create a server-based firewall, view server properties, create database, connect and query using workbench and mysql.exe, see [Design your first Azure MySQL database](tutorial-design-database-using-portal.md)</span></span>

## <a name="language-and-platform"></a><span data-ttu-id="a059a-106">Język i platforma</span><span class="sxs-lookup"><span data-stu-id="a059a-106">Language and platform</span></span>
<span data-ttu-id="a059a-107">Dostępne są przykłady kodu dla różnych języków programowania i platform programistycznych.</span><span class="sxs-lookup"><span data-stu-id="a059a-107">There are code samples available for various programming languages and platforms.</span></span> <span data-ttu-id="a059a-108">Można skorzystać z łączy toohello przykłady kodu w: [bibliotek łączności używane tooAzure tooconnect bazy danych dla programu MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="a059a-108">You can find links toohello code samples at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="tools"></a><span data-ttu-id="a059a-109">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="a059a-109">Tools</span></span>
<span data-ttu-id="a059a-110">Bazy danych platformy Azure dla programu MySQL używa hello MySQL community wersji, zgodnej z programem MySQL popularnych narzędzi do zarządzania takich jak narzędzia Workbench lub MySQL, takich jak mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql)i inne.</span><span class="sxs-lookup"><span data-stu-id="a059a-110">Azure Database for MySQL uses hello MySQL community version, compatible with MySQL common management tools such as Workbench or MySQL utilities such as mysql.exe, [phpMyAdmin](https://www.phpmyadmin.net/), [Navicat](https://www.navicat.com/products/navicat-for-mysql), and others.</span></span> <span data-ttu-id="a059a-111">Można również używać hello portalu Azure, interfejsu wiersza polecenia Azure i toointeract interfejsów API REST z hello bazy danych usługi.</span><span class="sxs-lookup"><span data-stu-id="a059a-111">You can also use hello Azure portal, Azure CLI, and REST APIs toointeract with hello database service.</span></span>

## <a name="resource-limitations"></a><span data-ttu-id="a059a-112">Ograniczenia zasobów</span><span class="sxs-lookup"><span data-stu-id="a059a-112">Resource limitations</span></span>
<span data-ttu-id="a059a-113">Baza danych MySQL Azure zarządza serwer tooa dostępne zasoby hello przy użyciu dwóch różnych mechanizmów:</span><span class="sxs-lookup"><span data-stu-id="a059a-113">Azure MySQL Database manages hello resources available tooa server using two different mechanisms:</span></span> 
- <span data-ttu-id="a059a-114">Zarządzanie zasobami</span><span class="sxs-lookup"><span data-stu-id="a059a-114">Resources Governance</span></span> 
- <span data-ttu-id="a059a-115">Wymuszanie ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="a059a-115">Enforcement of Limits.</span></span>

## <a name="security"></a><span data-ttu-id="a059a-116">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="a059a-116">Security</span></span>
<span data-ttu-id="a059a-117">Baza danych MySQL Azure zawiera zasoby dotyczące ograniczanie dostępu, ochrona danych Konfigurowanie użytkowników i ról i monitorowanie działań na bazę danych MySQL.</span><span class="sxs-lookup"><span data-stu-id="a059a-117">Azure MySQL Database provides resources for limiting access, protecting data, configuring users and role, and monitoring activities on a MySQL Database.</span></span>

## <a name="authentication"></a><span data-ttu-id="a059a-118">Authentication</span><span class="sxs-lookup"><span data-stu-id="a059a-118">Authentication</span></span>
<span data-ttu-id="a059a-119">Baza danych MySQL Azure obsługuje uwierzytelnianie serwera użytkowników i nazwy logowania.</span><span class="sxs-lookup"><span data-stu-id="a059a-119">Azure MySQL Database supports server authentication of users and logins.</span></span>

## <a name="resiliency"></a><span data-ttu-id="a059a-120">Odporność</span><span class="sxs-lookup"><span data-stu-id="a059a-120">Resiliency</span></span>
<span data-ttu-id="a059a-121">Po wystąpieniu błędu przejściowego podczas łączenia tooMySQL bazy danych, kod powinien ponów wywołanie hello.</span><span class="sxs-lookup"><span data-stu-id="a059a-121">When a transient error occurs while connecting tooMySQL Database, your code should retry hello call.</span></span> <span data-ttu-id="a059a-122">Firma Microsoft zaleca użycie logiki ponawiania hello wycofania logiki, tak, że nie przeciąży hello bazy danych SQL z wielu klientów jednocześnie ponawianie próby.</span><span class="sxs-lookup"><span data-stu-id="a059a-122">We recommend hello retry logic use back off logic, so that it does not overwhelm hello SQL Database with multiple clients retrying simultaneously.</span></span>

- <span data-ttu-id="a059a-123">Przykłady kodu: Logika ponawiania próby przykłady kodu, które ilustrują temacie Przykłady dla języka hello wybranym w: [bibliotek łączności używane tooAzure tooconnect bazy danych dla programu MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="a059a-123">Code samples: For code samples that illustrate retry logic, see samples for hello language of your choice at: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>

## <a name="managing-connections"></a><span data-ttu-id="a059a-124">Zarządzanie połączeniami</span><span class="sxs-lookup"><span data-stu-id="a059a-124">Managing Connections</span></span>
<span data-ttu-id="a059a-125">Połączenia bazy danych są ograniczone zasobu, tak więc zaleca się użycie za pośrednictwem połączenia podczas uzyskiwania dostępu do bazy danych MySQL tooachieve lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="a059a-125">Database connections are a limited resource, so we recommend sensible use of connections when accessing your MySQL Database tooachieve better performance.</span></span>
- <span data-ttu-id="a059a-126">Hello dostępu do bazy danych przy użyciu puli połączeń lub połączeń trwałych.</span><span class="sxs-lookup"><span data-stu-id="a059a-126">Access hello database by using connection pooling or persistent connections.</span></span>
- <span data-ttu-id="a059a-127">Hello dostępu do bazy danych przy użyciu krótkich połączenia życia.</span><span class="sxs-lookup"><span data-stu-id="a059a-127">Access hello database by using short connection life span.</span></span> 
- <span data-ttu-id="a059a-128">Logika ponawiania użycia w aplikacji w punkcie hello hello próba połączenia, błędy toocatch powodu połączeń tooconcurrent osiągnięto hello maksymalna dozwolona liczba.</span><span class="sxs-lookup"><span data-stu-id="a059a-128">Use retry logic in your application at hello point of hello connection attempt, toocatch failures due tooconcurrent connections have reached hello maximum allowed.</span></span> <span data-ttu-id="a059a-129">W hello Logika ponawiania próby, ustawić krótkie opóźnienie i poczekaj losowy czas przed hello prób dodatkowego połączenia.</span><span class="sxs-lookup"><span data-stu-id="a059a-129">In hello retry logic, set a short delay, and then wait for a random time before hello additional connection attempts.</span></span>
