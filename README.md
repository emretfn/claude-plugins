# claude-plugins

Kişisel Claude Code plugin kataloğum. Plugin'ler bu repoya kopyalanmaz; `.claude-plugin/marketplace.json` her birini kendi GitHub reposuna yönlendirir.

## Kurulum

```
/plugin marketplace add emretfn/claude-plugins
/plugin install emil@emretufan-plugins
```

Ardından `/plugin` → **Marketplaces** → `emretufan-plugins` → **Enable auto-update**.

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
