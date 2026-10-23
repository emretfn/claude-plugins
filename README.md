# claude-plugins

Kişisel Claude Code plugin kataloğum. Plugin'ler bu repoya kopyalanmaz; `.claude-plugin/marketplace.json` her birini kendi GitHub reposuna yönlendirir.

## Kurulum

```
/plugin marketplace add emretfn/claude-plugins
/plugin install emil@emretufan-plugins
/plugin install cloudflare@emretufan-plugins
```

Ardından `/plugin` → **Marketplaces** → `emretufan-plugins` → **Enable auto-update**.

## Plugin'ler ve skill'ler

Skill'ler `/<plugin>:<skill>` olarak çağrılır, örneğin `/emil:animate`. ✋ işaretliler yalnızca elle çağrılır; Claude onları kendiliğinden kullanmaz.

Liste elle tutuluyor ve upstream'in gerisinde kalabilir. Kurulu olanın güncel listesi: `claude plugin details <plugin>`.

### `emil` — [emilkowalski/skills](https://github.com/emilkowalski/skills)

UI, animasyon ve tasarım mühendisliği.

| Skill | Ne yapar |
| :- | :- |
| `emil-design-eng` | Ana skill: UI cilası, bileşen tasarımı ve animasyon kararlarına dair genel yaklaşım |
| `animate` | Sıfırdan animasyon kurar; eğri, süre, özellik ve kesilme davranışını doğru sırayla seçer |
| `animate-expo` | React Native / Expo için aynısı: Reanimated, jestler, sheet'ler, haptics |
| `animation-performance` | Kare düşüren animasyonları düzeltir; composite-only özellikler, `will-change`, CSS vs JS |
| `animation-vocabulary` | Tarif ettiğin efektin doğru adını bulur ("popover açılınca zıplayan şey" → Pop in) |
| `apple-design` | Apple'ın arayüz ve akıcı hareket ilkeleri, web'e uyarlanmış hâli |
| `find-animation-opportunities` | Animasyon eklenmesi gereken (ve gerekmeyen) yerleri bulur; kod yazmaz |
| `improve-animations` | Kod tabanındaki animasyonları denetler, öncelikli uygulama planları çıkarır; kod yazmaz |
| `review-animations` ✋ | Animasyon kodunu Emil'in kurallarına göre sıkı biçimde inceler |
| `mobile-native` | Web uygulamasının telefonda native hissettirmesi: hover, 100vh, safe area, input zoom |
| `break-ui` | Bileşeni en kötü durum verisiyle zorlar ve kırılan her şeyi düzeltmesiyle raporlar |
| `ask-sonner` | Sonner toast kütüphanesi için kurulum, stil ve sorun giderme rehberi |
| `pick-ui-library` ✋ | İş için doğru, güvenilir UI kütüphanesini seçer |
| `prototype` ✋ | Bir UI parçasının birkaç farklı versiyonunu kurar, aralarında geçiş yapılır |
| `write-swift` | Modern Swift: value type'lar, Swift 6 concurrency, generics, Swift Testing |

### `cloudflare` — [cloudflare/security-audit-skill](https://github.com/cloudflare/security-audit-skill)

| Skill | Ne yapar |
| :- | :- |
| `security-audit` | Çok aşamalı güvenlik denetimi; bulguları bağımsız doğrular ve makine tarafından okunabilir rapor üretir |

## Yeni plugin eklemek

`plugins` dizisine bir kayıt ekleyin:

```json
{
  "name": "kisa-ad",
  "description": "Ne işe yaradığı",
  "source": { "source": "url", "url": "https://github.com/sahip/repo.git" }
}
```

- Kaynağı `github` + `owner/repo` yerine tam `https://` adresiyle verin: bu makinede GitHub SSH anahtarı yok ve `github` kaynakları oturum içi güncellemelerde HTTPS'e geçmiyor.
- Hedef repoda skill'ler `skills/<ad>/SKILL.md` düzenindeyse başka bir şey gerekmez.
- Skill'ler bir alt klasördeyse `git-subdir` kullanın: `{ "source": "git-subdir", "url": "https://github.com/sahip/repo.git", "path": "alt/klasor" }`.
- `version` yazmayın: yazılmazsa her upstream commit yeni sürüm sayılır ve auto-update onu çeker.

Push etmeden önce kontrol: `claude plugin validate .`
