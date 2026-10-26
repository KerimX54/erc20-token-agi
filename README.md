# ERC-20 Token Transfer Ağı: Motif Analizi

**Sosyal Ağ Analizi · Yakup Kerim Tilki · 2516016032**

**Araştırma sorusu:** Token transferleri birkaç "balina" ve borsa adresi etrafında mı yoğunlaşıyor?
Hangi üçlü motifler sık görülüyor?

**Bulgunun tek cümlelik özeti:** _(final teslimde eklenecek)_

## Durum

- [x] Veri toplama scripti (BigQuery) ve tekrarlanabilir ağ kurma
- [x] Kenar listesi (CSV) + GraphML + veri sözlüğü
- [x] Temel istatistikler: düğüm, kenar, yoğunluk, bileşenler → [`results/temel_istatistikler.md`](results/temel_istatistikler.md)
- [ ] Merkeziyetler, derece dağılımı (powerlaw), topluluk tespiti (Louvain/Leiden)
- [ ] Null model (100+ configuration model), ağırlıklı derece Gini'si, üçlü motif z-skorları, borsa etiketleri
- [ ] Poster (A3), etkileşimli ağ, rapor, sunum

## Veri ve ağ tanımı

- **Kaynak:** Google BigQuery `bigquery-public-data.crypto_ethereum.token_transfers` (açık Ethereum verisi)
- **Kapsam:** tek token, bir haftalık transferler (ayrıntılar: [`veri_sozlugu.md`](veri_sozlugu.md))
- **Düğüm:** cüzdan adresi, tuzlu HMAC-SHA256 ile anonimleştirilmiş
- **Kenar:** gönderen → alıcı (yönlü). Para akışının yönü, "balina"ların toplayıcı mı dağıtıcı mı olduğunu
  ve üçlü motifleri (ör. A→B→C zinciri, A←B→C dağıtım) ayırt etmek için gereklidir.
- **Ağırlık:** toplam transfer miktarı (ek öznitelik: transfer sayısı). Miktar, "balina" yoğunlaşmasını
  ölçmek için; transfer sayısı ise etkileşim sıklığı için kullanılır.
- **Çıkarılanlar:** `0x000…000` (mint/burn; gerçek bir cüzdan değil) ve kendine transferler.

## Dosyalar

| Dosya | İçerik |
| --- | --- |
| `01_veri_toplama.ipynb` | Veri toplama, temizleme, anonimleştirme, ağ kurma, temel istatistikler |
| `data/edges.csv` | Kenar listesi (source, target, weight, n_transfers, first_ts, last_ts) |
| `data/nodes.csv` | Düğüm listesi (dereceler, gönderilen/alınan miktar) |
| `data/network.graphml` | Gephi ile açılabilen ağ dosyası |
| `results/temel_istatistikler.md` | Temel ölçüler tablosu |
| `veri_sozlugu.md` | Sütunlar, toplama tarihi, kaynak ve lisans |

## Çalıştırma

1. Defteri Google Colab'da açın (`File → Upload notebook`).
2. İlk hücrede `PROJECT_ID` değerini kendi Google Cloud projenizle değiştirin (BigQuery sandbox ücretsizdir).
3. `Runtime → Run all`. Anonimleştirme tuzu sorulur; aynı tuzla aynı kimlikler yeniden üretilir.
4. Rastgele tohum sabittir (`SEED = 42`).

Yerelde: `pip install -r requirements.txt` ve `gcloud auth application-default login`.

## Etik ve gizlilik

Cüzdan adresleri yayımlanmaz; yalnızca anonim kimlikler paylaşılır. Tuz ve adres eşleştirme tablosu
(`private/`) depoya eklenmez. Bulgular ağ yapısını betimler; nedensellik iddiası taşımaz.

## CV cümlesi

_(final teslimde eklenecek)_

## Yapay zekâ kullanım beyanı

- **Claude (Anthropic):** Ödev metninin ara kontrol adımlarına ayrılması ve `01_veri_toplama.ipynb`
  defterinin ilk taslağı (BigQuery sorgusu, anonimleştirme, temel istatistikler).
  _(Çıktıyı nasıl kontrol ettiğinizi/değiştirdiğinizi kendi cümlelerinizle yazın.)_
