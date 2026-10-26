# Veri sözlüğü

- **Kaynak:** Google BigQuery public dataset `bigquery-public-data.crypto_ethereum.token_transfers`
  (Ethereum ERC-20 `Transfer` olayları; Google Cloud Public Datasets, açık blokzincir verisi)
- **Token:** LINK — `0x514910771af9ca656af840dff83e8264ecf986ca` (18 ondalık)
- **Zaman penceresi (UTC):** 2026-10-19 – 2026-10-25
- **Toplama tarihi:** 2026-10-26 17:48 UTC
- **Anonimleştirme:** adresler gizli bir tuzla HMAC-SHA256 → ilk 12 hex karakter (`w_` önekli). Tuz ve
  adres eşleştirme tablosu depoda yayımlanmaz.

## data/edges.csv (kenar listesi)
| Sütun | Anlamı |
| --- | --- |
| source | Gönderen cüzdanın anonim kimliği |
| target | Alıcı cüzdanın anonim kimliği |
| weight | Pencere boyunca source→target toplam transfer miktarı (LINK birimi) |
| n_transfers | Pencere boyunca source→target transfer sayısı |
| first_ts / last_ts | İlk ve son transferin zamanı (UTC, ISO 8601) |

## data/nodes.csv (düğüm listesi)
| Sütun | Anlamı |
| --- | --- |
| node_id | Anonim cüzdan kimliği |
| in_degree / out_degree | Farklı kaç cüzdandan para aldığı / kaç cüzdana gönderdiği |
| sent_amount / received_amount | Toplam gönderilen / alınan miktar (LINK) |
| sent_transfers / received_transfers | Toplam gönderim / alım işlemi sayısı |

## data/network.graphml
Aynı yönlü ağırlıklı ağ; düğüm ve kenar öznitelikleri yukarıdaki sütunlarla aynıdır (Gephi ile açılabilir).
