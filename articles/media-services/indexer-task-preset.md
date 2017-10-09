---
title: "aaaTask ustawienia wstępnego dla indeksatora multimediów Azure"
description: "Ten temat zawiera omówienie zadań ustawień dla usługi Azure Media indeksatora."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ca0b3e7aa9f6dd9fdecddfc5b3137281ed5cef35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Zadanie ustawień dla indeksatora multimediów Azure

Azure Media indeksatora jest procesor multimediów, że używasz hello tooperform następujące zadania: udostępnianie plików multimedialnych i treści można wyszukiwać, generowanie zamkniętego śledzi podpisów i słów kluczowych, indeksu pliki zasobów, które są częścią zawartości.

W tym temacie opisano hello zadań ustawień potrzebnych tooyour toopass indeksowania zadania. Aby uzyskać pełny przykład, zobacz [indeksowania plików multimedialnych na pliki z usługi Azure Media indeksatora](media-services-index-content.md).

## <a name="azure-media-indexer-configuration-xml"></a>Plik XML konfiguracji indeksatora multimediów Azure

Witaj poniższej tabeli opisano elementy i atrybuty hello konfiguracji XML.

|Nazwa|Wymagane|Opis|
|---|---|---|
|Dane wejściowe|Wartość true|Pliki zasobów, które mają tooindex.<br/>Indeksator multimediów Azure obsługuje następujące formaty plików nośnika hello: MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV. <br/><br/>Można określić nazwę pliku hello (s) w hello **nazwa** lub **listy** atrybutu hello **wejściowych** elementu (jak pokazano poniżej). Jeśli nie określisz, które tooindex pliku zasobów, jest pobierany plik podstawowy hello. Jeśli plik podstawowy zasobów nie jest ustawiona, pierwszy plik zasobów wejściowych hello hello jest indeksowany.<br/><br/>tooexplicitly Określ nazwę pliku zasobów hello, czy:<br/>```<input name="TestFile.wmv" />```<br/><br/>Można również indeksu wielu plików zasobów jednocześnie (zapasowej too10). toodo to:<br/>-Utwórz plik tekstowy (plik manifestu) i nadaj mu rozszerzenie .lst.<br/>-Dodaj listę wszystkich nazw plików zasobów hello w pliku manifestu toothis zasobów wejściowych.<br/>-Dodaj zasobów toohello pliku thanifest (przekazywanie).<br/>-Podaj nazwę hello hello pliku manifestu w atrybucie listy hello danych wejściowych.<br/>```<input list="input.lst">```<br/><br/>**Uwaga:** Jeśli dodasz więcej niż 10 pliku manifestu toohello pliki zadania indeksowania hello zakończy się niepowodzeniem z kodem błędu hello 2006.|
|Metadane|wartość false|Metadane dla hello określone pliki zasobów.<br/>```<metadata key="..." value="..." />```<br/><br/>Można podać wartości dla wstępnie zdefiniowanych kluczy. <br/><br/>Obecnie są obsługiwane następujące klucze hello:<br/><br/>**Tytuł** i **opis** — używane dokładność rozpoznawania mowy tooimprove modelu tooupdate hello języka.<br/>```<metadata key="title" value="[Title of hello media file]" /><metadata key="description" value="[Description of hello media file]" />```<br/><br/>**Nazwa użytkownika** i **hasło** — używana do uwierzytelniania podczas pobierania plików internetowych za pośrednictwem protokołu http lub https.<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>Hello nazwy użytkownika i hasła wartości stosować tooall nośnika URL w manifeście wejściowych hello.|
|danych<br/><br/>Dodany w wersji 1.2. Hello obsługiwana tylko funkcja jest obecnie rozpoznawania mowy ("ASR").|wartość false|Funkcja rozpoznawania mowy Hello ma hello następujące klucze ustawień:<br/><br/>Język:<br/>-hello w pliku multimedialnym hello toobe języka naturalnego.<br/>-Angielski, hiszpański<br/><br/>CaptionFormats:<br/>-Rozdzielana średnikami lista hello potrzeby formatów podpisu danych wyjściowych (jeśli istnieje)<br/>-ttml; sami; webvtt<br/><br/><br/>GenerateAIB:<br/>-Określenie, czy plik AIB jest wymagany (na potrzeby używania z programu SQL Server i powitania klienta IFilter indeksatora) Flaga wartości logicznej. Aby uzyskać więcej informacji zobacz przy użyciu plików AIB za pomocą usługi Azure Media indeksatora i SQL Server.<br/>— Wartość PRAWDA; Wartość false<br/><br/>GenerateKeywords:<br/>-Określenie, czy wymagany jest plik XML — słowo kluczowe Flaga wartości logicznej.<br/>— Wartość PRAWDA; Wartość false.|

## <a name="azure-media-indexer-configuration-xml-example"></a>Przykład XML konfiguracji w usłudze Azure indeksatora nośnika

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of hello media file]" />  
    <metadata key="description" value="[Description of hello media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a>Następne kroki

Zobacz [indeksowania plików multimedialnych na pliki z usługi Azure Media indeksatora](media-services-index-content.md).

