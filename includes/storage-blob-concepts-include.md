## <a name="what-is-blob-storage"></a>Co to jest usługa Blob Storage?
Magazyn obiektów Blob Azure to usługa do przechowywania dużych ilości danych obiektów niestrukturalnych, takich jak dane tekstowe lub binarne, który można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS. Możesz użyć danych tooexpose magazynu obiektów Blob publicznie toohello world lub toostore danych aplikacji prywatnie.

Najczęstsze zastosowania usługi Blob Storage obejmują:

* Obrazy lub dokumentów bezpośrednio tooa przeglądarki
* Przechowywanie plików do dostępu rozproszonego
* Przesyłanie strumieniowe audio i wideo
* Zapisywanie danych w celu tworzenia kopii zapasowych, przywracania, odzyskiwania po awarii i archiwizowania
* Przechowywanie danych w celu analizy w usłudze lokalnej lub hostowanej na platformie Azure

## <a name="blob-service-concepts"></a>Pojęcia dotyczące usługi Blob
Usługa Blob Hello zawiera hello następujące składniki:

![Architektura obiektów blob](./media/storage-blob-concepts-include/blob1.png)

* **Konto magazynu:** wszystkie dostępu tooAzure magazynu odbywa się za pomocą konta magazynu. Konto magazynu może być **kontem magazynu ogólnego przeznaczenia** lub **kontem usługi Blob Storage** służącym do przechowywania obiektów/obiektów blob. Aby uzyskać więcej informacji, zobacz [About Azure storage accounts](../articles/storage/common/storage-create-storage-account.md) (Informacje o kontach usługi Azure Storage).
* **Kontener:** kontener zawiera grupowanie zestawu obiektów blob. Wszystkie obiekty blob muszą być w kontenerze. Konto może zawierać nieograniczoną liczbę kontenerów. Kontener może przechowywać nieograniczoną liczbę obiektów blob. Należy pamiętać, że czy nazwa kontenera hello muszą być małymi literami.
* **Obiekt blob:** plik dowolnego typu o dowolnym rozmiarze. Usługa Azure Storage udostępnia trzy typy obiektów blob: blokowe, stronicowe i uzupełnialne.
  
    *Blokowe obiekty blob* idealnie nadają się do przechowywania tekstu lub plików binarnych, takich dokumenty czy pliki multimedialne. *Uzupełnialne* są podobne tooblock obiekty BLOB w tym składają się z bloków, ale zoptymalizowane do operacji uzupełnialnych, więc są przydatne w scenariuszach logowania. Pojedynczy blokowy obiekt blob może zawierać zapasowej too50, 000 bloków too100 MB, rozmiar całkowity może nieco przekraczać 4,75 TB (100 MB X 50 000). Dołącz pojedynczego obiektu blob może zawierać zapasowej too50, 000 bloków too4 MB, całkowita rozmiaru nieco przekraczać 195 GB (4 MB X 50 000).
  
    *Stronicowe obiekty BLOB* może być zapasowej too1 TB, rozmiar i są bardziej efektywne w przypadku operacji częstego odczytu/zapisu. Usługa Azure Virtual Machines używa stronicowych obiektów blob jako systemu operacyjnego lub dysków z danymi.
  
    Aby uzyskać szczegółowe informacje o nazewnictwie kontenerów i obiektów blob, zobacz temat [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) (Nazewnictwo i odwoływanie się do kontenerów, obiektów blob i metadanych).

