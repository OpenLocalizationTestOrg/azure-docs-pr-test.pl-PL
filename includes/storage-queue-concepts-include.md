## <a name="what-is-queue-storage"></a>Co to jest usługa Queue Storage?
Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS. Pojedynczy komunikat z kolejki można się too64 KB, rozmiar, a kolejka może zawierać miliony komunikatów w górę toohello całkowitego limitu pojemności konta magazynu.

Najczęstsze zastosowania usługi Queue Storage obejmują:

* Tworzenie zaległości pracy tooprocess asynchronicznie
* Przekazywanie komunikatów z roli procesu roboczego platformy Azure tooan roli sieci web platformy Azure

## <a name="queue-service-concepts"></a>Pojęcia dotyczące usługi kolejki
Hello usługa kolejki zawiera hello następujące składniki:

![Queue1](./media/storage-queue-concepts-include/queue1.png)

* **Format adresu URL:** kolejek mają hello następującego formatu adresu URL:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    Witaj następującego adresu URL dotyczy kolejki w diagramie hello:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Konto magazynu:** wszystkie dostępu tooAzure magazynu odbywa się za pomocą konta magazynu. Aby uzyskać szczegółowe informacje na temat pojemności konta magazynu, zobacz temat [Cele dotyczące skalowalności i wydajności usługi Azure Storage](../articles/storage/common/storage-scalability-targets.md).
* **Kolejka:** kolejka zawiera zestaw komunikatów. Wszystkie komunikaty muszą być w kolejce. Należy zauważyć, że nazwa kolejki hello musi być tylko małe litery. Informacje dotyczące nazewnictwa kolejek można znaleźć w temacie [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx) (Nazewnictwo kolejek i metadanych).
* **Komunikat o błędzie:** A komunikatu, w dowolnym formacie z zapasowej too64 KB. Witaj maksymalny czas, który komunikatu może pozostawać w kolejce hello wynosi 7 dni.

