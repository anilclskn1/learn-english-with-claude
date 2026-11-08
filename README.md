# Dil Öğrenme Skill'leri — Kurulum Adımları

Instagram videosundaki 3 araç + 1 bonus: Claude'u ücretsiz dil öğretmenine çeviren skill'ler. Dört aracın hepsi ücretsiz ve açık kaynak. Her birini Claude Code'da kurup denedim; aşağıdaki adımlar o denemeden.

📄 Aynı rehber PDF olarak: [Kurulum-Adimlari.pdf](Kurulum-Adimlari.pdf)

| | Araç | Ne yapıyor |
|---|---|---|
| 1 | [English Coach](https://github.com/tianmind-studio/english-coach) | Claude'la konuşurken İngilizce hatalarını düzeltip nedenini anlatıyor |
| 2 | [Language Tutor](https://github.com/gislio/claude-language-tutor) | Seviyeni ölçüyor (okuma, yazma, konuşma) ve sana özel çalışma planı çıkarıyor |
| 3 | [Anki MCP](https://github.com/ankimcp/anki-mcp-server-addon) | Bilmediğin kelimeleri Anki'ye kart olarak kendisi ekliyor |
| 🎁 | [Fluent](https://github.com/m98/fluent) | Claude'un içinde Duolingo gibi, her dilde |

---

## Başlamadan

- **Claude Code** kurulu olmalı: [claude.ai/code](https://claude.ai/code) sayfasındaki tek satırlık komutu Terminal'e yapıştır, Claude hesabınla giriş yap. Üç araç (English Coach, Language Tutor, Fluent) Claude Code'da çalışıyor.
- Her araç için ayrı bir klasör aç (örnek: Masaüstü'nde `ingilizce`). Terminal'de `cd ~/Desktop/ingilizce` yaz, sonra `claude` yaz. İlk açılışta "Yes, I trust this folder" seç.
- Anki MCP için bilgisayarda **Anki** uygulaması da kurulu ve açık olmalı ([apps.ankiweb.net](https://apps.ankiweb.net/), ücretsiz).
- Araçlar senin Claude kullanım limitinden harcar. Seviye testi gibi uzun işlerde limit dolarsa bekleyip devam et.

---

## 1. English Coach

Yapımcı: [tianmind-studio/english-coach](https://github.com/tianmind-studio/english-coach). Claude'la normal konuşurken önce cevap veriyor, sonra İngilizce hatalarını düzeltip küçük bir ders ekliyor.

### Kurulum (benim denediğim yol)

1. GitHub sayfasında yeşil **Code → Download ZIP**. ZIP'i aç.
2. İçindeki `english-coach` klasörünü (içinde `SKILL.md` olan) `~/.claude/skills/` klasörüne kopyala. Finder'da Cmd+Shift+G → `~/.claude/skills` yaz; klasör yoksa oluştur.
3. Terminal'de `claude` yaz.

Alternatif tek komut (projenin README'sindeki):

```bash
npx skills add tianmind-studio/english-coach -a claude-code -g -y
```

### Kullanım

1. Komutla mesajı birlikte yaz: `/english-coach Hi! I am going to London next month...`
2. Claude önce cevap veriyor, sonra **English Corrections** bölümünde hataları kategoriyle gösteriyor (Grammar, Expression…), en sonda bir gramer ipucu veriyor.
3. Konuşmaya İngilizce devam et; tekrar eden hataları ayrıca işaretliyor.

Denemede yakaladıkları: "some advices" → "some advice", "for prepare" → "to prepare", "little bit nervous" → "a little bit nervous".

---

## 2. Language Tutor

Yapımcı: [gislio/claude-language-tutor](https://github.com/gislio/claude-language-tutor). 5 skill'den oluşuyor: seviye testi (assessor), ders (session), kelime tekrarı (vocab), ilerleme raporu (tracker), okuma materyali (immersion). Her dilde çalışıyor.

### Kurulum

1. GitHub sayfasından 5 `.skill` dosyasını indir (Code → Download ZIP).
2. `.skill` dosyası aslında bir ZIP. Her birini aç, çıkan klasörü (`langtutor-assessor` vb.) `~/.claude/skills/` içine kopyala. Ben böyle kurdum.
3. Yapımcıya göre dosyaya çift tıklayıp Claude masaüstü uygulamasına da kurulabiliyor; bu yolu denemedim.

### Kullanım

1. Bilgileri tek mesajda ver:
   ```
   /langtutor-assessor İngilizce öğrenmek istiyorum. Ana dilim Türkçe. Hedefim iş toplantılarında akıcı konuşmak. Günde 30 dakikam var.
   ```
2. 5 soru soruyor; İngilizce cevapla, hatalı olmasından korkma.
3. Kayıt için izin isterse **1. Yes** seç. Profili ve planı `Language-Tutor/learner-data/` klasörüne yazıyor.
4. Sonuç: her beceri için ayrı seviye (bende genel B1, konuşma A2+), tekrarlayan hatalar, haftalık plan ve kilometre taşları.
5. Sonra derse geç: `/langtutor-session`.

---

## 3. Anki MCP

Yapımcı: [ankimcp](https://github.com/ankimcp/anki-mcp-server-addon) (topluluk projesi, Anki'nin resmi aracı değil). Claude, Anki'de doğrudan deste ve kart oluşturuyor.

### Kurulum (benim denediğim yol: AnkiMCP eklentisi)

1. Anki'yi aç → **Araçlar → Eklentiler → Eklenti Al** → kod: `124672614` → Tamam. Anki'yi kapatıp yeniden aç.
2. Üst çubukta **AnkiMCP** yazısı görünüyorsa eklenti çalışıyor (adres: `http://127.0.0.1:3141`).
3. Terminal'de çalışacağın klasöre gir ve şunu yaz:
   ```bash
   claude mcp add --transport http anki http://127.0.0.1:3141/ -s project
   ```
4. `claude` yaz. "New MCP server found" sorusunda **Use this MCP server** seç.
5. Kontrol: `/mcp` yaz; listede `anki` yanında ✔ görmelisin.

### Kullanım

1. Anki açık kalsın.
2. Örnek mesaj:
   ```
   Bu paragraftaki B1-B2 seviyesindeki kelimeleri bul. Anki'de "İngilizce Kelimeler" adında bir deste aç ve her biri için kart ekle: ön yüz İngilizce kelime ve paragraftaki cümlesi, arka yüz Türkçe anlamı. Paragraf: "..."
   ```
3. Claude her araç kullanımında izin isterse **Yes** de.
4. Bende 9 kart, 14 saniyede istediğim desteye düştü. Anki'de desteye tıkla → **Şimdi Çalış**.

---

## 🎁 Bonus: Fluent

Yapımcı: [m98/fluent](https://github.com/m98/fluent) (~300 yıldız, en popüler olanı). Duolingo tadında: seviye, seri (streak), aralıklı tekrar, yazma/konuşma/okuma modları. Her dilde çalışıyor; Python 3.8+ istiyor (Mac'te genelde kurulu).

### Kurulum

1. Terminal'de:
   ```bash
   claude plugin marketplace add m98/fluent
   ```
2. Sonra:
   ```bash
   claude plugin install fluent@m98
   ```
3. Claude Code'u yeniden aç.

### Kullanım

1. `/fluent-setup` yaz. Menülerden seç: öğreneceğin dil, ana dilin, seviyen, hedefin, süre, günlük dakika.
2. Dosya oluştururken izin sorarsa **2** (bu oturum için `~/.claude` klasöründe düzenlemeye izin ver) seç.
3. Kurulum bitince "yes" yazma; ilk dersi kendin başlat: `/fluent-learn`.
4. Menüde numara seçmek de dersi başlatmıyor. Kelime için doğrudan `/fluent-vocab`, yazma için `/fluent-writing` yaz.
5. Bende Almanca A1 ile başladı; "danke shön" yazınca düzeltti ve "ö" harfini Türkçeyle açıkladı.

---

## Denemede çıkan sorunlar

| Sorun | Neden | Çözüm |
|---|---|---|
| Anki'de kartlar "Varsayılan" desteye düştü, Claude ise doğru desteye ekledim dedi | İlk denemede AnkiConnect eklentisinin GitHub kopyası + Node MCP sunucusu kullandım; yeni Anki sürümünde deste adını yok saydı | AnkiMCP eklentisine (kod `124672614`) geçtim; kartlar doğru desteye gitti. AnkiWeb'deki AnkiConnect sürümünü denemedim |
| Fluent'te "yes" deyince ders başlamadı | Fluent'in ders skill'leri yalnızca kullanıcı komutla başlatınca çalışıyor | `/fluent-learn` veya `/fluent-vocab` komutunu kendin yaz |
| Fluent kuruluyken başka bir klasördeki Claude da Fluent'i çağırmaya çalıştı | Eklenti kullanıcı genelinde kurulu | Kullanmadığın zaman `claude plugin disable fluent@m98` |
| Language Tutor kayıt yaparken izin sordu | Dosya yazmak için komut çalıştırıyor | **1. Yes** seç; tehlikeli değil, sadece kendi klasörüne yazıyor |

---

## Kaynaklar

- [English Coach](https://github.com/tianmind-studio/english-coach)
- [Language Tutor](https://github.com/gislio/claude-language-tutor)
- [AnkiMCP eklentisi](https://github.com/ankimcp/anki-mcp-server-addon)
- [Fluent](https://github.com/m98/fluent)
- [Anki](https://apps.ankiweb.net/)
